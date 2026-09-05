# Requirements and operating characteristics

Source: `SISO-STD-002-2021.pdf`, PDF pages 20-28.

Navigation: previous [Definitions](02-definitions-pages-014-019.md) | [coverage index](README.md) | next [DIS Transmitter PDU](04-dis-transmitter-pdu-pages-029-033.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-20"></a>

## Source PDF page 20

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 20 of 90 This is an approved SISO Standard.

### 4 Requirements

### 4.1 JTIDS Operating Characteristics

JTIDS uses the principle of Time  Division Multiple Access (TDMA) to divide network time, and capacity, into divisions called time slots. Each time slot is 7.8125 milliseconds long with 128 time slots per second. Time slots are organized into three interleaved sets (A, B, and C). An epoch  is 12.8 minutes long comprised of 98,304 time slots. There are 112.5 epochs in a 24 -hour day. Therefore, the current epoch, set, and time slot number can be calculated from the current time. Operationally, groups of time slots are assigned to a common fun ction known as a Network Participation Group (NPG). Time slot assignments are published in a Network Data Load (NDL) (by a central net design agency), with participation groups identified by the time slot set, the “offset” of the time slot, and the time sl ot recurrence rate. The recurrence rate is expressed as an exponential power of 2, representing how often the time slot assigned to the NPG occurs within the set. [13] TDMA architecture requires that each JTIDS participant, know n as a JTIDS Unit (JU), must know when its transmit time slots occur. JUs must be synchronized with a common network time to receive and transmit on the network. In JTIDS, one JU in a network is designated as the Network Time Reference (NTR). [ 13] Link 16 also uses frequency hopping to provide jam resistance on the Link 16 network.  Hopping is done on a pulse by pulse basis, with each hop being 13 microseconds long which allows 76,923 hops per second. The frequency sequence is pse udo-randomly selected using a crypto variable to force any potential jammer to spread its energy over a wider frequency range when it cannot follow the sequence. [13]

### 4.1.1 General Requirements

This section describes general requireme nts for simulation of Link 16 independent of the simulation protocol used. The specific requirements for implementation under DIS are described in section  4.2. The specific requirements for implementation under HLA are described in section 4.3. 1. Simulators in compliance with this standard shall as a minimum have the capability to identify the NPG and net number of transmitted data to allow them to operate at Time Slot Allocation (TSA) level 0 and 1. 2. All Link 16 messages shall be bit encoded in accordance with the Reference 7 and Reference 8 TADIL J specification. In the specification, each time slot contains one 35 -bit header, padded to 48 b its, and  a varying number of 75 -bit messages, padded to 80 bits, unless the Message Type Identifier specifies otherwise. 3. It is not required to perform error detection encoding for the Link 16 messages. If error detection encoding is not performed, the parity bits of the 75-bit messages shall be set to 0. Usage of error detection encoding and interpretation of the parity bits may be specified in exercise agreements. 4. When the header indicates Reed -Solomon encoding, the data area shall still be comprised of non-Reed-Solomon encoded Link 16 messages. 5. Regardless of level of fidelity, all transmission modulation parameter fields shall be filled with valid data in accordance with this standard. 6. Any simulator that is not emulating JTIDS NDL throughput shall have the ability  to configure the maximum number of Link 16  words transmitted per second, but shall not exceed the JTIDS maximum of 1536 J -words per second (twelve J -words per Pack -4 Single Pulse time slot multiplied by 128 time slots per second). This upper limit shall n ot apply to JTIDS Link 16 Enhanced Throughput (LET) packets. For additional information see Reference 12.

<a id="source-pdf-page-21"></a>

## Source PDF page 21

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 21 of 90 This is an approved SISO Standard. 7. The J31.7 No Statement message is a 1 -word J Message used by terminals to pad time slot message structures to either 3, 6,  or 12 words. When issuing a Link 16 signal message, simulations may use J31.7 messages to pad to 3, 6, or 12 words in accordance with the time slot message packing format, but this is not recommended. When receiving a Link 16 signal message, simulations s hall process the message whether or not J31.7 padding is included, i.e., the receiver shall treat any missing words as J31.7 padding. 8. If the number of J Words in a signal message is greater than prescribed by the packing format, the extra J Words shall be ignored. 9. When receiving a Link 16 signal message, simulations shall only process complete J Messages that are properly formatted in terms of initial, extension, and/or continuation words IAW References 7 and 8. 10. A Link 16 signal message may include multiple J Messages. For example, in Link 16 simulation, a 6 -word time slot message packing format may be used to represent one or more J Messages as long as the total number of J Words is 6 or less. 11. Systems shall wait until their time slot occurs to transmit data in order to receive the latest update to data (i.e. , time slots shall not be “pre -sent”). Receiving systems shall buffer messages after the time slot has occurred to account for network delays. The a mount of time to buffer messages for a time slot shall be a runtime configuration item. The amount of time entered shall be the same for all participants in the same network and will cause the simulations to all “retire” a particular time slot at the same time. This effect is not important for lower levels of fidelity (TSA Levels 0, 1) but is critical for all fidelity levels that tie a message to a particular time slot along with a NDL. If the effects of messages arriving later than the time slot are not important (multiple JUs transmitting in the same time slot, contention access, or data arriving while the receiving JU is transmitting), or the physical network infrastructure has low delays (less than 3 millisecond), the buffer time can be set to a low numb er or to zero. When TSA Level 0 or 1 systems interoperate with higher -fidelity systems, the buffer has to be the same for all participants. When network is composed exclusive of TSA Level 0 and

### 1 systems, the buffer may be set to a low number or zero.

12. All systems set at TSA Level 2 or higher shall have their system times synchronized to a common time reference. Any error in the clock synchronization times (e.g. , average Network Time Protocol (NTP) error) must be added to the network delays (the buffer time)  before retiring a time slot. For real -time DIS or HLA simulation applications, NTP (or equivalent) is recommended. For non -real-time simulation applications, HLA time management is recommended. 13. All systems should have some representation of a terminal clo ck time. If medium-fidelity synchronization is to be accomplished, the system shall model a terminal clock (and its associated drift). 14. At TSA Level 2 or greater, if multiple messages are received with identical Transmission Security Encryption Codes (TSEC) , net number , and time  slot, receivers shall not process messages except from the closest transmitting entity (in the simulation space). 15. There are three communication modes for a real JTIDS/MIDS network: modes 1, 2 , and 4 (See Table 1). The selected communication mode determines whether or not the network can operate on multiple nets (by employing frequency hopping) and the transmitted data are encrypted. All JUs in a JTIDS/MIDS network must operate in the same communication mode . A. The normal JTIDS communication mode is mode 1. Frequency hopping and crypto variables shall be simulated appropriately to the specified level of fidelity. B. When operating with JTIDS communication mode 2, there will be no frequency hopping, but encryption sha ll still be used, depending on the level of fidelity. The explicit frequency of 969 MHz shall be set in the transmission message frequency field and the bandwidth will be 3 MHz. The net number in the signal message shall be zero for all transmissions (no multi-netting).

<a id="source-pdf-page-22"></a>

## Source PDF page 22

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 22 of 90 This is an approved SISO Standard. C. Mode 4 eliminates communications security in addition to the features of communications mode 2. The TSEC and MSEC encryption fields shall be set to 255 when in communications mode 4 in addition to specifying the explicit transmit frequency as in communications mode 2.

### Table 1: JTIDS Communication Modes

- `Communication Mode Frequency Hopping Data Encrypted`
### 1 Yes Yes

### 2 No Yes

### 3 Not Used Not Used

### 4 No No

16. Time slots shall be numbered sequentially, such that time slot 0 represents time slot A-1, and time slot 98303 represents C -32767. When the epoch is 112, the last valid time slot is 45151 (end of the day). 17. Generated machine receipts shall use time slots as assigned in the network description. There is no special conside ration given to machine receipts; therefore, they are treated as any other Link 16 fixed format message. 18. Relay is accomplished by transmitting relay information in assigned time slots. There is no special mechanism necessary to simulate relay transmissions. 19. Transmission messages shall be issued in accordance with Reference 4 (Issuance of the Transmitter PDU), or for as far as applicable to the equivalent HLA object, with the exception of the requirement to issue the Transmitter P DU before and after each group of Link 16 Signal PDUs, i.e., Transmitter PDU “bracketing” is not required. Transmitter PDU bracketing of Link 16 Signal PDUs is allowed but is not recommended. Once the Transmit State of the Link 16 transmitter is set to On and Transmitting, the Transmit State should remain in that mode indefinitely, i.e., until the radio is turned off or otherwise leaves the network. All other Reference 4 Transmitter PDU issuance rules apply for Link 16 simulation , including issuance for Transmit State changes and for heartbeats. When receiving transmission and signal messages, Link 16 simulations should be tolerant of implementations that use Transmitter PDU bracketing with or without Transmit State toggling, no bracketing, or other variations. 20. All information in the Link 16 Message Data field following the Link 16 Simulation Network Header of the Signal PDU, and the corresponding parameters of the HLA interactions derived from Link16RadioSignal, shall be treated a s a bit stream. The individual bit fields of the bit stream shall be packed into bytes (octets) as follows: A. Bit 0 of the first bit field shall begin at bit 0 of the first octet in the bit stream and continue until the number of bits in the field are consumed. B. Bit 0 of the next bit field shall begin in the next available bit of the current octet or in bit 0 of the next octet if all bits of the current octet have been consumed exactly. C. If insufficient bits remain in an octet for a bit field, as many bits as w ill fit in the current octet shall be consumed, then the bit field shall continue to be packed starting with bit

### 0 of the next octet.

D. Subsequent bit fields shall be packed in a like manner. E. Individual bit fields may span multiple octets as necessary to fit all bits in the bit field. See Table 17 for an example of packing the JTIDS message bit stream data starting at Octet 20. This table also shows how bytes are ordered for the Link 16 Simulation Network Header in octets 0 to 19, which is not a bit stream.

<a id="source-pdf-page-23"></a>

## Source PDF page 23

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 23 of 90 This is an approved SISO Standard.

### 4.1.2 TSA Levels of Fidelity

This protocol allows simulations to achieve different levels of fidelity by assigning one of five Time Slot Allocation (TSA) levels. If the simulator allows for a settable level of fidelity, the level of fide lity shall be set at runtime. The TSA Level shall be set in Modulation Parameter #1 of the transmitter message with an enumeration of 0-4 as described in Table 2 and Reference 3 [UID 172].

### Table 2: Link 16 Simulation TSA Levels

### TSA

Level

### TSA

Fidelity Time Synchronization Fidelity 1 Issues Recommended Usage

### 0 Low None or Low May simulate simplified

segregation of messages on separate virtual networks, but does not emulate detailed TDMA network characteristics. Data rates are not constrained. Intended for legacy use. Experiments and/or training concerned with message format and/or message content only.

### 1 Low None or Low May simulate simplified

segregation of messages on separate virtual networks, but does not emulate detailed TDMA network characteristics. Experiments and/or training where total network throughput is important. Allows for bandwidth throttling to emulate Link 16 network throughputs without assigning messages to specific time slots. Network Data Loads can be loaded into terminal simulation equipment to simulate data rates in NPGs on the Link 16 network.

### 2 Medium Low Network delay must be

sufficiently small if time slot sensitive conversations are required to duplicate live Link 16 networks (e.g., relay emulation, RELNAV, messages requiring responses). Experiments and/or training concerned with throughput limits of the Link 16 network. Also suitable for experiments/training emulating message traffic and timing of Link 16 networks without emulating effects of RTTs, RELNAV, or stacked/multi-nets.

### 3 Medium Low Same as TSA Level 2. Experiments and/or training

concerned with emulating detailed TDMA time slots and encryption associated with stacked nets, multi-nets, and crypto-nets.

### 1 Time Synchronization Fidelity levels are discussed below in section 4.1.4.

<a id="source-pdf-page-24"></a>

## Source PDF page 24

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 24 of 90 This is an approved SISO Standard.

### TSA

Level

### TSA

Fidelity Time Synchronization Fidelity 1 Issues Recommended Usage

### 4 High Medium Extremely sensitive to network

latency. Experiments and/or training concerned with effects deriving from emulation of detailed network entry timing and synchronization maintenance.

### 4.1.2.1 TSA Level 0, Low Fidelity

TSA Level 0 is the lowest  level of fidelity. For the transmitter message Modulation Parameters, the Time Slot Allocation Level field, Transmitting Terminal Primary Mode, and Transmitting Terminal Secondary Mode fields shall be populated. In addition, the Synchronization State fiel d shall be set to Fine Synchronization (3) IAW paragraph 4.1.4.1. The Network Synchronization ID shall be set to zero to indicate it is not used, or to a unique non -zero value if participation in a distinct simulated network is desired.  For the signal message Link 16 Simulation Network Header, the NPG Number, Net Number, Message Type Identifier, and SISO -STD-002 Version fields shall be populated. All bits of t he TSEC CVLL, MSEC CVLL, Time Slot ID, and Perceived Transmit Time fie lds shall be set to one to indicate a no statement/wildcard. Multiple messages are permitted in a single signal message. All messages within the signal message shall be of the same NPG Number, Net Number, and assumed packing format. Simulation participants may compare the NPG Number and Net Number values in the signal message to their own simulated terminal settings to model simplified stacked network reception effects. There is no TSA or metering with up to the maximum number of messages (as specified in t he DIS standard) packed into the data area of a single signal message. No or low-fidelity time synchronization is allowed under TSA Level 0.  No time synchronization shall be accomplished in accordance with paragraph 4.1.4.1. Low-fidelity time synchronization shall be achieved in accordance with paragraph 4.1.4.2.

### 4.1.2.2 TSA Level 1, Low Fidelity

TSA Level 1 is similar to TSA Level 0 except that there is minimal metered data. For the transmitter message, all  Modulation Parameter fields have the same valid values as TSA Level 0, except Synchronization State may be set to 2 or 3.  For the signal message, one time slot worth of information shall be in one signal message, and all Link 16 Simulation Network Header  fields shall be populated as in TSA Level 0.  No or low-fidelity time synchronization is allowed under TSA Level 1.  No time synchronization shall be accomplished in accordance with paragraph 4.1.4.1.  Low -fidelity time synchronization shall be achieved in accordance with paragraph 4.1.4.2.

### 4.1.2.3 TSA Level 2, Medium Fidelity

TSA Level 2 allows for metered data with no encryption. For the transmitter message, all Modulation Parameter fields have the same val id values as TSA Level 1.  For TSA Level 2, all signal messages shall be assigned to individual time slots (i.e., setting a valid Time Slot ID). All other Link 16 Simulation Network Header fields shall be populated as in TSA Level 1. Low -fidelity time synchronization shall be achieved in accordance with paragraph 4.1.4.2.

<a id="source-pdf-page-25"></a>

## Source PDF page 25

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 25 of 90 This is an approved SISO Standard.

### 4.1.2.4 TSA Level 3, Medium Fidelity

This level enables full TSA to include encryption. When TSA Level is set to 3, more detailed timing characteristics of stacked nets, multi-nets, and crypto-nets can be emulated. For the transmitter message, all Modulation Parameter fields are required to be populated with meaningful data.  The Synchronization State field is initially set to Initial Net Entry  (1), then progresses to Coarse Synchronization (2) when an acceptable J0.0 message is received, and then to Fine Synchronization (3) if able to transmit. The Network Synchronization ID shall be set to a non-zero, 32-bit unsigned integer generated by the NTR. For the signal message,  all Link 16 Simulation Network Header fields from TSA Level 2 are populated plus the TSEC CVLL  and MSEC CVLL fields. Low -fidelity time synchronization shall be achieved in accordance with paragraph 4.1.4.2.

### 4.1.2.5 TSA Level 4, High Fidelity

If the TSA Level is set to 4, everything from TSA Level 3 is emulated, with the addition of the medium fidelity synchronization procedures. All transmitter message Modulation Parameter fields shall be populated as described for TSA Level 3.  All Lin k 16 Simulation Network Header fields in the signal message, except Link 16 Version , shall be populated with meaningful values. Medium fidelity time synchronization shall be achieved in accordance with paragraph 4.1.4.3.

### 4.1.2.6 Fidelity Level Summary

Tables 3 and Table 4 summarize the valid field values for the different TSA Levels for Link 16 modeling for transmitter and signal messages. Signal message fields with all bits set to one are treated as a no statement/wildcard.

### Table 3: Transmitter Message Modulation Parameters - Valid Field Values for Different TSA Levels

- `Modulation`
- `Parameter #`
- `Field Name TSA Level`
### 0 1 2 3 4

### 1 Time Slot

Allocation Level

### 0 1 2 3 4

### 2 Transmitting

Terminal Primary Mode Required

### 3 Transmitting

Terminal Secondary Mode Required

### 4 Synchronization

State

### 3 2 or 3 1, 2, or 3

### 5 Network

Synchronization ID 0,  or non-zero, 32-bit unsigned integer Non-zero, 32-bit unsigned integer

<a id="source-pdf-page-26"></a>

## Source PDF page 26

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 26 of 90 This is an approved SISO Standard.

### Table 4: Signal Message Link 16 Simulation Network Header - Valid Field Values for Different TSA Levels

- `Field Name TSA Level`
### 0 1 2 3 4

NPG Number Required Net Number Required TSEC CVLL 255 Required MSEC CVLL 255 Required Message Type Identifier Required SISO-STD-002 Version Required Link 16 Version Optional (Default: “No Statement”) Time Slot ID 4 294 967 295 Required Perceived Transmit Time 4 294 967 295 and 4 294 967 295 Required

### 4.1.3 Communication Between JUs with Different Fidelity Levels

In the event tha t participants in a simulated Link 16 network cannot set their respective simulations to operate at a common TSA Level, the following procedures shall apply: 1. If a TSA Level 0 or 1  network participant attempts net entry into a simulated Link 16 network with a higher-fidelity NTR, the network participant shall follow the low-fidelity synchronization procedures in paragraph  4.1.4.2 by skipping the RTT synchronization process and may proceed to Fine Synchronization state once it rece ives a J0.0 Initial Entry message from the NTR or any IEJU. A TSA Level 0 or 1  participant should not proceed past Coarse Synchronization while its simulated terminal is in a non-transmitting (i.e., Silent) state. 2. If a higher-fidelity network participant i s in a simulated Link 16 network with a lower-fidelity NTR, the higher-fidelity participant shall either follow the low-fidelity synchronization procedures in paragraph 4.1.4.2 or achieve fine sync with other high -fidelity simulators. This may be accomplished by exchanging RTT B messages or by passively synchronizing with other available high-fidelity simulators. If no other high-fidelity simulators are available to synchronize with, the high-fidelity participant shall skip the R TT exchange, and directly enter Fine Synchronization once the J0.0 message is received. If the participant’s simulated terminal is in a non -transmit (i.e. , Silent) state, it may not proceed past Coarse Synchronization until placed in a transmitting state. 3. If the NTR is a lower-fidelity simulation and unable to simulate full NTR duties, the NTR shall still have the ability to transmit net entry messages. If a  low-fidelity simulation models time slots, then it may provide time slot information in the J0.0 mes sage continuation word, otherwise it shall set the time slot information to zero . RTT emulation is not required of lowfidelity NTRs. 4. A lower-fidelity JU entering the net shall use the Network Synchronization ID received from the NTR/IEJU in its transmitter messages. It shall then issue Precise Participant Location and Identifications (PPLIs) at the assigned rate. This is nominally once every 12 seconds (equivalent to the A -0-6 time slot block). All simulators, regardless of fidelity, shall accept another terminal’s statement of synchronization capability if the Network Synchronization ID matches its own Network Synchronization ID, or if either Network Synchronization ID is zero (i.e., wildcard).

<a id="source-pdf-page-27"></a>

## Source PDF page 27

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 27 of 90 This is an approved SISO Standard. 5. In a low-fidelity synchronization simulation, non -reception of a PPLI message pair (two PPLI messages from the same JU) for 60 seconds shall indicate that the unit has fallen out of the data link. Synchronization procedures shall be re -accomplished; i.e., reception of a PPLI message stating Fine Synchronization must occur before data from the JU will be accepted.

### 4.1.4 Time Synchronization

Modeling of Link 16 time synchronization under this standard can be implemented at one of three levels of fidelity, None, Low, or Medium as described in subsequent sections.

### 4.1.4.1 No Time Synchronization

When operating at TSA Levels 0 or 1, no NTR or time synchronization of any kind is required and the Synchronization State shall be set to Fine Synchronization (3).

### 4.1.4.2 Low-Fidelity Time Synchronization

1. Low-fidelity time synchronization is applicable  to simulation systems interested primarily in providing tactical data  link information as part of an operational scenario. The low-fidelity synchronization procedure allows such systems to exchange Link 16 messages without being encumbered by the actual exchange of RTT messages and the associated network latency. 2. When operating under low-fidelity time synchronization, systems may optionally set Synchronization State directly to Fine Synchronization (3) without starting at Coarse Synchronization (2). 3. The NTR shall begin by issuing net entry message pairs at a rate in accordance with the Link

### 16 terminal specification (typically in time slot A -0-6 at a rate of every 12 seconds). For TSA

Levels 0-2, the Network Synchronization ID may be set to zero (wildcard),  or to a unique nonzero value if low-fidelity participation in a distinct simulated network is desired. For TSA Level 3, a unique key shall populate the Network Synchronization ID field. The Transmitting Terminal Primary Mode field shall contain an NTR enumeration IAW Reference 3 [UID 173]. 4. For TSA Level 3, i f the simulated terminal is in a transmit -capable state, modulation Parameter 4 (Synchronization State) in the transmission message shall be allowed to progress to Fine Sync hronization after reception of an acceptable J0.0 Initial Entry message from the IEJU or NTR. If the simulated terminal is currently in a non -transmitting (silent) state, it may only progress to the Coarse Synchronization state until it is place d into a tr ansmitting state. Once reaching either the Coarse or Fine Synchronization state, the simulated terminal shall update its own Network Synchronization ID to match that of the accepted NTR and update its own terminal time statement to match that conveyed in t he accepted NTR’s J0.0 message.

### 4.1.4.3 Medium-Fidelity Time Synchronization

1. Medium-Fidelity Synchronization corresponds to only the high-fidelity TSA Level 4. It is applicable to those systems for which simulation of the fine synchronization methodology is paramount, potentially for high-fidelity training, network testing , and network experimentation. Because the latency of WANs (latencies up to hundreds of milliseconds) is orders of magnitude higher than in a real Link 16 network (latencies up to 3ms), this metho dology will not meet the needs of sub -millisecond accuracy. Communities with the need for sub millisecond accuracy will need to use a centralized server on a real -time operating system to simulate the microsecond intricacies of the Link 16 network. The ter m “ High-Fidelity Synchronization” will be reserved for synchronization mechanisms that are able to model the sub-millisecond accuracy of the Link 16 network. 2. The accuracy of the synchronization mechanism shall have an error less than the simulated time of propagation. The accuracy of the synchronization mechanism shall be taken into account when modeling fine synchronization.

<a id="source-pdf-page-28"></a>

## Source PDF page 28

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 28 of 90 This is an approved SISO Standard. 3. The Medium-Fidelity Synchronization procedure is as follows: A. The NTR shall begin by issuing net entry message pairs at a rate in acco rdance with the Link 16 terminal specification (typically in time slot A -0-6 at a rate of every 12 seconds). The synchronization state shall be set to Initial Net Entry (1). B. The NTR shall populate the Network Synchronization ID field with a unique randomly generated key. The Transmitting Terminal Primary Mode field shall contain an NTR enumeration IAW Reference 3 [UID 173]. At this point, the JU is considered to have achieved Coarse Synchronization. C. Before the synchronization pro cess starts, the JU shall set the Synchroni zation state to Initial Net Entry (1). The JU shall then transmit the appropriate RTT message (A or B). After RTT message transmission, the Synchronization State shall be set to Coarse Synchronization. The JU shal l use its own terminal perceived time in the Perceived Transmit Time field. D. The appropriate NTR/JU shall answer (in accordance with the Link 16 terminal specification), using the JU perceived time and the entity distance to calculate the perceived receive time. The RTT is then transmitted. E. The transmitting JU shall fill its own terminal perceived time with the received transmit time field. The formula for filling in the receive time in the RTT reply is: propagatedelayalterreply ttRTRTT  min

The tdelay is computed by: timetimedelay TTRTt  Where RTtime is the actual time held by the receiving/replying participant (Derived from NTP, GPS, etc) RT terminal is the value of the simulated Link 16 terminal clock at the receiving/replying participant. TTtime is the actual time held of transmitting participant (Derived from NTP, GPS, etc). tdelay is the difference between the receiver’s real-time clock at the time of receipt and the sender’s real-time clock at the time of transmission (i.e., it approximates the emulation network latency), and tpropagate is the propagation time of the radio frequency message in the simulated environment. This formula computes the perceived time of receipt by the receiving simulator with respect to the simulated terminal clock of the sender. 4. The originating JU shall then update its own terminal time in accordance with the simulator model and the Link 16 fine synchronization procedures. 5. After the appropriate number of RTT exchanges have occurred (depending whether the RTT A or RTT B method of synchroniza tion was used and the internal Link 16 terminal simulation model), the JU shall consider itself to be in fine synchronization and shall continually issue RTT message pairs to maintain synchronization at rates specified within the Link 16 terminal specification. Once the terminal emulator model has met the requirements for fine synchronization, normal message transmissions shall occur in accordance with References 7 and 8.

### 4.1.4.4 General Time Synchronization Provisions

General time synchronization provisions are described below.

Navigation: previous [Definitions](02-definitions-pages-014-019.md) | [coverage index](README.md) | next [DIS Transmitter PDU](04-dis-transmitter-pdu-pages-029-033.md)
