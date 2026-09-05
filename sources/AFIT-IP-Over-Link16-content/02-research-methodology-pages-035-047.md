# Research methodology

Source: `AFIT-IP-Over-Link16.pdf`, PDF pages 35-47.

Navigation: previous [Introduction and background](01-introduction-and-background-pages-012-034.md) | [coverage index](README.md) | next [Model implementation and verification](03-model-implementation-and-verification-pages-048-059.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-35"></a>

## Source PDF page 35

2-16 Security Parameters Index – 32 bits Sequence Number – 32 bits Payload Data – Variable Size Padding – 0 to 255 bytes Pad Length Next Header

Authentication Data – Variable Size

### Figure 2.5:  Encapsulating Security Payload (ESP) Format

2-7. Link-16. The purpose of Link-16 is to provide a mechanism for the exchange of real-time tactical data among units of U.S. forces, Joint Forces, and NATO forces.  Link-16 is an integral part of the Joint Battlespace Infosphere (JBI) and provides the network backbone for JBI communications.  Link-

### 16 provides Message Security (MSEC) through Type 1 Encryption, and provides Transmission

Security (TSEC) through frequency hopping. Link-16 uses the Joint Tactical Information Distribution System (JTIDS) for the communications component of Link-16.  The JTIDS data terminal encompasses the Class-2 terminal software, hardware, RF equipment, and the high-capacity, secure, anti-jam waveform that they generate [Nor01].  The JTIDS terminal is an advanced radio system that provides for the rapid exchange of tactical information among a large number of users.  The U.S. Air Force Class-2 terminal implements the Class 1 Interim JTIDS Message Specification (IJMS) protocol as well as JTIDS.  JTIDS operates in the Lx band between 960 MHz and 1215 MHz and employs the Time

<a id="source-pdf-page-36"></a>

## Source PDF page 36

2-17 Division Multiple Access (TDMA) architecture.  By using different frequencies, a technique called “frequency hopping”, multiple nets can be “stacked” through the simultaneous use of time slots. Each time slot is 7.8125 milliseconds in duration.  JTIDS provides 51 different frequencies for frequency hopping.  The frequencies assigned to JTIDS for TDMA1 transmissions vary in range from 969 MHz to 1206 MHz in 3 MHz increments.  Each pulse is transmitted on a different frequency in a pseudorandom pattern that depends on the net number and the TSEC cryptovariable.  The nominal frequency-hopping rate is greater than 33,000 hops per second [Nor01].

### 2.7.1 Data Exchange Rates.  Link-16 can transmit either 3, 6, or 12 data words in a 7.8125

msec (1/128 sec) time slot depending on whether the Standard, Packed-2, or Packed-4 data packing structure is used.  Each Link-16 data word is made up of 75 bits, of which 70 bits are data, 4 are used for parity and 1 is reserved as a spare bit.  The effective tactical data rates of Link-16 are 26.88 kilo bits per second (kbps), 53.76 kbps, or 107.52 kbps, depending on the data packing structure used.  Each 7.1825 msec time slot of unencoded information holds 450 bits at Standard packing,

### 900 bits at Packed-2 packing, and 1800 bits at Packed-4 packing.  Because error detection and

correction (EDAC) requires 16 bits for every 15 bits of data, the same time slot with Reed- Solomon encoding only holds 210, 420, and 840 bits of tactical information for the Standard, Packed-2, and Packed-4 encoding [Nor01].

### 1 Link-16 operates on the principle of Time Division Multiple Ac cess (TDMA), wherein 128 time slots per second are allocated

among all participating JTIDS Units (JU) for the origination and reception of data.

<a id="source-pdf-page-37"></a>

## Source PDF page 37

2-18 Therefore, the effective tactical data rates are calculated by multiplying the number of tactical information bits per slot by the number of slots per second, for example: • Standard packing:  210 data bits (3 × 70 bits/word) × 128 = 26.88 kbps • Standard packing with 5 parity bits:  225 (3 × 75 bits/word) × 128 = 28.80 kbps • Standard packing with EDAC:  465 (3 × 155 bits/word) × 128 = 59.52 kbps Therefore, when using EDAC, a little less than ha lf of the JTIDS word is used for data.  If EDAC is not used, then the entire word can be used for data. If the additional bits for Reed-Solomon EDAC encoding are considered, then data rates1 increase to 59.52 kbps, 119.04 kbps, and 238.08 kbps [Nor01].  Link-16 supports Link-4A and Link-112 functions as well as additional functions such as voice, navigation, and an expanded electronic warfare capability.  The table below shows a comparison to Link-11 and Link-4A common data rates.

### Table 2.1:  Link-16 Data Rate Comparison

- `Data Rates (kbps)`

- `Link`

- `Architecture`

- `Protocol`
- `Message`
- `Standard`

- `Tactical`
- `With`
- `Parity`
- `With`
### EDAC

Link-4A TDM Command/ Response V-Series R-Series

### 3.06 -- --

Link-11 Netted Polling by Net Control M-Series Fast – 1.80 Slow – 1.09 -- 2.250 1.365

Link-16 TDMA Assigned Time Slots J-Series Standard – 26.88 Packed-2 – 53.76 Packed-4 – 107.52 28.8 57.6 115.2 59.52 119.04 238.08

### 1 These data rates should not be considered “effective” data rates because they include encoding overhead, however they are

provided to give the reader an idea of actual “non-effective” bandwidth that Link-16 is capable of achieving.

### 2 Link-16 provides communication improvements over its ancestors, the Link-4A (TADIL C) and Link-11 (TADIL A/B) tactical

data link architectures.

<a id="source-pdf-page-38"></a>

## Source PDF page 38

2-19

### 2.7.2 Link-16 Data Security.  Link-16 encrypts both the message and the transmission.

Message security (MSEC) uses the KGV-8 encryption device and cryptovariables to encrypt message traffic.  Transmission security (TSEC) is also accomplished through the use of cryptovariables, which control the JTIDS waveform.  An important feature of the waveform is its use of frequency hopping.  The hopping pattern is determined by both the net number and the TSEC cryptovariable.  The TSEC cryptovariable also determines the amount of jitter in the signal, and a predetermined, pseudorandom pattern of noise that is mixed with the signal prior to transmission. 2-8. Common Object Request Broker Architecture (CORBA) CORBA, considered to be the most widely-used middleware standard, is an industrydefined specification for distributed systems.  The CORBA specifications are a product of the Object Management Group (OMG) [TaV02].  The global architecture (reference Figure 2.6) of CORBA consists of four groups of architectural elements connected to what is call the Object Request Broker (ORB). The ORB forms the core of any CORBA distributed system and is responsible for enabling communication between objects and their clients [Tav02].  In the notional architecture discussed above, CORBA objects (Cups) may reside either in the JBI server or on-board the aircraft. Security threats to CORBA objects may appear in the form of attackers attempting unauthorized access to a CORBA object or unauthorized creation of a CORBA object.  Countermeasures include the use of ORBs, which fully support the CORBA Security (CORBASec) specification, at the CORBA middleware level of the notional architecture as shown in Figure 2.6.

<a id="source-pdf-page-39"></a>

## Source PDF page 39

2-20

### Figure 2.6:  The Global Architecture of CORBA

2-9. Current Research. The following summarizes other research effort s either ongoing or completed related to this work.

### 2.9.1 Tactical Digital Information Link (TADIL) J Range Extension (JRE).  Link-16 has

proven to be an effective mode of communication for Tactical Data Links and will continue to be an integral part of military weapon’s communications systems.  The major draw back to Link-16 is it is limited to LOS communications.  However, there are several initiatives working to extend JTIDS beyond LOS.  The most common method of extending JTIDS range beyond LOS is through the employment of airborne relays.  However, this is not always possible due to lack of airborne assets.  Other means of extending beyond LOS include use of satellite communications, or use of a program called Joint Range Extension (JRE) [DGSP97]. The Joint Data Network (JDN) capacity is often strained because many participants require relays to reach Non LOS units.  A solution has been proposed using SATCOM as a means to supplement TADIL J traffic.  The primary means of distributing data in the JDN is with the JTIDS system.  JTIDS uses a TDMA architecture for the transmission and reception of voice and data on Object Request Broker Vertical Facilities (domain specific) Horizontal Facilities (general purpose) Application Objects Common Object Services

<a id="source-pdf-page-40"></a>

## Source PDF page 40

2-21 a finite number of time slots.  When relays are needed to reach NLOS units, the number of time slots is doubled for that particular operation. The TADIL J JRE program proposes a possible solution to the relay problem.  The program is being conducted in three phases.  The Phase 1 demonstration is a simple check to see if TADIL-J messages could be sent through a satellite and received within the required TMD latency.  Phase 1 was successful and demonstrated that TADIL-J messages could be relayed through a satellite in near real time.  Phase 2 of JRE was similar to Phase 1 but the data was passed through a STU-III before it was reformatted into a J3.6 message before being sent via SATCOM.  Phase 2 also proved successful.  Phases 1 and 2 were conducted without using JTIDS terminals or networks. The Phase 3 demonstration connected remote JTIDS networks through the satellite range extension.  The Phase 3 demonstration was also successful and demonstrated there was a potential savings of time slots on the JDN utilizing the JRE.  JRE also provides more reliable connectivity in hostile environments because airborne assets might not be available.

### 2.9.2 ATM Network-Based Integrated Battlespace Simulation With Multiple UAV-AWACS-

Fighter Platforms.  This research provides a realistic input to the amount of throughput that is required to support realistic C4I applications, real time battle management, SAR image processing and analysis, and real time air tasking order (ATO) monitoring through the demonstration of an integrated battlespace simulation on an advanced AWACS prototype network.  The integrated battlespace simulation includes the unmanned aerial vehicle (UAV), C4I platform, and fighter aircraft as core battlefield components.  The simulation uses a scenario not unlike the scenario introduced at the beginning of this chapter.  For its demonstration it uses both ATM LAN emulation and classical IP over ATM multicast configurations.

<a id="source-pdf-page-41"></a>

## Source PDF page 41

2-22 ATM Classical IP-based (CIP) Multicast Solution:  The ATM CIP protocol lacks a broadcast mechanism.  This is resolved by setting up point-to-multipoint permanent virtual circuit (PVC) connections from a broadcast server to all clients.  Since there is no such server in CIP, creation of a virtual broadcasting node (that corresponds to a broadcast service access point) at the switch is necessary. ATM LAN Emulation-based Multicast Solution:  ATM LAN emulation can support multiple independent emulated LANs (ELANs), and the membership in any of the ELANs is independent of the physical location of the end system.  The AWACS mission computer must be a member of all ELANs so that it can selectively broadcast information to any of the AWACS, fighter, or UAV group as different multicast groups. The maximum throughput in the TCP stream test was 108 Mbps for the ATM LAN emulation solution and 118 Mbps for the ATM CIP solution.  As long as the socket buffer sizes were kept above 64 Kilobytes, then both solutions demonstrated normal operation.

### 2.9.3 IP Mobility Management for the Airborne Communications Node (ACN) Platform.

In network-centric architecture where data is transferred via IP packets, it is important to consider issues that occur when moving from one ACN to another.  These include:  average signal strength; subscriber mobility as they move from one footprint of an ACN to another; and other types of mobile subscribers.  A potential problem occurs when, for example, an entire brigade moves relative to the ACN, into the footprint of another ACN.  Mobility management must ensure that routing to and from the edge routers continues to operate correctly.  One solution is Mobile IP, an IETF protocol designed to handle IP mobility [RFC 2002].  However, the range of movements of

<a id="source-pdf-page-42"></a>

## Source PDF page 42

2-23 the edge routers will be restricted to within the ACN network domain.  Therefore, only small-scale mobility management is required and an alternative to the Mobile IP solution can be considered such as a dynamic routing table update solution.  Link state routing performed better than the mobile IP solution in terms of overhead and does not have a single point of failure (as in Mobile IP with its home agent) [JaW00].  Although security overhead was not considered, other overhead issues were which may be beneficial when considering security overhead [JaW00].

### 2.9.4 Surveillance and Control Data Link Network (SCDLN) for Joint STARS.  The Joint

Surveillance and Target Attack Radar System (Joint STARS) communications systems is used to connect an airborne radar platform and many mobile Ground Station Modules (GSM) [SaB94]. The SCDLN uses a secure, highly jam-resistant, dynamically alterable two-way digital data link for the control and distribution of information.  The SCDLN has an additional capability to provide an autonomous message communication network over a wide aerial coverage in a hostile environment.  The major contributor to the anti-jam performance is the Fast Frequency Hopping (FFH) spread spectrum waveform.  Of particular interest in this article is the network architecture. Messages are transmitted in packets and the format will support the transfer of TADIL-J (JTIDS) packet messages. The network is configured so that an airborne platform retransmits incoming data from any GSM back to another or multiple GSMs within the local theatre of operations.  The network operates in half-duplex mode where time is divided into bursts, each burst lasting for 100 milliseconds.  The downlink operation (from airborne platform to GSM) occupies approximately half this time, and two independent uplinks plus a guard time occupy the other half.  The retransmittal of the uplink message becomes an automatic acknowledgement to the sending GSM

<a id="source-pdf-page-43"></a>

## Source PDF page 43

2-24 that the uplink message was correctly received at the AWACS and also allows addressing information to any other GSM in the network (or all of them).  An unlimited number of GSMs can copy both downlink sensor data and relayed messages.  However, a maximum of 15 GSMs can be active at any time and participate in transmitting uplink messages.  Any GSM or AWACS can be the master in the network at a given time.  GSMs are allowed to enter or depart from the network. Once the AWACS commences downlink transmission, an initial polling sequence begins and the network is established by each GSM searching independently for the AWACS downlink signal and once found, begins downlink tracking. 2-10. Summary. This chapter provides a general background and literature review for this research.  A notional JBI architecture was presented and how Link-16 fits into the overall JBI scenario was discussed.  Of particular interest are IA issues within the JBI and the best approach to establishing a robust IA security within the Link-16 arena through the use of IPv6 and IPSec.  Other approaches were considered through the use of CORBA security using objects to control access rights.

<a id="source-pdf-page-44"></a>

## Source PDF page 44

3-1

III.  Methodology

### 3.1 Problem Definition.

As communications technologies have developed, military systems have migrated from stand-alone systems to client-server and fully networked systems.  Therefore, more stringent security requirements have resulted in increased demands on security mechanisms.  The integration of embedded systems such as the F-15E within the proposed Joint Battlespace Infosphere (JBI) network topology exposes this aircraft to new information warfare threats. Exacerbating the problem, information assurance technologies designed for use in real-time embedded systems have not kept pace with emerging threats [Ray01].  Link-16 is a prime candidate to provide a network backbone for the proposed JBI communications.  The Joint Tactical Information Distribution System (JTIDS) terminal, which makes up the communications component of Link-16, provides Message Security (MSEC) through data encryption and Transmission Security (TSEC) through frequency hopping.  However, further security can be implemented through the network layer of the communications architecture.

### 3.1.1 Goals and Hypothesis.  The research goal is to evaluate the performance of an

Information Assurance scheme that incorporates IPv6 and IPSec over a Link-16 datalink network.  This goal is further defined by the following sub-goals: 1. Evaluate the performance metrics of a baseline Link-16 system that incorporates IP packets across the Link-16 network. 2. Determine the impact of incorporating IPSec into the baseline system. 3. Determine the impact of various offered loads to the baseline system.

<a id="source-pdf-page-45"></a>

## Source PDF page 45

3-2

It is hypothesized that IPv6 and/or IPSec can be incorporated into the Link-16 network without degrading performance to a level that it is incapable of supporting real-time data and voice transmission.

### 3.1.2 Approach.  To accomplish the above stated goals, a Link-16 model was used with

the OPNET network simulation software to simulate IP traffic over a Link-16 network.  A distributed software system was used in which an external model communicates with the OPNET software to simulate incoming JBI traffic fed to the Link-16 network.  This system provided the necessary model to compare IP baseline traffic to IPSec to determine effects of increased load on the Link-16 network.

### 3.2 System Boundaries.

The System Under Test (SUT), Figure 3.1, includes the F-15E JBI Connectivity Software Architecture.  This includes the Real-Time OS, the Physical Layer (Link-16), an Adaptation Layer, the Network (IP) Layer, the Transport (TCP) Layer, Real-Time CORBA Middleware, and the JBI applications.  Also included but not pictured in Figure 3.1 is the JTIDS terminal, the communications component used to transmit data and voice transmissions across the Link-16 network.  Not included in the SUT are the other components of the F-15E Avionics System Architecture which include Intelligence, Sensors, and Radar (ISR) collecting components. Within the SUT, the Component Under Test (CUT) includes the JTIDS terminal, the Physical Layer (Link-16), the Adaptation Layer, the Network Layer (IP), and the Transport Layer (TCP).

<a id="source-pdf-page-46"></a>

## Source PDF page 46

3-3

### Figure 3.1:  F-15E JBI Connectivity Software Architecture [Ray01]

### 3.3 System Services.

The network layer decouples upper layers with independence from the data transmission and switching technologies used to connect systems.  In addition, the network layer provides network security including security services at the IP layer of the TCP/IP protocol stack.  The set of security services IPSec can provide includes data origin authentication, data integrity, confidentiality (encryption), and rejection of replayed packets (a form of partial sequence integrity), and limited traffic flow confidentiality.  All of these services are provided at the IP Network (IP)

### JTIDS

Control Transport (TCP) Link-16 Real-Time OS

### SATCOM

### JBI

Client JBI Data Resources Browser Resource Management JBI Applications Collaboration Client

### RT CORBA MIDDLEWARE

Adaptation Layer

<a id="source-pdf-page-47"></a>

## Source PDF page 47

3-4

layer and can be used by any higher layer protocol such as TCP and UDP [Kae99].  The primary services for this study and their possible outcomes include: 1. Data Origin Authentication. a. Success – Packet received from valid origin (packet accepted) b. Failure – Unable to establish that packet came from valid origin (packet dropped) 2. Data Integrity, Data Confidentiality. a. Success – Packet payload has not been tampered with (packet accepted) b. Failure – Unable to establish that packet payload can be trusted (packet dropped) 3. Replay Protection. a. Success – Packets are prevented from being resent from an unauthorized source therefore preventing unauthorized access (packet dropped) b. Failure – Unable to detect that a packet came from an unauthorized source (packet accepted)

### 3.4 Performance Metrics.

The following metrics are used: 1. Throughput – Throughput is defined as Transfer Size/Transfer Time, where Transfer Size is measured in bits and Transfer Time is measured in seconds.  Transfer Size is defined to be number of tactical data bits, thus does not include Reed-Solomon encoding.  The effective tactical data rates of Link-16 vary depending on the data packing structure used.

Navigation: previous [Introduction and background](01-introduction-and-background-pages-012-034.md) | [coverage index](README.md) | next [Model implementation and verification](03-model-implementation-and-verification-pages-048-059.md)
