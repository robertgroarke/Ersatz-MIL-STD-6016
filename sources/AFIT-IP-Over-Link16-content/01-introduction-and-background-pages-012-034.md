# Introduction and background

Source: `AFIT-IP-Over-Link16.pdf`, PDF pages 12-34.

Navigation: previous [Front matter](00-front-matter-pages-001-011.md) | [coverage index](README.md) | next [Research methodology](02-research-methodology-pages-035-047.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-12"></a>

## Source PDF page 12

vi

### C.1 Raw Throughput (Baseline) ............................................................................................... C-1

### C.2 Raw Throughput (Baseline and AH) ................................................................................. C-1

### C.3 Raw Throughput (Basel ine, AH, and ESP) ....................................................................... C-2

<a id="source-pdf-page-13"></a>

## Source PDF page 13

vii List of Tables Table Page

### 2.1 Link-16 Data Ra te Comparison.........................................................................................2-18

### 3.1 Offered Load Parame ters - Methodology ........................................................................... 3-7

### 4.1 Verification Worklo ad Parameters...................................................................................... 4-5

### 4.2 Implementation Workload Parameters................................................................................ 4-9

### 4.3 End-to-End (ETE) Delay Allocation of Variation (ANOVA) .........................................4-17

### 4.4 Effective Thr oughput ANOVA.........................................................................................4-18

### A.1 ETE De lay Data.................................................................................................................. A-1

### A.2 ETE De lay Mean ................................................................................................................ A-1

### A.3 ETE Delay Standard Deviations ........................................................................................ A-1

### A.4 ETE Delay Computa tion of Effects ................................................................................... A-2

### A.5 ETE Delay Inter action Effects ........................................................................................... A-2

### A.6 ETE Delay Allocatio n of Variation.................................................................................... A-2

### A.7 ETE Delay Confidence Interval  (CI) for Overhead Effects .............................................. A-2

### A.8 ETE Delay CI for Offe red Load Effects ............................................................................ A-2

### B.1 Effective Throughput Data................................................................................................. B-1

### B.2 Effective Throughput Mean ............................................................................................... B-1

### B.3 Effective Throughput St andard Deviations ....................................................................... B-1

### B.4 Effective Throughput Comp utation of Effects .................................................................. B-2

<a id="source-pdf-page-14"></a>

## Source PDF page 14

viii

### B.5 Effective Throughput In teraction Effects........................................................................... B-2

### B.6 Effective Throughput Allo cation of Variation................................................................... B-2

### B.7 Effective Throughput Co nfidence Interval (CI) for Overhead Effects ............................. B-2

### B.8 Effective Throughput CI fo r Offered Load Effects ........................................................... B-2

### D.1 Sample Size for Determining Mean (Baseline) ................................................................. D-1

### D.2 Sample Size for Determining Mean (AH) ......................................................................... D-1

### D.3 Sample Size for Determining Me an (Baseline, AH, and ESP) ......................................... D-2

<a id="source-pdf-page-15"></a>

## Source PDF page 15

ix

### AFIT/GCE/ENG/03-04

Abstract The purpose of Link-16 is to exchange real -time tactical data among units of the United States and allied forces.  Primary Link-16 functions include exchange of friendly unit position and status data, the dissemination of tactical surveillance track data, and the control/management of air, surface, and subsurface engagements.  Because Link-16 will play an integral part in the networkcentric Joint Battlespace Infosphere (JBI), the performance of Internet Protocol version six (IPv6) and IP Security (IPSec) over Link-16 needs to be determined.  IP packets also afford additional security measures within the JBI. Using OPNET  modeling software to simulate a Link-16 network, the investigation of this research revealed that the overhead from IPv6 and IPSec does not significantly affect end-to-end delay and effective throughput of the Link-16 network.  As long as the encryption and authentication protocols are preprocessed, these protocols add minimal amounts of latency overhead to the Link-16 network.  However, as the offered load is extended beyond the 90 % level, the overhead from the IPSec extensions begins to have more of a negative effect on the End-to-End delay and throughput.  Therefore, as the offered load increases beyond the 90 % level, it begins to have a significant impact on the performance of the Link-16 network.

<a id="source-pdf-page-16"></a>

## Source PDF page 16

1-1

### INTERNET PROTOCOL (IP) OVER LINK-16

I.  Introduction One of the key challenges of the 21 st century military force is Information Superiority.  This challenge is being addressed in one respect through the Joint Battlespace Infosphere (JBI) [SAB99].  The JBI uses a network-centric concept, versus platform-centric concept, so that all JBI data can be easily transmitted from one platform to another.  The JBI can accommodate both legacy and new communications systems.  The integration of new and legacy systems provides essential improvements in the distribution of information through various platforms at all levels of the command structure from Joint Forces Air Component Command (JFACC) to the pilot in the cockpit [Ray01].  Link-16, a tactical data link used among U.S. and NATO forces, has the potential to bridge new and legacy systems through the use of the Internet Protocol (IP).

### 1.1 Background

The proposed JBI includes elem ents from deployed U.S., allied, and coalition forces that require the ability to communicate with one another [SAB99].  There is a relationship between the timeliness of information and the tempo of operations across any war-fighting theatre of operations.  For instance, at the high end of the performance spectrum are cooperative sensing and engagement of high-speed targets that require high data rate and low latency information transport capabilities.  At the intermediate level, there are various command and control activities that can tolerate information delays on the order of seconds.  These operations are typically supported by

<a id="source-pdf-page-17"></a>

## Source PDF page 17

1-2 data links on various platforms such as fighter and support aircraft, fixed and mobile ground units, and naval vessels. The JBI structure can be view ed as an integrated network of communication devices of multi-mode transport capabilities to include civilian and military networks, satellite communications, multiple types of data links, radios, and other commercial information services combined to create a distributed computing environment.  Emerging technologies enable multiple stand-alone networks to be integrated into a dynamic network-of-networks communications system.  In the current environment, voice, video, and data networks operate independently in order to meet required timelines for information exchange.  Each network operates with protocols that are separate and distinct from the protocols employed in Transmission Control Protocol/Internet Protocol (TCP/IP) based networks, such as the Secret Internet Protocol Router Network (SIPRNET), or the Unclassified Internet Protocol Router Network (NIPRNET).  Until recently, the reason for separate networks was due to lack of quality of service across IP networking technology.  However, technology now exists to solve this problem. Most current platforms use a tactical data li nk of one form or another.  The Air Force is migrating its legacy data link systems to the J-Series family of tactical data links using Link-16 as the foundation.  Link-16 will replace the Interim JTIDS Message System, TADIL-A, TADIL-B, and TADIL-C systems [USAF01].  The standard way of transporting data across most networks is through the use of IP packets.  Therefore, it is essential that Link-16 be able to transport IP packets across its network as well.  IP Next Generation (IPv6) is the latest version of the Internet protocol, designed to be the successor of IP version 4 (IPv4).  Although one of the major reasons for creating IPv6 was to increase the IP address size from 32 bits to 128 bits, and thereby relieve the rapidly

<a id="source-pdf-page-18"></a>

## Source PDF page 18

1-3 shrinking available addresses, another key feature of IPv6 is its authentication and privacy capabilities.  Extensions to the IP to support authentication, data integrity, and data confidentiality are specified in IPv6 [RFC 2460].  These extensions include the IP Security (IPSec) protocol which provides various security services at the IP layer.  The two traffic security protocols contained in IPSec are the Authentication Header (AH) protocol and the Encapsulating Security Payload (ESP) protocol.  IPSec is designed to provide interoperable, high quality, cryptographically-based security for IPv4 and IPv6 [RFC2401]. Although Link-16 has its own security m easures (Message Security and Transmission Security), if additional security can be added without significantly adding to transmission overhead, then it is advantageous to provide security at an additional layer such as the IP layer. This research focuses on the latency effects from transmitting IP and IPSec over a Link-16 data link.

### 1.2 Goals

The overall goal of this research is to evaluate the performance of a scheme that incorporates IP and  IPSec into a Link-16 datalink network.  In assessing this goal, this research will first consider, as a baseline, the effect of IP overhead when “packaging” IP messages into JTIDS packets.  Once the baseline is established, then the effects from the IPSec overhead will be considered.  The IPSec protocols to be evaluated include the AH and ESP protocols.  Their effect on network latency will be analyzed to determine if their additional overhead will adversely affect the Link-16 data link network.  In order to attain the above stated goal, the following objectives will need to be met:

<a id="source-pdf-page-19"></a>

## Source PDF page 19

1-4 • Develop or obtain a Link-16 network simulation model • Verify the simulation model • Determine what impact IP messages passed over a Link-16 network have on overall latency

### 1.3 Document Overview

This chapter provides an introduction and some  background to the network-centric concept of battlefield communications and focuses in on the data-link aspect, particularly, the Link-16 network aspect.   It concludes with the goals of this research.  Chapter II provides background information in the areas of  the JBI, Information Assurance, IP, IPSec, and various communications platforms.  Chapter III contains the methodology this research used to approach the problem.  Chapter IV describes the verification and simulation process of the OPNET Link-

### 16 model, as well as the accumulation of data and analysis of the results acquired from the

OPNET Link-16 model.  Chapter V describes research conclusions and areas that should be considered for future study.

<a id="source-pdf-page-20"></a>

## Source PDF page 20

2-1 II.  Literature Review

### 2.1  Introduction

This chapter examines the increasing need for Information Assurance (IA) within older generation aircraft communications systems and the unique challenges these systems face when communicating with newer communications systems.  Currently fielded IA methods for embedded information systems were designed on systems that were limited due to their proprietary interfaces to other systems.  In contrast, network-centric warfare depends on a reliable flow of information among systems, which are designed around open architectures and commonly used standards and products.  Additionally, older generation aircraft were not built to support the high data throughput rate common in many applications used today, nor can they support the graphical interfaces commonly used in many applications.  Consider, for example the F-15E, a 70’s era aircraft, which still plays a vital role in the U.S. Air Force.  It is designed to support data transfer rates in the kilobit per second range not the megabit or even gigabit per second range that modern systems currently use.  Modern systems are capable of high data transfer rates.  These systems, such as the F-22 Raptor Stealth Fighter, also have IA integrated into them by design [Loc03].  It is a challenge to integrate IA into older generation aircraft such as the F-15E, not only because of limited bandwidth problems, but also because of the inherent difficulty in integrating new technology into older systems.

### 2.2 Scenario

Figure 2.1 shows a scenario in the proposed Joint Battlespace Infosphere (JBI) [SAB99]. The JBI is made up of a complex, heterogeneous system of systems with globally distributed fixed

<a id="source-pdf-page-21"></a>

## Source PDF page 21

2-2 and deployed assets consisting of various servers, databases, gateways, and proxies. Communications networks include WANs, LANs, terrestrial and space-based assets and also include such resources such as SIPRNET and NIPRNET.  Figure 2.1 is split into two parts:  fixed assets represent Continental United States (CONUS) resources and deployed assets represent outside (OCONUS) resources.  In this scenario, an F-15E flight operating within the Joint Battlespace Infosphere (JBI) is enroute to its pre-planned target [Ray01]1.

### Figure 2.1:  A Notional Deployed Joint Battlespace Infosphere

### 1 Since the JBI is still a concept and not complete in design, assumptions have been made regarding ground-based JBI components.

Reconnaissance Global Information Grid Fixed Assets Deployed Assets

### MILSAT

### COMSAT

Wing/Squadron Home Base Wing Air Ops. Center

### C4ISR C2

JBI Fusion Engine JBI Server Network Infrastructure - Military & Commercial

### JFACC

<a id="source-pdf-page-22"></a>

## Source PDF page 22

2-3 Simultaneously, in the same theatre of opera tions, an Unmanned Air Vehicle (UAV) detects a Surface-to-Air Missile (SAM) and transmits this data to the JBI mission servers via Satellite Communication (SATCOM).  Since SAMs are a high priority target, Air Command decides to reroute the F-15E flight to take out the SAM.  Using JBI, Air Command directs the AWACS and F-15E to change the mission to intercept the SAM target.  The F-15E on-board JBI client receives an Air Tasking Order (ATO) change alert.  The AWACS operator and lead Weapons System Officer (WSO) review the ATO alert for additional info.  The F-15E acknowledges the new ATO and diverts to the new target. In this notional scenario there are many simultaneous communications occurring between fighter aircraft, AWACS, UAVs, satellites, JBI servers, and the Air Operations Centers (AOC), using various data formats, each encompassing their own security measures.  It is problematic to insert data security into data communications due to the additional overhead that comes along with the added security.  This is especially true for older generation aircraft with limited communications bandwidth.  Yet, IA measures are needed to protect communication systems, data integrity, data confidentiality, data availability, and provide proper authentication and authorization measures. Figure 2.2 shows an established F-15E—JBI communications link.  Prior to the F-15E departure, the Link-16 network is configured to allow communication among the F-15Es, the AWACS controller aircraft and the ground-based AOC JBI Server Gateway.  Once the connectivity between the on-board JBI client and ground-based JBI server is established, communication data is transferred via flight “Cups”, or objects whose implementation consists of a

<a id="source-pdf-page-23"></a>

## Source PDF page 23

2-4

CORBA object that provides services such as write and read to other objects.  A CORBA object is defined as an identifiable, encapsulated entity that provides one or more services that can be requested by a client [TaV02].  Access to the Cup’s services is typically restricted to objects that possess proper authorization rights. Figure 2.3 shows the JBI Server Gateway that  includes the JBI Server application and it’s related databases and associated collaboration applications.  The above mentioned “Cup” or mission fuselet resides on the JBI Server.  In this scenario, CORBA serves as the distributed object JBI Server Gateway

### AWACS

Link-16 Nets JBI Fusion Engine 306th Wing Air Operations Center JBI Server Link-16 Dist. Object Interface JBI Client Link-16 Dist. Object Interface JBI Server Link-16 Dist. Object Interface Fuselet Cup Subscription / Publish

### Figure 2.2:  Linking the F-15E Aircraft into the JBI

### F-15E

<a id="source-pdf-page-24"></a>

## Source PDF page 24

2-5

middleware to facilitate communication between the different OSI layers in accordance with the security policy.  An adaptation layer supports communication between the Internet Protocol (IP) and the Link-16 protocol.  The F-15E on-board Advanced Display Core Processor (ADCP) serves as host to the JBI applications and required databases.  Link-16 and SATCOM components communicate through the Communication, Navigation, and Identification (CNI) suite of the F-15E on-board communications system to provide wireless JBI connectivity.  The CNI is connected to the ADCP via the MIL-SPEC 1553 Avionics Bus.

### Figure 2.3:  AOC Notional Hardware Architecture and JBI

Server Gatewa y Software Architecture Mission Planning Work Stations w.

### DTM

JBI Server / Gateway

### JTIDS

Terminal Mission Systems

JBI Server Printer

### SATCOM

Link Encryptor Firewall Router Browser Imagery

### ATO

JBI Data Resources

### JBI

Server JBI Applications Network (IP) CORBA Middleware Transport (TCP) Link-16 Operating System Ethernet Adaptation Layer Shogun Mission Fuselet Shogun Mission Cup Collaboration Server

<a id="source-pdf-page-25"></a>

## Source PDF page 25

2-6

### 2.4 Information Assurance (IA) Capabilities.

IA functionality can be implem ented in various components of the JBI—F-15E architecture. Countermeasures are layered to provide “defense in depth”, where each layer provides it’s own layer of security.  Combined system security, then, is reinforced by each layer.  For instance, security could be deployed in the ground-based host systems, in the JBI network nodes, or onboard the F-15E Strike Eagle.  In focusing on the F-15E on-board notional architecture, there are several areas where IA functionality can be implemented, such as: • Real-Time Operating System:  Trusted Security Kernel, Access Control • Data Link Layer:  Link-16/JTIDS Security and SATCOM Security • IP Layer:  IPSec/IPv6.0 • Middleware Layer:  CORBASec • Application/Transport Layer:  SSL and/or Database Security This research focuses on security implemented at the IP layer.  It is assumed that IPv6 will be used.  IP Security (IPSec) is integrated into IPv6 and supports data origin, data integrity, data confidentiality, replay protection and automated management of cryptographic keys [Kae99].

### 2.4.1 Security Threats and Countermeasures.   When considering implementation of IA into

a communications system it is important to define threats and mechanisms available to counter those threats.  There are four types of security threats to consider along with their typical countermeasures [TaV02]:

<a id="source-pdf-page-26"></a>

## Source PDF page 26

2-7 • Interception:  This occurs when an unauthorized party gains access to data, such as when a third party eavesdrops on a conversation by two other parties or when data is illegally copied.  A principle countermeasure to interception is data encryption. • Interruption:  Interruption occurs when data or services become unavailable, such as when data is corrupted or lost.  A typical example is a Denial of Service (DOS) attack when a server can no longer be accessed because of overload.  DOS is difficult to defend against, but authorization countermeasures put in place through a firewall are a typical method of protection • Modification:  Modification is the unauthorized changing of data or tampering with a service so it no longer conforms to the original specification.  An example is tampering with database files or modifying the behavior of a program.  Principle counter measures include authentication, authorization, and/or auditing. Authentication and authorization are put in place to prevent modification in the first place whereas auditing is used to identify a perpetrator after-the-fact. • Fabrication:  Adding information to gain unauthorized access, such as replay attacks or adding an entry into a password file are examples of fabrication.  Similar to protecting against the modification threat, authentication, authorization and auditing provide a defense in this situation.

Some typical threats that might be enc ountered in the notional architecture include:

• Spoofing (modification):  For example, communications from SATCOM to F-15Es can be modified, such that an attacker attempts to introduce data packets that appear to come from a trusted source.  Countermeasures:  TRANSEC and COMSEC of Airborne

<a id="source-pdf-page-27"></a>

## Source PDF page 27

2-8 Links and/or additional data encryption and packet source authentication mechanisms at higher communication layers. • Introduction of malicious software into an F-15E from the JBI can occur when an adversary uses a JBI host to launch an attack against an F-15E.  A typical situation is where a hacker finds a backdoor into the JBI network (through Battlefield networks, Defense Information System Networks, or the Internet) and creates a JBI object with embedded malicious code payload.  The corrupted JBI object is uploaded to the F-15E aircraft via the Data Transfer Module (DTM), Link-16, or through SATCOM.  The malicious code can then execute its payload on-board the F-15E.  Countermeasures: Intrusion detection on-board the aircraft can mitigate the threat. • Eavesdropping and/or Surveillance:  This involves the unauthorized interception of information.  Successful attacks against airborne links requires the ability to thwart TSEC and MSEC countermeasures at the data link level or the ability to monitor the unencrypted messages at the source or destination nodes.  Countermeasures:  Data encryption through TSEC and MSEC. A comprehensive IA approach can be implemented by using a layered approach to security. These layers need to:  (1) protect the system from attacks through access control, firewalls, and cryptography; (2) detect successful attacks (intrusions) through intrusion detection; (3) react to attacks by terminating the attack, confining and deleting malicious software, restoring the system to full integrity, notifying the pilot, WSO, and audit log.

<a id="source-pdf-page-28"></a>

## Source PDF page 28

2-9

### 2.5 Multi-Platform Common  Data Link (MP-CDL)

MP-CDL provides a network-centric data link between airborne and surface Intelligence, Surveillance, and Reconnaissance (ISR) assets.    The MP-CDL program (contract awarded in November 2002) is planned to meet the needs for a number of airborne and surface platforms to simultaneously distribute sensor data products to multiple supporting airborne and ground stations.  MP-CDL is designed to meet the needs of various network clients (airborne and surface) to interact with a centrally located airborne terminal as well as other clients. All terminals will support gateway connectivity to other links external to the MP-CDL network.  These links may be either in-theater line-of-site (LOS) or beyond LOS such as SATCOM links.  The initial application of MP-CDL will be in support of Army surface units command and control access to surveillance products from the Multi-Platform Radar Technology Insertion Program (MP-RTIP) platform.  In addition to network operations, the MP-CDL terminals support the capability for point-to-point interoperability with CDL surface and/or airborne terminals. The requirement for a central airborne terminal is to provide a single point-to-point data link operating simultaneously with an independent multi-user network.  The terminal’s point-topoint data link must be interoperable with exiting CDL surface communication equipment and Airborne Information Transmission (ABIT) relay terminals at established standard data rates up to 274 Megabits per second.

The multi-user network will connect up to 32 users on a COTS based network architecture. Range will be dependent on size, weight, and power requirements and mission geometries to be determined later, but is estimated to be approximately equal to the maximum LOS from an

<a id="source-pdf-page-29"></a>

## Source PDF page 29

2-10 altitude of 40,000 feet, or approximately 275-350 feet, depending on the height of the receiving antenna near the earth’s surface.  The MP-CDL system will operate in the Ku band and will support future capability to operate in one or more alternative RF bands (i.e., X, Ku, Ka) to allow multiple simultaneous links [PIX02]. The MP-CDL vision grew out of the MP-RTIP, which was originally a Joint STARS radar upgrade.  MP-RTIP was restructured in 2000 to develop a common modular scaleable radar in three sizes: • Large:  Wide Area Surveillance (WAS) • Medium:  NATO • Small:  Global Hawk

### 2.5.1 MP-CDL Main Goals.   The goals of MP-CDL are to provide:

• Transparent communication between deployed platforms [Cha02] o IP based, per Global Grid Standards o Low-latency, wideband path o Common carrier for all types of traffic in IP packets o Same HW/SW for air, ground, and sea • A “LAN hub in the sky” • Tradeoff Data rate vs. Antijam

<a id="source-pdf-page-30"></a>

## Source PDF page 30

2-11 • Common and COTS/GOTS Hardware

### 2.5.2 MP-CDL Data Rates.  Throughput rates vary depending on the current

configuration of one-to-one communication devices such as AWACS to UAV, AWACS to Common Ground Stations (CGS), UAV to CGSs.  However, within the multi-user network, data transmission rate capabilities are based on these minimum required rates. The multi-user network data transmission rate from the central airborne terminal (host) to the CGSs (clients) is: • 45 Megabits per second unjammed to CGS • 2.2 Megabits per second in jam resistant mode • Similar rates from ISR hub for air-air net The multi-user network data transmission rate capability from the CGSs (clients) to the central airborne terminal (host) is: • CGSs:  low send data, limited power and antenna size.  Will dynamically share a low-rate up-link. • A ground station with more bandwidth and a bigger dish could reach aircraft with 40-60 Megabits per second. • ISR platforms should reach 20-40-60 Megabits per second air-air depending on geography and dish size.

<a id="source-pdf-page-31"></a>

## Source PDF page 31

2-12

### 2.5.3 Standardization Issues.  The DoD tactical message standard is TADIL-J (Link-16).

Non-tactical standard is IP.  MP-CDL terminals will transmit and receive IP packets, and will not be involved in the content, format, or protocol of the data (unless the packet is addressed to that particular terminal).  MP-CDL message sizes vary in length from 100 bits to 100 Mbits, and message types and sensor data from the Air Force, Army and Navy, such as TADIL-J, Moving Target Indicator (MTI), Synthetic Aperture Radar (SAR), Signals Intelligence (SIGINT), Air Tasking Order (ATO), and Global Grid (GG).

### 2.6  IPSec/IPv6

IPSec, short for IP Security, is a set of protocols developed by the Internet Engineering Task Force (IETF) to support secure exchange of packets at the IP layer [Kae99].  IPSec has been deployed widely to implement Virtual Private Networks (VPN).   IPSec is supported in IP version 4 (IPv4) and is mandatory for the next generation of IP, version 6 (IPv6).  IPSec supports two encryption modes:  Transport and Tunnel. Transport mode encrypts only the data portion (payload) of each packet, but leaves the header untouched. The more secure Tunnel mode encrypts both the header and the payload. A compliant IPSec implementation must support the required set of Security Association (SA) bundle types as outline in Section 4.5 of the Internet Engineering Task Force (IETF) Request For Comments (RFC) 2401 [RFC 2401].  The bundle types include four different combinations of the Authentication Header (AH) and Encapsulating Security Payload (ESP) protocols.  On the receiving side, a compliant device decrypts each packet.  The compliant protocol is designed to support these security areas:

<a id="source-pdf-page-32"></a>

## Source PDF page 32

2-13 • Data Origin Authentication • Data Integrity • Data Confidentiality • Replay Protection The Security Association (SA) concept is fundamental to IPSec.  An SA is a relationship between two or more entities that describes how the entities will use security services to communicate effectively.  The SA includes:  an encryption algorithm; an authentication algorithm; and a shared session key. For a compliant IPSec implementation to work, sending and receiving devices must share a public key.  This is accomplished through a protocol known as Internet Security Association and Key Management Protocol/Oakley (ISAKMP/Oakley), which allows the receiver to obtain a public key and authenticate the sender using digital certificates [Kae99]. IPSec uses the AH protocol and ESP protocols to provide proof of data origin on received packets, data integrity, anti-replay protection, data confidentiality and limited traffic flow confidentiality.  These two protocols can be combined and used to protect an entire IP datagram or just the upper-layer protocols of the IP payload. Besides support for mobility, security is a key requirement for the successor to today's Internet Protocol version.   Except for application-level protocols like SSL or SSH, all IP traffic between two nodes can be transmitted without changing any applications. All applications on a

<a id="source-pdf-page-33"></a>

## Source PDF page 33

2-14 machine that benefit from encryption and authentication policies can be set on a per-host (or even per-network) basis, not per application/service.

### 2.6.1  Authentication Header Protocol.   Use of the AH protocol will increase the IP

protocol processing costs and will also increase the communications latency.  The increased latency is due to the additional authentication data contained in the AH.  The fields of the AH as shown in Figure 2-4 are explained as follows: • Next Header – 8 bit field which identifies the type of the next payload after the AH • Payload Length – 8 bit field which specifies the length of the AH in 32 bit words • Reserved – 16 bit field which must be set to zero • Security Parameters Index (SPI) – A 32 bit value that in combination with the destination address identifies the SA for the datagram • Sequence Number Field – Unsigned 32 bit field contains a monotonically increasing counter value for defense against replay attacks • Authentication Data – Variable length field that contains the Integrity Check Value (ICV) for the payload

Next Header – 8 bits Payload Length – 8 bits Reserved – 16 bits Security Parameters Index (SPI) – 32 bits Sequence Number Field – 32 bits Authentication Data – Variable Size

### Figure 2.4:  Authentication Header (AH) Format

<a id="source-pdf-page-34"></a>

## Source PDF page 34

2-15

### 2.6.2  Encapsulating Security Payload Protocol.  Use of the ESP protocol will also

increase processing costs and communication costs in a similar manner as the AH protocol.  The ESP header holds encryption, replay, and authentication information for its IP datagram.  If authentication is selected as part of the SA, encryption is performed first followed by authentication.  The encryption algorithm used is selected by the SA.  ESP is designed to use symmetric key encryption algorithms.  The fields of the ESP header as shown in Figure 2-5 are: • Security Parameters Index (SPI) – A 32 bit value that in combination with the destination address identifies the Security Association for the datagram • Sequence Number Field – Unsigned 32 bit field contains a monotonically increasing counter value for defense against replay attacks • Payload Data – Variable length field containing data described by the Next header field.  If the encryption algorithm requires an initialization Vector then that would be contained here • Padding (0-255 bytes) – May be required to satisfy requirements for encryption algorithms • Pad Length – Indicates the number of bytes used in the Padding field • Next Header – Identifies the type of data contained in the Payload field • Authentication Data – Variable length field that contains the Integrity Check Value (ICV) for the packet

Navigation: previous [Front matter](00-front-matter-pages-001-011.md) | [coverage index](README.md) | next [Research methodology](02-research-methodology-pages-035-047.md)
