# Definitions

Source: `SISO-STD-002-2021.pdf`, PDF pages 14-19.

Navigation: previous [Overview](01-overview-pages-012-013.md) | [coverage index](README.md) | next [Requirements and operating characteristics](03-requirements-and-operating-characteristics-pages-020-028.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-14"></a>

## Source PDF page 14

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 14 of 90 This is an approved SISO Standard.

### 3 Definitions, Acronyms, and Abbreviations

English words are used in accordance with their d efinitions in the latest edition of Merriam -Webster's Collegiate Dictionary [10] except when special SISO product-related technical terms are required.

### 3.1 Definitions

Term Definition Epoch A 12.8-minute time interval consisting of 98,304 time slot intervals, each of

### 7.8125 milliseconds duration. The time slots in each epoch are organized into

three sets (A, B, or C) of 32,768 time slots each. There are 112.5 epochs in a 24-hour period. Free Text Message The Free Text Message format is a type of Link 16 message structure that uses all bits for data. A bit-oriented message whose information bits may be used to represent digitized voice, teletype, and other forms of free text information. Not the same as the fixed word format J28.2 message. In this protocol, Free Text Messages are used to support JTIDS Free Text Voice Data. Fidelity Level In terms of this standard, a fidelity level is a measure of the level of functionality of the implementation of this Link 16 Simulation standard. This allows for a standard nomenclature to be used within the community to describe the functionality of implementations of this standard. See section

### 4.1.2 for additional information and Table 2 for definitions of fidelity levels in

this standard. Fixed Word Format

### (FWF)

A 70-bit structure consisting of a formalized arrangement of predefined fields of fixed length and sequence. Fixed Word Format Message A J-Series message utilizing Fixed Word Format (FWF). An FWF message is started by an initial word that may be then followed by one or more extension and/or continuation words. Initial Entry The procedure by which a JTIDS/MIDS unit initially synchronizes with network time sufficient to receive network messages. Initial Entry JTIDS/MIDS Unit

### (IEJU)

Any JTIDS/MIDS unit that transmits the Initial Entry message in the appropriate time slot. Joint Tactical Information Distribution System

### (JTIDS)

See MIDS. JTIDS/MIDS Net A code division structure. There are 128 unique code divisions for waveform and data encryption in a time slot for the cryptovariable that may be employed during the time slot. The code division used by the terminal is by specification of a seven-bit number. JTIDS/MIDS Network The JTIDS/MIDS structure (usable only with Mode 1 communications) having a total usable capacity of 98,304 time slots per epoch per net and 128 nets. All nets are synchronized so that each time slot of each net is time-coincident with the corresponding time slot (same set and number) of every other net. The signal characteristics of all data distributed within a specified multi-netted structure are determined by a cryptographic variable in conjunction with a set of net numbers that define the structure.

<a id="source-pdf-page-15"></a>

## Source PDF page 15

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 15 of 90 This is an approved SISO Standard. Term Definition JTIDS/MIDS Unit (JU) A unit communicating directly on Link 16. JU is used within the context of this standard to indicate a simulated TADIL J terminal. JTIDS Voice Voice communications over a JTIDS network. For additional information on JTIDS voice, see References 12 and 13. J-Word JTIDS Word. Link 16 Header Word The leading bits of each message which are coded as a Reed-Solomon code word that provides 35 bits of information. Link 16 Message A functionally oriented, variable length string of one or more 70 bit words. Machine Receipt A machine verification function whereby a terminal that receives a message addressed to it retransmits a copy of that message back to the source during a later time slot, verifying the receipt of the original message. Mode 1 Communications Mode 1 JTIDS/MIDS transmissions consist of a sequence of wide-band transmission symbol packets (single pulse, 13-microsecond packets and double-pulse, 26-microsecond packets), the pulses of which are formed by continuous phase shift modulation (CPSM) of the carrier frequency. The signal processing required to transform base-band data to the JTIDS signal waveforms for transmission includes base-band data encryption, forward error correction encoding, error detection encoding, cyclic code shift keying (CCSK) encoding, data symbol interleaving, and the selection of a variable start time. Mode 2 Communications Mode 2 JTIDS/MIDS transmissions are identical to Mode 1, except that Mode

### 2 operates in the narrow-band mode.

Mode 4 Communications Mode 4 JTIDS/MIDS transmissions have signal waveform characteristics identical to Mode 2, except that Mode 4 does not employ base-band data encryption signal processing. Multifunctional Information Distribution System

### (MIDS)

The MIDS is a system which provides an Integrated Communication, Navigation, and Identification (ICNI) capability. The MIDS provides a reliable, secure, jam resistant, high capacity, ICNI capability through the use of directsequence, spread-spectrum, frequency-hopping, and error detection and correction techniques. JTIDS is synonymous with MIDS. For the purpose of this document, there is no difference. Navigation Controller The Navigation Controller establishes the origin and North orientation of the U, V relative grid for the Relative Navigation function. Net See "JTIDS/MIDS Net." Net Number A 7-bit code that identifies each net as a decimal number (0 through 127). Network See "JTIDS/MIDS Network". Network Participation Group (NPG) An agreed upon list of messages specified by label/sublabel used to support a technical function. Messages of the NPG are transmitted in time slots assigned to the JTIDS/MIDS Unit for the NPG without regard to subscriber identities. Network Time Reference (NTR) A subscriber terminal that is assigned as the reference for system time for each synchronized netted system. The NTR terminal's clock time is never updated by system information and is the reference to which all other terminals synchronize their own clocks. There is only one NTR per network.

<a id="source-pdf-page-16"></a>

## Source PDF page 16

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 16 of 90 This is an approved SISO Standard. Term Definition Network Synchronization ID An unsigned integer that identifies a simulated Link 16 network. Network Synchronization ID is a simulation-only construct which supports multiple simultaneous independent Link 16 networks.  Higher fidelity simulations also use it to simulate the Link 16 network time synchronization process. Network Synchronization ID is not to be confused with NPG Number or Net Number which are real-world constructs that support various forms of stacked nets or multi-netting within a single Link 16 network. Pulse (JTIDS/MIDS) A 6.4-microsecond burst of carrier frequency continuous phase shift modulated at a 5-megabit-per-second rate by the transmission symbol. Precise Participant Location and Identification (PPLI) The PPLI function provides network participation status, identification, and position of JUs on the Link 16 interface. Recurrence Rate The total number of time slots per epoch in a single block assignment, specified as an integer, R from 0 to 15 where 2R is the number of time slots. Reed-Solomon Code As applied to JTIDS/MIDS, a forward error correction encoding scheme. In this protocol, when Reed-Solomon encoding is indicated in the Signal PDU, the data area is still comprised of 75-bit non-Reed-Solomon encoded Link 16 messages. Relative Navigation

### (RELNAV)

A procedure used by a terminal to determine its position and velocity in a common reference coordinate system by passive observations of Position and Status messages transmitted by other terminals. To make use of RELNAV, the simulation system must achieve medium-fidelity synchronization. Round-Trip-Timing

### (RTT)

The process used by a JTIDS/MIDS terminal to directly determine the offset between its clock and that of another JTIDS/MIDS terminal. This is used to achieve and maintain fine synchronization and to improve the terminal's time quality. This process involves the exchange of RTT Interrogation and Reply Messages. RTT Addressed (RTT

### A)

The RTT A message provides the means for a JTIDS Terminal to synchronize with system time using the active synchronization procedure. A specific terminal with a time quality greater than the interrogating terminal is interrogated and responds with the RTT Reply. Typically the interrogating terminal addresses the NTR. RTT Broadcast (RTT

### B)

The RTT B message provides the means for a JTIDS Terminal to synchronize with the system time using the active synchronization procedure. The RTT B message is not addressed to a specific terminal. The interrogating terminal transmits the RTT B message on the net number of the highest time quality PPLI that it has received. Any terminal with a time quality equal or higher than that net number shall reply. RTT Reply The RTT reply message provides the means for a JTIDS terminal to support the active synchronization procedure by providing time-of-arrival data in response to either an RTT A or RTT B interrogation. Stacked Net The coordinated use of specific blocks of time slots on different nets in a JTIDS/MIDS network by different communities of users. Subscriber A participant in the use of the system, either actively (transmission of information) or passively (receiver of information only), or both.

<a id="source-pdf-page-17"></a>

## Source PDF page 17

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 17 of 90 This is an approved SISO Standard. Term Definition Synchronization Active Synchronization: A procedure used by a JTIDS/MIDS terminal to effect and maintain fine synchronization with system time based on the Round-Trip- Timing (RTT) process. Passive Synchronization: A procedure used by a terminal to effect and maintain fine synchronization with system time by passive observations of Position and Status messages transmitted by other terminals. The synchronizing terminal is not required to transmit any information. Coarse Synchronization: The state of synchronization with system time that allows a terminal to receive and process messages and to achieve fine synchronization. Fine Synchronization: The state of synchronization with system time that allows a terminal to transmit messages. A terminal may utilize a passive or an active synchronization procedure to achieve fine synchronization. Low-Fidelity Synchronization: Simulated fine synchronization without using RTT messages. Medium-Fidelity Synchronization: Simulated fine synchronization using RTT messages. Tactical Digital Information Link

### (TADIL)

A Joint Chiefs of Staff (JCS) approved standardized communications link suitable for transmission of digital information. A data link is characterized by its standardized message formats and transmission characteristic. TADIL J Tactical Digital Information Link J. A secure, jam-resistant, nodeless data link that utilizes the Joint Tactical Information Distribution System (JTIDS), and the protocols, conventions, and Link 16 fixed word message formats defined by Reference 7. TADIL TALES Tactical Digital Information Link Technical Advice and Lexicon for Enabling Simulation. Time (System) The time maintained by the terminal assigned as the Network Time Reference (NTR) to which all other participating terminals are synchronized. Time (Terminal) The estimate of system time derived by a terminal as a result of executing either the active or a passive synchronization procedure. Time Quality A measure of the quality of a terminal's state of synchronization with system time reported in the terminal's PPLI message. Time quality is reported as an integer from 0 to 15 where the higher numbers correspond to the higher levels of quality, that is, lower errors in timing. Time Slot A 7.8125-millisecond time interval during which messages may be transmitted and received. Time Slot Allocation (TSA) Level In this simulation standard a TSA level corresponds to one of five selectable levels of fidelity. See Table 2 for a description of each level. Time Slot Assignment The designation to the terminal of the specific time slot block in which it will transmit or receive messages. Time Slot Block A collection of time slots spaced uniformly in time over each epoch and belonging to a single time slot set. A block is defined by indexing time slot number (0 to 32,767) set (A, B, or C), and a recurrence rate number (0 to 15). Time Slot Number A 17-bit code that identifies each full time slot. The code consists of a 2-bit set field (set A, B, or C) and a 15-bit slot field representing the decimal numbers zero to 32,767.

<a id="source-pdf-page-18"></a>

## Source PDF page 18

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 18 of 90 This is an approved SISO Standard. Term Definition Unique Identifier Enumeration fields have values and descriptions defined in SISO-REF-010. The table for each enumeration is identified by a Unique Identifier (UID) in the form “[UID nnn]”. In this standard, references to SISO-REF-010 tables use the same UID syntax; for example, “see [UID 874]”. Variable Message Format (VMF) A message structure using predefined fields of fixed length employing internal syntax and a header extension. The internal syntax specifies the presence, absence, and recurrence of fields as selected by the user. The VMF message format is not to be confused with MIL-STD-6017.

### 3.2 Acronyms and Abbreviations

Acronym/Abbreviation Definition BOM Base Object Model C2 Command and Control CCSK Cyclic Code Shift Keying CPSM Continuous Phase Shift Modulation CVLL Crypto Variable Logic Label CVSD Continuous Variable Slope Delta (modulation) DIF Data Interchange Format DIS Distributed Interactive Simulation DM Declaration Management EDAC Error Detection and Correction FOM Federation Object Model FWF Fixed Word Format GPS Global Positioning System HLA High Level Architecture IAW In Accordance With ICNI Integrated Communications, Navigation, and Identification IEEE Institute of Electrical and Electronics Engineers IEJU Initial Entry JTIDS unit JCS Joint Chiefs of Staff JTIDS Joint Tactical Information Distribution System JU JTIDS Unit LET Link 16 Enhanced Throughput LPC Linear Predictive Coding MIDS Multifunctional Information Distribution System MIL STD Military Standard M&S Modeling and Simulation

<a id="source-pdf-page-19"></a>

## Source PDF page 19

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 19 of 90 This is an approved SISO Standard. Acronym/Abbreviation Definition MSEC Message Security Encryption Code NATO North Atlantic Treaty Organization NDL Network Data Load NPG Network Participation Group NTP Network Time Protocol NTR Network Time Reference OMT Object Model Template PDU Protocol Data Unit PPLI Precise Participant Location and Identification RPR Real-time Platform Reference RELNAV RELative NAVigation RTT Round Trip Timing SATCOM SATellite COMmunications SIMPLE Standard Interface for Multiple Platform Link Evaluation SISO  Simulation Interoperability Standards Organization STANAG STANdardization AGreement TADIL Tactical Digital Information Link TADIL J Tactical Digital Information Link J TDMA Time Division Multiple Access TDL Tactical Data Link TSA Time Slot Allocation TSEC Transmission Security Encryption Code UID Unique IDentifier UTC  Coordinated Universal Time VMF Variable Message Format WAN Wide Area Network XML Extensible Markup Language

Navigation: previous [Overview](01-overview-pages-012-013.md) | [coverage index](README.md) | next [Requirements and operating characteristics](03-requirements-and-operating-characteristics-pages-020-028.md)
