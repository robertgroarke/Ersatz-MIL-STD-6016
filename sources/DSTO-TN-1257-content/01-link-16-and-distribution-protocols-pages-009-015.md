# Link 16 and distribution protocols

Source: `DSTO-TN-1257.pdf`, PDF pages 9-15.

Navigation: previous [Front matter and executive summary](00-front-matter-and-executive-summary-pages-001-008.md) | [coverage index](README.md) | next [Wireshark dissector design and implementation](02-wireshark-dissector-design-and-implementation-pages-016-024.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-9"></a>

## Source PDF page 9

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

1 1. Introduction Tactical Data Links (TDLs) enable the military to exchange tactical information in a precise, efficient and timely manner. They complement, and in many instances substitute, traditional voice-based communication bearers such as VHF radio. Major military platforms operated by the Australian Defence Force are either equipped, or are being equipped with TDL systems. Concurrent with real -world adoption, training simulators are being fitted with simulated tactical data links.

This techn ical note describes the development  of a Link 16 message dissector for the Wireshark network protocol analyser. Wireshark is a freely-available open-source protocol analyser that is an industry standard tool for network protocol troubleshooting. The dissector supports analysis of J-series messages adhering to the Simulation Interoperability Standards Organization’s Standard for Link 16 Simulations. While existing Link 16 test tools are available, they are more suited to non -simulated data link operations, w here quality assurance and safety are paramount. The cost and thus availability of these dedicated test tools make them less desirable for use with simulators.

Development of the dissector was completed as a summer vacation student project over a 10 week period during 2009–2010, using sources from the open literature on Link 16. No export controlled technical data was used in the production of this technical note.

2. Link 16 Link 16 is a United States and North Atlantic Treaty Organization (NATO) tactical data link standard that defines the message format, methods of radio transmission , and network management procedures1. It is the current data link system operated by the United States, NATO members and allied countries. Development commenced in 1975 [ 1], with systems fielded by the United States Air Force and Navy in the early 1990s [2].

Link 16 may also be referred to as the Joint Tactical Information Distribution System (JTIDS), which is the name assigned to the original project and first- generation terminal, or more simply Tactical Digital Information Link J (TADIL-J).

### 2.1 J-series Message Format

Tactical data link messages are the units of information exchanged between the participants of a tactical data link network. Link 16 supports the exchange of fixed formatted messages, more commonly referred to as J-series messages, to convey information. There are over 70 messages defined [3].

### 1 Link 16 is defined by several standards including MIL-STD-6016 Tactical Data Link 16 Message Standard

and STANAG -5516 Tactical Data Exchange –  Link 16 ; STANAG 4175 Technical Characteristics of the Multifunctional Information Distribution System ; and US CJCSM 6120.01 Joint Multi-TADIL Operating Procedures and NATO-ADATP-16 Standard Operating Procedures for NATO Link 16. These standards are not published in the open literature and were not used in the production of this technical note.

<a id="source-pdf-page-10"></a>

## Source PDF page 10

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

2

Each J-series message comprises an initial word, followed by extension word(s) and optional continuation words. Each word is 75 bits long, containing 70 bits of data and 5 bits parity. An example of the initial word layout is shown in Figure 1.

Messages are identified by a label and sub-label. For example, label 2, sub-label 2, identified in shorthand as J2.2, conveys the Precise Participant Location and Identification (PPLI) of an air platform. This message is published on the network to advise other interested participants of an air platform’s location and identifying information. United States Department of Defense MIL-STD-6016 and NATO Standardisation Agreement (STANAG) 5516  define how the information is stored and retrieved from the 75-bit words, and rules governing the issuance and receipt of those words.

### MSB                        LSB

### 24            12  10 9  7 6    2 1 0

### MESSAGE

### LENGTH

### INDICATOR

### SUB-LABEL LABEL WORD

### FORMAT

### 49                        25

### 74    70                    50

### PARITY

### Figure 1: Example J -series Initial Word  (reproduced from [4], §5.2.1). The dashed area concerns

message specific information.

### 2.2 Distribution System

When operating within li ne of sight of one another , the participants of a Link 16 network exchange messages using  frequency hopping Time Division Multiple Access (TDMA) transceiver terminals operating in the UHF Lx radar band (960 - 1215 MHz). The distribution system provides resistance against electronic countermeasures whilst maintaining security and integrity of the message content.  Network throughput is 28800, 57600 or 115200 bps depending on the required level of electronic countermeasure protection.

Where there is a need to exchange messages beyond line of sight, as is the case with distributed mission training exercises, protocols exist that allow for the data link messages to be exchanged over satellite or fixed-line networks. These protocols are sometimes referred to as wrappers, as their primary task is to encapsulate J-series messages in a format suitable for transmission over alternate media  [5]. A list of frequently used beyond line of sight distribution protocols is given below:

• United States Department of Defense MIL-STD-3011 Joint Range Extension Application Protocol (JREAP). JREAP is the military standard protocol for exchanging messages beyond line of sight over satellite, serial line or Internet Protocol [6].

<a id="source-pdf-page-11"></a>

## Source PDF page 11

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

3

• NATO STANAG 5602 Standard Interface for Multiple Platform Link Evaluation (SIMPLE) [7]. SIMPLE was developed by the NATO Tactical Data Link Interoperability Test Syndicate to support interoperability testing between development laboratories. The protocol may be operated over serial line or Internet Protocol.

• Simulation Interoperability Standards Organization SISO -STD-002 S tandard f or Link  16 Simulations [8]. Also known as SISO-J, this protocol was developed by the simulation community to address the needs of training and research simulations. SISO-J is an extension of the Distributed Interactive Simulation (DIS) application protocol, and High Level Architecture (HLA) Real-time Platform Reference Federation Object Model (RPR- FOM). It encapsulates J-series messages inside the DIS Transmitter and Signal Protocol Data Units (PDUs) or RPR-FOM equivalents, allowing line of sight, signal propagation and interference to be modelled within the simulation. The standard defines optional rules for modelling the characteristics of the TDMA network.

• Global Command and Control System (GCCS) Multi TADIL Capability (MTC).  The MTC protocol was developed initially for exchanging J-series messages with GCCS software [9], but has been since adopted by other systems. Whereas the other distribution protocols listed here employ detailed encapsulation headers and issuance and receipt rules, the MTC protocol uses minimalist headers. It may be operated over serial line or Internet Protocol, and is referred to informally as Serial-J or Socket-J.

Of the above protocols, only SIMPLE and SISO-J have been published in the open literature. JREAP protocol data structures are described in [10], but the issuance and receipt rules are omitted.

3. Link 11/ 11B Link 16 complements an earlier generation TDL standard known as Link 11. Development of Link 11 commence d in 1954, with sea trials undertaken in the 1960s. The airborn e and maritime variant of Link 11 is also known as TADIL-A, and the variant intended for point to point links is known as Link 11B, or TADIL-B [2]. Link 11 is governed by several standards that define the message format, method of signal modulation, and procedures for network management2. Although Link 11 is not the focus of our work, appreciating the similarities between it and Link 16 provides for meaningful discussion later in this technical note.

### 2 Link 11 is defined by several standards including MIL-STD-188-203-1 Interoperability and Performance

Requirements for TADIL -A and MIL -STD-188-203-2 Subsystem Design and Engineering Standards for TADIL-B; MIL-STD-6011 Tactical Data Link 11/11B Message Standard and STANAG -5511 Tactical Data Exchange – Link 11/Link 11B; and NATO-ADATP-11 Standard Operating Procedures for NATO Link 11/Link 11B.  With the exception of MIL -STD-188-203-1 and MIL -STD-188-203-2, these standards are not published in the open literature.

<a id="source-pdf-page-12"></a>

## Source PDF page 12

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

4

### 3.1 M-series Message Format

Link 11 M-series messages are transmitted as two 30 bit frames, with each frame containing 24 bits of data, and 6 bits for forward error correction. Messages are identified by a 4-bit label. United States Department of Defense MIL-STD-6011 and NATO STANAG 5511 describe how information is stored and retrieved from the 30 bit frames. An example of the message layout is shown in Figure 2.

### MSB                            LSB

### 29     24 23                       0

### FORWARD

### ERROR CORRECTION

### LABEL

### 29     24 23                       0

### FORWARD

### ERROR CORRECTION

### Figure 2: Example M-series message (reproduced from [11], §2.1). The dashed area concerns message

specific information.

### 3.2 Distribution System

Link 11 messages are modulated  using Quadrature Phased -Shift Keying (QPSK) and exchanged over half-duplex HF or UHF radio. The modulator/demodulator is known as the Data Terminal Set (DTS). Security is achieved by encrypting the digital message stream prior to modulation. The system supports two data rates: 2250 bps (fast) and 1364 bps (slow) [2].

Link 11B messages are transmitted over point to point radio links, such as microwave or satellite.

Protocols to distribute Link 11 messages beyond radio coverage include:

• The plain old telephone system. To achieve point-to-point connectivity, the radio transceiver is replaced with a standard telephone line.

• TADIL-B over Internet Protocol. The TADIL -B transmission frame format [ 12] can be exchanged over serial line or Internet Protocol.

• NATO STANAG 5602 Standard Interface for Multiple Platform Link Evaluation (SIMPLE) . Refer to the previous description of SIMPLE in section 2.2.

• SISO-STD-005 Standard for Link 11 /11B Simulation [13]. Currently in draft form,  this standard encapsulates M-series messages within the DIS Transmitter and Signal PDUs (or RPR-FOM equivalents). The performance characteristics of the network may be optionally modelled.

<a id="source-pdf-page-13"></a>

## Source PDF page 13

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

5 4. Wireshark Wireshark, previously named Ethereal,  is an open -source network protocol analyser. It provides a comprehensive filtering and query system, utilities for performing statistical analysis, and dissector modules to decode and inspect protocol content. A graphical and textmode (known as tshark) user interface is provided [14]. Wireshark uses the libpcap library [15] (or WinPcap libraries for  Microsoft Windows) to capture Ethernet frames directly from a computer’s network interface adaptor.

Dissectors are modules that exist within Wireshark to decode specific network protocols and present the information in a human-readable format. A diverse range of dissectors is included with Wireshark, such as Ethernet, Internet Protocol, Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) and over 1000 other protocols. Wireshark includes routines for dissecting DIS PDUs. However at the time of the student project only the most common of PDU types were supported: Entity State, Fire and Detonation PDUs. Since then other developers have expanded the DIS dissector to  support many more PDUs  from the Distributed Emission Regeneration, Radio Communication and Simulation Management families.

Wireshark was chosen as a foundation for this student project for the following reasons:

• Industry standard . Wireshark is an industry standard tool for network protocol troubleshooting. Any effort spent improving Wireshark is likely to benefit its other users.

• Familiarity. For distributed simulation exercises, staff at DSTO already use Wireshark to diagnose faults and capture packets in simulation exercises. Where practical the libpcap file format is used to archive exercise recordings.

• Heritage. Wireshark has been under development since 1998. Infrastructure to decode byte sequences, display information, and manage configuration files has been previously built and thoroughly tested.

• Portability. Wireshark is written in the C89 programming language and runs on Linux, Mac OS X, BSD, Solaris and Microsoft Windows operating systems.

• Active open -source project.  The software is distribu ted using  the GNU General Public License, and is supported by an active developer and user community. The project features a high volume email reflector (averaging 11, 11 and 7 messages per day over 2010,

### 2011 and 2012 respectively [16]), library of reference packet capture files, regression testing

system and issue tracker.

<a id="source-pdf-page-14"></a>

## Source PDF page 14

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

6 5. Requirements Requirements for the student project were defined as follows.

1. Modify the existing DIS dissector to decode Signal PDUs and SISO -J headers and display content of fields, performing enumeration lookups where necessary. 2. Support dissection of J-series messages ; display the label and sub -label of each message. 3. Ensure the Link 16 routines are sufficiently modular, allowing them to be reused by other protocol dissectors ( such as a hypothetical JREAP or MTC dissector). An experimental SIMPLE protocol dissector , developed some years earlier by DSTO , provides a use case for this requirement. 4. Support filtering of messages such that search queries can be answered. For example ‘display all packets containing the J2.2 message.’ 5. Document all material used in the development of the dissector to allow auditing of the source code. 6. Reuse or adapt existing Wireshark routines where possible. 7. Produce a working software patch that can be applied to a known version of Wireshark.

6. Development The modifications to Wireshark were developed over several weeks  in 2010. They were revised in 2013 in order to be compatible with Wireshark v1.11.0 (the current version at time of publication).

### 6.1 Environment

An appropriate build environment was needed to begin programming of the dissector. As the primary development computer was a Linux system (Ubuntu Linux 9.10 and 12.10), this was achieved by running the included configure shell script and the required dependencies via the Linux package manager.

### 6.2 Implementation

It was necessary to become familiar with the design and internal workings of Wireshark and its existing DIS dissector. There were plenty of development resources available on the Internet; a particularly useful resource was an article in The Code Project on writing a new dissector [17]. A review of the existing Wireshark DIS dissector  found it to use a custom system for parsing DIS PDUs. Given a description of a DIS PDU or Record, the parsing system would automatically extract the appropriate bytes from the PDU, perform endian conversion, and register fields with Wireshark’s filtering and query system. This approach was found to be unique compared to other existing protocol dissectors.

The task of extending Wireshark to support Link 16 was broken into three main activities:

<a id="source-pdf-page-15"></a>

## Source PDF page 15

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

7 1. Write a new Link 16 dissector module that decodes J-series message words. 2. Modify the existing DIS dissector to process SISO-J Signal PDUs. 3. Modify an experimental SIMPLE dissector to use the new Link 16 dissector.

Logic to detect SISO-J headers was added to the Signal PDU processor of the DIS dissector. When detected, the relevant headers are decoded, and the Link 16 J -series messages are handed off individually to the Link 16 dissector. By separating the Link 16 J-series message dissector from the DIS dissector, the requirement for a modular system was fulfilled.

Distribution protocols were each found to format J-series message words differently for transmission. The SIMPLE protocol stores each word as a 80-bit little endian word, whereas the SISO-J Signal PDU stores them as a series of three interleaved big endian 32-bit words [18]. JREAP and MTC may use different formatting again. It was therefore necessary to make the Link 16 dissect or agnostic to the underlying transmission format. This was achieved by normalising the format accepted by the Link 16 dissector module, and making the SISO-J and SIMPLE dissectors responsible for converting between  the transmission and normalised format (80-bit little endian was chosen as the normalised format).

Because only the initial word of a J-series message contains the label and sublabel identifiers, and subsequent extension and continuation messages rely on that information, it was also necessary to store these values within the context of the dissector. This enabled subsequent words within the message to be identified correctly.

### 6.3 Testing

The modified Wireshark has been evaluated against the example J2.2 Air PPLI message defined in the SISO-J standard (refer to Appendix A), and data generated by third-party SISO- J capable equipment. Significant observations from the test phase are given below.

Using the built in Wireshark tool fuzz-test.sh, more than 2000 iterations of fuzzed capture files were fed into the dissectors to test for its ability to handle corrupted packets. T he test was completed with no errors encountered. This was done to gain confidence that the dissector would not crash when subjected to invalid data. As a troubleshooting tool, it must be able to cope with malformed DIS PDUs and J-series messages.

The software was tested on Ubuntu Linux 12.10 (on both i386 and 64 bit PowerPC hardware), Debian 6.06 (SPARC64) and Windows Server 2003 R2 (i386) operating systems – providing coverage of 32 bit, 64 bit, little endian and big endian environments. Two faults were found during this testing; these have since been corrected.

1. Initially Link 16 words were not being decoded correctly. T his was due to misinterpretation of the method SISO-J used to store J-series messages.

2. Output from the text-mode tshark program did not match the output from the Wireshark graphical user interface  – the data in the information column was not being updated. Moving the code that handled this to outside the if(tree) { ... } section allowed tshark to function properly.

Navigation: previous [Front matter and executive summary](00-front-matter-and-executive-summary-pages-001-008.md) | [coverage index](README.md) | next [Wireshark dissector design and implementation](02-wireshark-dissector-design-and-implementation-pages-016-024.md)
