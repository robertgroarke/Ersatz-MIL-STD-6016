# Wireshark dissector design and implementation

Source: `DSTO-TN-1257.pdf`, PDF pages 16-24.

Navigation: previous [Link 16 and distribution protocols](01-link-16-and-distribution-protocols-pages-009-015.md) | [coverage index](README.md) | next [Testing and conclusions](03-testing-and-conclusions-pages-025-029.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-16"></a>

## Source PDF page 16

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

8

### 6.4 Development Observations

Through the development of the dissector it became apparent that it is very important to be working with u p to date materials. Although the latest published version of the SISO -J standard document was being used, a draft revision of the standard gave useful examples of the byte swapping operations required to decode the Link 16 messages.

Software development began using an older version of the Wireshark source code. Changes were being made to the DIS dissector upstream 3, and halfway through the development process it was necessary to merge these changes (some of which were overlapping with updates that had been made in the local repository).

### 6.5 Software Patch

In accordance with the Wireshark development guidelines [19], a source code patch against the current version of Wireshark was made. Three patch files were created, one to introduce the Link-16 dissector, and another to add SISO-J header parsing to the existing DIS dissector. A third patch addresses typographic errors found in the existing DIS dissector. R efer to Appendix B for the source code patch.

7. Conclusion and Further Work The Wireshark network protocol analyser has been extended to support analysis of tactical data link messages. This work was done as a summer vacation student project. The extended version of Wireshark  has been evaluated against several sources of J -series messages and demonstrated publically [20]. It has been used to support the development and testing of distributed mission training simulators.

There are several ways in which this work could be furthered. The authors’ suggestions are given below.

Develop a more comprehensive J-series message dissector. The dissector presented in this work only decodes the label and sub-label fields. While this is sufficient for superficial analysis of Link 16 networks, there are many fields within the J-series messages (such as track and coordinate numbers) that would make the dissector more useful for troubleshooting faults.

Support dissection of other distribution protocols. Wireshark could be further extended to dissect the JREAP and MTC protocols.

Develop a Link 11 dissector. Using the approach described in this technical note, one could develop a SISO-STD-005 protocol dissector and complementary M-series message dissector.

### 3  In this context, upstream refers to changes made to the official Wireshark project.

<a id="source-pdf-page-17"></a>

## Source PDF page 17

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

9 Visualisation and statistical utilities In addition to analysing packets, Wireshark includes utilities to visualise and gather statistics on particular protocols. There are potentially use cases where visualisation or presentation of the statistics of the link network would assist with fault diagnosis.

8. References 1. Hura, M., et al. (2000), Interoperability – A Continuing Challenge In Coalition Air Operations, RAND Document No. MR-1235-AF, ISBN 0-8330-2912-6.

2. Friedman, N., (2006), The Naval Institute Guide to W orld Naval Weapon Systems, Naval Institute Press, ISBN 1557502625.

3. Viasat, Inc., (2012), L ink 16 Network Participant Group and Message Card , accessed from <http://www.viasat.com/files/assets/assets/Link16_NPG_Message_Card_100112a.pdf> on 15 April 2013.

4. Elmasry, G., (2012), Tactical Wireless Communications and Networks: Design Concepts and Challenges, Wiley, ISBN 9781119951766.

5. Hill, F., (2003), Systemic Problems With Data Link Simulation,  Fall Simulation Interoperability Workshop 2003, Paper No. 03F-SIW-002.

6. Boardman, B., (2008), Introduction to Tactical Data Links in the ADF , accessed from <http://www.milcis.com.au/milcis2008pdf/Tue/Brett%20Boardman.pdf> on 27 January 2010.

7. STANAG-5602 (2010), Standard Interface for Multiple Platform Link Evaluation (SIMPLE) , Edition 3, NATO Standardization Agency, accessed from < https://assist.dla.mil/> on 30 October 2013.

8. Simulation Interoperability Standards Organization, (2006), SISO-STD-002 Standard for Link 16 Simulations, June 2006.

9. Andersen, D.P. and Thomas, K.D., (2001), Systems Integration Facility: Past, Present, and Future, Space and Naval Warfare Systems Center Biennial Review  2001, accessed from <http://www.spawar.navy.mil/sti/publications/pubs/td/3117/index.html> on 15 April 2013.

10. Teege, G., Eggendorfer, T., Eiseler, V., and Göhner, M., (2007), Militärische mobile Kommunikationsnetze, Universität der Bundeswehr München , Institute of Information Systems Report 2007-02, accessed from <https://dokumente.unibw.de/pub/bscw.cgi/1799259> on 15 April 2013.

11. Sorroche, J. (2006), Tactical Digital Information Link-Technical Advice and Lexicon for Enabling Simulation (TADIL -TALES) II: Link 11/11B, 11th International Command and Control Research and Technology Symposium.

<a id="source-pdf-page-18"></a>

## Source PDF page 18

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

10

12. United State Department of Defense , (1984), MIL-STD-188-203-2 Subsystem Design and Engineering Standards for Tactical Digital Information Link (TADIL) B, 23 March 1984.

13. Simulation Interoperability Standards Organization, (2008), SISO-STD-005 Standard for Link 11/11B Simulation (Draft), 8 September 2008.

14. Orebaugh, A., (2007), Wireshark & Ethereal: N etwork Protocol Analyzer Toolkit, Syngress,

### ISBN 1597490733.

15. Jacobson, V., Leres, C., and McCanne, S., (1994), libpcap. Lawrence Berkeley Laboratory, Berkeley, CA, initial public release June 1994, accessed from <http://www.tcpdump.org/> on

### 18 February 2010.

16. GMANE, (2013), Email archive statistics for the w ireshark-dev mailing list, accessed from <http://gmane.org/output-rate.php?group=gmane.network.wireshark.devel> on 15 April 2013.

17. Thompson, K., (2007), Creating Your Own Custom Wireshark Dissector, Code Project article, accessed from <http://www.codeproject.com/KB/IP/custom_dissector.aspx> on 27 January 2010.

18. Sorroche, J., (2008), SISO J to SIMPLE Translation Advice and Lexicon for Enabling Simulations (SIMPLE TALES), European Simulation Interoperability Workshop 2008, Paper No. 08E-

### SIW-046.

19. Lamping, U., (2013), Wireshark Developer’s Guide for Wireshark 1.11 , accessed from <http://www.wireshark.org/docs/wsdg_html_chunked/> on 16 October 2013.

20. Robertson, W., Ross, P., and Robbie, A.,  (2010), Open Source Analyzer for SISO-J Tactical Data Link Simulation, SimTecT 2010 Conference Proceedings, 31 May— 3 June 2010.

<a id="source-pdf-page-19"></a>

## Source PDF page 19

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

11 Appendix A:  Reference Capture File An exemplar DIS Signal PDU containing J -series messages is described by SISO -STD-002 Annex B. Ethernet, IP and UDP headers were added to this PDU to create a reference capture file compatible with Wireshark. The reference file is shown at Figure B1 and dissected output is shown at Figures B2, B3 and B4.

begin-base64 600 siso_std_002_annex_b_example.pcap 1MOyoQIABAAAAAAAAAAAAP//AAABAAAAAAAAAAAAAACCAAAAggAAAAEAXgEB AQAAAAAAAAgARQAAdAjBAACAEY8MwKgBAeABAQELuAu4AGDavgYBGgQAAAAA AFgAAAAwAAEAAQABQAMAZAAAAAABwAAAAAYA//8AAAAAAAAA//////////8A AACQCQgAANgL8LoAAP/kLGtLKs10tzQ1BQAFkgByBwAAAAE= ====

### Figure B1: Input file (uuencoded)

% tshark -r siso_std_002_annex_b_example.pcap

### 1   0.000000  192.168.1.1 -> 224.1.1.1    Link 16 130 PDUType: Signal, RadioID=1, STN=011,

Link 16 Words: J2.2I J2.2E0 J2.2C1

### Figure B2: Dissector output using tshark

% tshark -r siso_std_002_annex_b_example.pcap –V

Frame 1: 130 bytes on wire (1040 bits), 130 bytes captured (1040 bits) Encapsulation type: Ethernet (1) Arrival Time: Jan  1, 1970 10:00:00.000000000 EST [Time shift for this packet: 0.000000000 seconds] Epoch Time: 0.000000000 seconds [Time delta from previous captured frame: 0.000000000 seconds] [Time delta from previous displayed frame: 0.000000000 seconds] [Time since reference or first frame: 0.000000000 seconds] Frame Number: 1 Frame Length: 130 bytes (1040 bits) Capture Length: 130 bytes (1040 bits) [Frame is marked: False] [Frame is ignored: False] [Protocols in frame: eth:ip:udp:dis:link16:link16:link16] Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: IPv4mcast_01:01:01 (01:00:5e:01:01:01) Destination: IPv4mcast_01:01:01 (01:00:5e:01:01:01) Address: IPv4mcast_01:01:01 (01:00:5e:01:01:01) .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default) .... ...1 .... .... .... .... = IG bit: Group address (multicast/broadcast) Source: 00:00:00_00:00:00 (00:00:00:00:00:00) Address: 00:00:00_00:00:00 (00:00:00:00:00:00) .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default) .... ...0 .... .... .... .... = IG bit: Individual address (unicast) Type: IP (0x0800) Internet Protocol Version 4, Src: 192.168.1.1 (192.168.1.1), Dst: 224.1.1.1 (224.1.1.1) Version: 4 Header Length: 20 bytes Differentiated Services Field: 0x00 (DSCP 0x00: Default; ECN: 0x00: Not- ECT (Not ECN- Capable Transport))

### 0000 00.. = Differentiated Services Codepoint: Default (0x00)

.... ..00 = Explicit Congestion Notification: Not- ECT (Not ECN- Capable Transport) (0x00) Total Length: 116 Identification: 0x08c1 (2241) Flags: 0x00

<a id="source-pdf-page-20"></a>

## Source PDF page 20

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

12 0... .... = Reserved bit: Not set .0.. .... = Don't fragment: Not set ..0. .... = More fragments: Not set Fragment offset: 0 Time to live: 128 Protocol: UDP (17) Header checksum: 0x8f0c [correct] [Good: True] [Bad: False] Source: 192.168.1.1 (192.168.1.1) Destination: 224.1.1.1 (224.1.1.1) User Datagram Protocol, Src Port: remoteware-cl (3000), Dst Port: remoteware-cl (3000) Source Port: remoteware-cl (3000) Destination Port: remoteware-cl (3000) Length: 96 Checksum: 0xdabe [validation disabled] [Good Checksum: False] [Bad Checksum: False] Distributed Interactive Simulation Header Proto version: IEEE 1278.1A-1998 (6) Excercise ID: 1 PDU type: Signal (26) Proto Family: Radio communications (4) Timestamp = 00:00 000 relative PDU Length: 88 Explicit Padding (2 bytes) Signal PDU Entity ID Entity ID Site: 48 Entity ID Application: 1 Entity ID Entity: 1 Radio ID: 1 Encoding Scheme: 0x4003 01.. .... .... .... = Encoding Class: Raw Binary Data (1) ..00 0000 0000 0011 = Encoding Type: 3 TDL Type: Link 16 Standardized Format (JTIDS/MIDS/TADIL J) (100) Sample Rate: 0 Data Length: 448 Number of Samples: 0 Link 16 Network Header NPG Number: PPLI and Status (6) Network Number = 0

### TSEC CVLL: NO STATEMENT (255)

### MSEC CVLL: NO STATEMENT (255)

Message Type: JTIDS Header/Messages (0) Padding = 0 Time Slot ID = 0 Perceived Transmit Time: NO STATEMENT Link 16 Message Data: JTIDS Header/Messages Time Slot Type: 0 Relay Transmission Indicator: 0 Source Track Number: 011 Secure Data Unit Serial Number: 0 Link 16 J2.2I Air PPLI Word Format: Initial Word (0) Label: Precise Participant Location and Identificaton (2) Sublabel: 2 Message Length Indicator: 2 Link 16 J2.2E0 Air PPLI Word Format: Extension Word (2) Link 16 J2.2C1 Air PPLI Word Format: Continuation Word (1) Continuation Word Label: 1

### Figure B3: Dissector output using tshark (with packet details)

<a id="source-pdf-page-21"></a>

## Source PDF page 21

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

13

### Figure B4: Dissector output using Wireshark graphical user interface

<a id="source-pdf-page-22"></a>

## Source PDF page 22

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

14 Appendix B:  Software Patch The modifications made against Wireshark v1.11.0 are shown at Figures A1, A2 and A3.

From 0f9b0c80580700cc4cf06f91b61cfe8b3b31fa6d Mon Sep 17 00:00:00 2001 From: Peter Ross <peter.ross@dsto.defence.gov.au> Date: Wed, 16 Oct 2013 10:00:01 +1100 Subject: [PATCH 1/3] packet-link16: Link 16 message dissector (MIL-STD-6016)

--epan/CMakeLists.txt             |   1 + epan/dissectors/Makefile.common |   1 + epan/dissectors/packet-link16.c | 276 ++++++++++++++++++++++++++++++++++++++++ epan/dissectors/packet-link16.h |  34 +++++

### 4 files changed, 312 insertions(+)

create mode 100644 epan/dissectors/packet-link16.c create mode 100644 epan/dissectors/packet-link16.h

diff --git a/epan/CMakeLists.txt b/epan/CMakeLists.txt index 9baeaa4..c8f54fa 100644 --- a/epan/CMakeLists.txt +++ b/epan/CMakeLists.txt @@ -843,6 +843,7 @@ set(DISSECTOR_SRC dissectors/packet-ldp.c dissectors/packet-ldss.c dissectors/packet-lge_monitor.c + dissectors/packet-link16.c dissectors/packet-linx.c dissectors/packet-lisp-data.c dissectors/packet-lisp.c diff --git a/epan/dissectors/Makefile.common b/epan/dissectors/Makefile.common index ae9831b..bad899e 100644 --- a/epan/dissectors/Makefile.common +++ b/epan/dissectors/Makefile.common

### @@ -772,6 +772,7 @@ DISSECTOR_SRC = \

packet-ldp.c  \ packet-ldss.c  \ packet-lge_monitor.c \ + packet-link16.c  \ packet-linx.c  \ packet-lisp-data.c \ packet-lisp.c  \ diff --git a/epan/dissectors/packet-link16.c b/epan/dissectors/packet-link16.c new file mode 100644 index 0000000..db131db --- /dev/null +++ b/epan/dissectors/packet-link16.c @@ -0,0 +1,276 @@ +/* packet-link16.c + * Routines for Link 16 message dissection (MIL-STD-6016) + * William Robertson <aliask@gmail.com> + * Peter Ross <peter.ross@dsto.defence.gov.au> + * + * $Id$ + * + * This program is free software; you can redistribute it and/or + * modify it under the terms of the GNU General Public License + * as published by the Free Software Foundation; either version 2 + * of the License, or (at your option) any later version. + * + * This program is distributed in the hope that it will be useful, + * but WITHOUT ANY WARRANTY; without even the implied warranty of + * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the + * GNU General Public License for more details. + * + * You should have received a copy of the GNU General Public License + * along with this program; if not, write to the Free Software

<a id="source-pdf-page-23"></a>

## Source PDF page 23

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

15 + * Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA + */ + +#include "config.h" + +#include <glib.h> +#include <epan/packet.h> +#include <epan/value_string.h> +#include <string.h> +#include "packet-link16.h" + +/* Elmasry, G., (2012), Tactical Wireless Communications and Networks: Design Concepts and Challenges, Wiley, ISBN 9781119951766. */ +enum {

### +    WORDFORMAT_INITIAL = 0,

### +    WORDFORMAT_CONTINUATION,

### +    WORDFORMAT_EXTENSION,

+}; + +static const value_string WordFormat_Strings[] = { +    { WORDFORMAT_INITIAL, "Initial Word" }, +    { WORDFORMAT_CONTINUATION, "Continuation Word" }, +    { WORDFORMAT_EXTENSION, "Extension Word" },

### +    { 0, NULL },

+}; + +/* Viasat, Inc., (2012), Link 16 Network Participant Group and Message Card, accessed from <http://www.viasat.com/files/assets/assets/Link16_NPG_Message_Card_100112a.pdf> on 15 April 2013. */ +static const value_string Link16_Label_Strings[] = { +    { 0, "Network Management" }, +    { 1, "Network Management" }, +    { 2, "Precise Participant Location and Identificaton" }, +    { 3, "Surveillance" }, +    { 5, "Anti-submarine Warfare" }, +    { 6, "Intelligence" }, +    { 7, "Information Management" }, +    { 8, "Information Management" }, +    { 9, "Weapons Coordination and Management" }, +    { 10, "Weapons Coordination and Management" }, +    { 11, "Weapons Coordination and Management" }, +    { 12, "Control" }, +    { 13, "Platform and System Status" }, +    { 14, "Electronic Warfare" }, +    { 15, "Threat Warning" }, +    { 16, "Imagery" }, +    { 17, "Weather" }, +    { 28, "National Use" }, +    { 29, "National Use" }, +    { 30, "National Use" }, +    { 31, "Miscellaneous" },

### +    { 0, NULL },

+}; + +/* Viasat, Inc., (2012), Link 16 Network Participant Group and Message Card, accessed from <http://www.viasat.com/files/assets/assets/Link16_NPG_Message_Card_100112a.pdf> on 15 April 2013. */ +#define MKPAIR(a, b) (((b) << 5) | (a)) +static const value_string Link16_Message_Strings[] = { +    { MKPAIR(0, 0), "Initial Entry" }, +    { MKPAIR(0, 1), "Test" }, +    { MKPAIR(0, 2), "Network Time Update" }, +    { MKPAIR(0, 3), "Time Slot Assignment" }, +    { MKPAIR(0, 4), "Radio Relay Control" }, +    { MKPAIR(0, 5), "Repromulgation Relay" }, +    { MKPAIR(0, 6), "Communication Control" }, +    { MKPAIR(0, 7), "Time Slot Reallocation" }, +    { MKPAIR(1, 0), "Connectivity Interrogation" }, +    { MKPAIR(1, 1), "Connectivity Status" }, +    { MKPAIR(1, 2), "Route Establishment" }, +    { MKPAIR(1, 3), "Acknowledgment" },

<a id="source-pdf-page-24"></a>

## Source PDF page 24

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

16 +    { MKPAIR(1, 4), "Communication Status" }, +    { MKPAIR(1, 5), "Net Control Initialization" }, +    { MKPAIR(1, 6), "Needline Participation Group Assignment" }, +    { MKPAIR(2, 0), "Indirect Interface Unit PPLI" }, +    { MKPAIR(2, 2), "Air PPLI" }, +    { MKPAIR(2, 3), "Surface PPLI" }, +    { MKPAIR(2, 4), "Subsurface PPLI" }, +    { MKPAIR(2, 5), "Land Point PPLI" }, +    { MKPAIR(2, 6), "Land Track PPLI" }, +    { MKPAIR(3, 0), "Reference Point" }, +    { MKPAIR(3, 1), "Emergency Point" }, +    { MKPAIR(3, 2), "Air Track" }, +    { MKPAIR(3, 3), "Surface Track" }, +    { MKPAIR(3, 4), "Subsurface Track" }, +    { MKPAIR(3, 5), "Land Point or Track" }, +    { MKPAIR(3, 6), "Space Track" }, +    { MKPAIR(3, 7), "Electronic Warfare Product Information" }, +    { MKPAIR(5, 4), "Acoustic Bearing and Range" }, +    { MKPAIR(6, 0), "Amplification" }, +    { MKPAIR(7, 0), "Track Management" }, +    { MKPAIR(7, 1), "Data Update Request" }, +    { MKPAIR(7, 2), "Correlation" }, +    { MKPAIR(7, 3), "Pointer" }, +    { MKPAIR(7, 4), "Track Identifier" }, +    { MKPAIR(7, 5), "IFF/SIF Management" }, +    { MKPAIR(7, 6), "Filter Management" }, +    { MKPAIR(7, 7), "Association" }, +    { MKPAIR(8, 0), "Unit Designator" }, +    { MKPAIR(8, 1), "Mission Correlator Change" }, +    { MKPAIR(9, 0), "Command" }, +    { MKPAIR(10, 2), "Engagement Status" }, +    { MKPAIR(10, 3), "Handover" }, +    { MKPAIR(10, 5), "Controlling Unit Report" }, +    { MKPAIR(10, 6), "Pairing" }, +    { MKPAIR(11, 0), "From the Weapon" }, +    { MKPAIR(11, 1), "To the Weapon" }, +    { MKPAIR(11, 2), "Weapon Coordination" }, +    { MKPAIR(12, 0), "Mission Assignment" }, +    { MKPAIR(12, 1), "Vector" }, +    { MKPAIR(12, 2), "Precision Aircraft Direction" }, +    { MKPAIR(12, 3), "Flight Path" }, +    { MKPAIR(12, 4), "Controlling Unit Change" }, +    { MKPAIR(12, 5), "Target/Track Correlation" }, +    { MKPAIR(12, 6), "Target Sorting" }, +    { MKPAIR(12, 7), "Target Bearing" }, +    { MKPAIR(13, 0), "Airfield Status" }, +    { MKPAIR(13, 2), "Air Platform and System Status" }, +    { MKPAIR(13, 3), "Surface Platform and System Status" }, +    { MKPAIR(13, 4), "Subsurface Platform and System Status" }, +    { MKPAIR(13, 5), "Land Platform and System Status" }, +    { MKPAIR(14, 0), "Parametric Information" }, +    { MKPAIR(14, 2), "Electronic Warfare Control / Coordination" }, +    { MKPAIR(15, 0), "Threat Warning" }, +    { MKPAIR(16, 0), "Imagery" }, +    { MKPAIR(17, 0), "Weather Over target" }, +    { MKPAIR(28, 0), "U.S. National 1 (Army)" }, +    { MKPAIR(28, 1), "U.S. National 2 (Navy)" }, +    { MKPAIR(28, 2), "U.S. National 3 (Air Force)" }, +    { MKPAIR(28, 3), "U.S. National 4 (Marine Corps)" }, +    { MKPAIR(28, 4), "French National 1" }, +    { MKPAIR(28, 5), "French National 2" }, +    { MKPAIR(28, 6), "U.S. National 5 (NSA)" }, +    { MKPAIR(28, 7), "UK National" }, +    { MKPAIR(31, 0), "Over-the-Air Rekeying Management" }, +    { MKPAIR(31, 1), "Over-the-Air Rekeying" }, +    { MKPAIR(31, 7), "No Statement" },

### +    { 0, NULL },

+}; + +/* Viasat, Inc., (2012), Link 16 Network Participant Group and Message Card, accessed from <http://www.viasat.com/files/assets/assets/Link16_NPG_Message_Card_100112a.pdf> on 15 April

Navigation: previous [Link 16 and distribution protocols](01-link-16-and-distribution-protocols-pages-009-015.md) | [coverage index](README.md) | next [Testing and conclusions](03-testing-and-conclusions-pages-025-029.md)
