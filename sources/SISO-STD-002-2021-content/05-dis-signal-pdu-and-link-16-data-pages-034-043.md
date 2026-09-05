# DIS Signal PDU and Link 16 data

Source: `SISO-STD-002-2021.pdf`, PDF pages 34-43.

Navigation: previous [DIS Transmitter PDU](04-dis-transmitter-pdu-pages-029-033.md) | [coverage index](README.md) | next [HLA requirements](06-hla-requirements-pages-044-051.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-34"></a>

## Source PDF page 34

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 34 of 90 This is an approved SISO Standard. Field Size (bits) Transmitter PDU Fields Value Total Link 16 Transmitter PDU size = 896 + 8A + 8 Σ Ki bits, for i = 1 to N

where

A is the length of the Antenna Pattern record in octets, which must be a multiple of 8 N is the number of Variable Transmitter Parameters records Ki is the total length of the Variable Transmitter Parameters record i in octets, including padding required in the Variable Transmitter Parameters record to make its length a multiple of 8 octets

### 4.2.2 Signal PDU

### Table 7 shows the format and values of the Signal PDU for Link 16 simulation.

- `Signal PDUs used in Link 16 simulation shall comply with requirements established in References 4 and`
### 3 and the following requirements:

1. Encoding Scheme. Bits 0-13 of this field shall contain the number of Link 16 words for JTIDS Header/Message, JTIDS LET, and JTIDS VMF message types, or shall contain the value 1 for RTT and JTIDS Voice message ty pes. Bits 14-15 shall contain the value 1 to indicate an Encoding Class of Raw Binary Data IAW Reference 3 [UID 270]. 2. TDL Type. This field shall specify the TDL type as a 16 -bit enumeration field, and shall be set to 100 for Lin k 16 Standardized Format (JTIDS/MIDS/TADIL J) IAW Reference 3 [UID 178]. TDL Type value Link 16 Surrogate for Non -NATO TDL (113) may also be used when simulating a non-NATO tactical data link. 3. Sample Rate. The sample rate shall be set to 0. 4. Data Length. This field shall contain the number of bits in the Data field . The Data field may end on a non-byte boundary, i.e., the length is not required to be a multiple of 8. Padding that follows the Data field to end the PDU on a 32 -bit boundary shall not be included in the Data Length. Padding bits at the end of Link 16 Message Data as specified in Table 9 through

### Table 16 are considered part of the Data field and shall be included in Data  Length. The Data

- `Length field shall be represented by a 16-bit unsigned integer.`
- `5. Samples. This field shall be set to 0.`
- `6. Data. For Link 16 , the Data field shall consist of two parts, a Link 16 Simulation Network`
- `Header portion and a Link 16 Message Data po rtion as shown in  Table 7 and described`
- `below.`
- `A. Link 16 Simulation Network Header. The Link 16 Simulation Network Header portion of`
- `the Signal PDU Data field shall be 160 bits long and shall use the same byte order as the`
- `Signal PDU. These fields are shown in Table 8, and shall be set as follows:`
- `i. NPG Number . This field is a 16 -bit unsigned integer (0 -511) used to segregate`
- `information within a JTIDS/MIDS network. It creates virtual networks of participants.`
- `ii. Net Number. This field is an 8-bit unsigned integer (0-127) used to create virtual sub-`
- `circuits within NPG for stacked nets or between NPGs for multi-net operations.`
- `iii. TSEC CVLL . This field is an 8 -bit unsigned integer that is used for transmission`
- `security and allows for simulated crypto netting. For TSA Levels 0-2 this field shall be`
- `set to 255 (all bits set to one) indicating a no statement/wildcard.`

<a id="source-pdf-page-35"></a>

## Source PDF page 35

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 35 of 90 This is an approved SISO Standard. iv. MSEC CVLL. This field is an 8 -bit unsigned integer that is used for message security in conjunction with the  TSEC CVLL and allows for simulated crypto netting. For TSA Levels 0-2 this field shall be set to 255 (all bits set to one) indicating a no statement/wildcard. v. Message Type Identifier . This field shall specify the format for the type of Link 16 message in the PDU. This field shall be set with an enumeration in accordance with

### Table 6 and Reference 3 [UID 176]. The message type formats are described in

- `detail in Table 9 through Table 16.`
### Table 6: Message Type Identifier

- `Message Type Identifier Enumeration`
- `JTIDS Header/Messages 0`
### RTT A/B 1

RTT Reply 2 JTIDS Voice CVSD 3 JTIDS Voice LPC10 4 JTIDS Voice LPC12 5

### JTIDS LET 6

### VMF 7

vi. SISO-STD-002 Version . This field shall be set IAW Reference 3 [UID 736] and indicates which SISO-STD-002 version was used, i.e., whether byte swapping has or has not been used in the Link 16 Message Data field (0 = SISO -STD-002-2006, legacy byte swapping employed; 1 = SISO -STD-002-2021, new method, bit stream, no byte swapping employed). vii. Link 16 Version . This field shall be set IAW Reference 3 [UID 800] and indicates which version of Reference 7 or Reference 8 is being used. viii. Time Slot ID . This field is a 32 -bit unsigned integer, and shall contain time slot information for time slot and epoch number i n accordance with Reference 7 and Reference 8. Time Slot Number is bits 0 – 16. Time Slot 0 represents time slot A -1, Time Slot 98 303 represents C -32 767. When the Epoch is 112, the last valid Time Slot is 45 151. Bits 17 – 23 are padding. Bits 24 – 31 are the Epoch number. An epoch is 12.8 minutes long, and there are 112.5 epochs in a 24 -hour day. For TSA Level 0 -1, this field shall be set to 4 294 967 295 (all bits set to one  including the padding field) to indicate a no statement/wildcard. ix. Perceived Transmit Time . The Perceived Transmit Time (in NTP timestamp format) shall indicate the time  the Link 16 message was sent , in seconds relative to 0  hours on 1 January 1900 Coordinated Universal Time (UTC ). It includes a 32 -bit unsigned seconds field spanning 136 years and a 32 -bit fraction field resolving 232 picoseconds. See Reference 11 for detailed format. Both fields shall  be set to 4 294

### 967 295 (all bits set to one) to indicate a no statement/wildcard.

B. Link 16 Message Data. The Link 16 Message Data portion of the Data field is a bit stream that shall contain the Link 16 message data corresponding to the message type specified in the  Message Type Identifier field . Link 16 m essage data bit orientation shall be accomplished in accordance with  paragraph 4.1.1 item 20. Table 17 shows an example of bit ordering for the  Link 16 Fixed Format Message , Message Type Identifier 0 (Table 9). Link 16 message types illustrated in  Table 10 through Table 16 have a similar structure.

<a id="source-pdf-page-36"></a>

## Source PDF page 36

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 36 of 90 This is an approved SISO Standard.

### Table 7: Signal PDU for Link 16

- `Field Size`
- `(bits) Signal PDU Fields Value`
### 96 PDU Header

Protocol Version 8-bit enumeration Exercise ID 8-bit unsigned integer PDU Type 8-bit enumeration Protocol Family 8-bit enumeration Timestamp 32-bit unsigned integer Length 16-bit unsigned integer PDU Status  8-bit record Padding 8 bits unused

### 48 Radio

Reference ID Site Number 16-bit unsigned integer Application Number 16-bit unsigned integer Reference Number 16-bit unsigned integer

### 16 Radio

Number  16-bit unsigned integer

### 16 Encoding

Scheme  16-bit record Bits 0-13 shall contain the number of Link 16 words for JTIDS Header/Message, JTIDS LET, and JTIDS VMF message types, or shall contain the value 1 for RTT and JTIDS Voice message types. Bits 14-15 shall contain the value 1 to indicate an Encoding Class of Raw Binary Data.

### 16 TDL Type  16-bit enumeration

### 100 (Link 16 Standardized Format)

### 113 (Link 16 Surrogate for Non-

### NATO TDL)

### 32 Sample Rate  32-bit unsigned

integer Audio sample rate in samples per second, otherwise set to 0.

### 16 Data Length

(K)  16-bit unsigned integer

### 16 Samples  16-bit unsigned

integer 0 Start of Data field

### 160 Link 16 Simulation Network

Header  See Table 8.

<a id="source-pdf-page-37"></a>

## Source PDF page 37

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 37 of 90 This is an approved SISO Standard. Field Size (bits) Signal PDU Fields Value K-160 Link 16 Message Data Bit stream The Link 16 message data, corresponding to the message type specified in the Message Type Identifier field and described in

### Table 9 through Table 16.

- `End of Data field`
- `P Padding Padding to 32-bit`
- `boundary`
- `Total Link 16 Signal PDU size = 256 + K + P bits`

- `where`

- `K is the length of the Data field in bits`
- `P is the number of padding bits, which is ⌈K/32⌉32 - K`
- `⌈x⌉ is the largest integer < x+1`

- `Note:`
- `P = 16 for Message Type Identifiers 1 and 2`
- `P = 16 for Message Type Identifiers 0, 6, and 7 if the number of J Words is even`
- `P = 0 for Message Type Identifiers 0, 6, and 7 if the number of J Words is odd`
- `For Message Type Identifiers 3, 4, and 5, P will vary between 0 and 31 depending on the length of the`
- `JTIDS Free Text Voice Data`

<a id="source-pdf-page-38"></a>

## Source PDF page 38

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 38 of 90 This is an approved SISO Standard.

### Table 8: Link 16 Simulation Network Header

- `Field Size`
- `(bits) Field Name and Data Type Valid Range Value`
- `160`
- `Link 16`
- `Simulation`
- `Network`
- `Header`
- `NPG Number 16-bit unsigned`
- `integer 0-511`
- `Net Number 8-bit unsigned`
- `integer 0-127`
- `TSEC CVLL 8-bit unsigned`
- `integer`
- `0-127 [255 no`
- `statement/`
- `wildcard]`

- `MSEC CVLL 8-bit unsigned`
- `integer`
- `0-127 [255 no`
- `statement/`
- `wildcard]`

- `Message Type`
- `Identifier`
- `8-bit`
- `enumeration  [UID 176]`
- `SISO-STD-002 Version 8-bit`
- `enumeration 0-1 [UID 736]`
- `Link 16 Version 8-bit`
- `enumeration 0-255 [UID 800]`
- `Time Slot`
### ID

Time Slot Number Bits 0-16 0-98 303 [131 071 no statement/ wildcard]

Padding Bits 17-23

### 0 [127 if no

statement/ wildcard]

Epoch Number Bits 24-31 0-112 [255 no statement/ wildcard]

Perceived Transmit Time Integer Part 32-bit unsigned integer 0-4 294 967 295 2

Fraction Part 32-bit unsigned integer 0-4 294 967 295 2

The following tables describe in detail the Signal PDU Message Data for each message format indicated in the Message Type Identifier field in Table 8 above.

### 2 All bits for both fields set to one, i.e., both field values being 4 294 967 295, indicates no statement/

wildcard.

<a id="source-pdf-page-39"></a>

## Source PDF page 39

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 39 of 90 This is an approved SISO Standard.

### Table 9: Message Type Identifier = 0, JTIDS Header/Messages

- `Field Size`
- `(bits) Link 16 Message Fields Bits Description`
### 48 Link 16

Header Word Time Slot Type Bits 0-2 [7, 8] Relay Transmission Indicator Bit 3 [7, 8] Source Track Number of Sender Bits 4-18 [7, 8] Secure Data Unit Serial Number Bits 19-34 [7, 8] Padding Bits 35-47

### 80 Message 1/

Word 1 FWF Message Data

### 70 Bits [7, 8]

Parity 5 Bits [7, 8] Padding 5 Bits

…

### 80 Message 1/

Word W FWF Message Data

### 70 Bits [7, 8]. W is the number of J Words in

a given J Message. Parity 5 Bits [7, 8] Padding 5 Bits

…

### 80 Message M/

Word 1 FWF Message Data

### 70 Bits [7, 8]. M is the number of J Messages

in the Signal PDU. Parity 5 Bits [7, 8] Padding 5 Bits

…

### 80 Message M/

Word W FWF Message Data

### 70 Bits [7, 8]

Parity 5 Bits [7, 8] Padding 5 Bits

### Table 10: Message Type Identifier = 1, RTT A/B

- `Field Size`
- `(bits) Link 16 Message Fields Bits Description`
### 48 RTT A/B RTT A/B Bits 0-34 [7, 8]

Padding Bits 35-47

<a id="source-pdf-page-40"></a>

## Source PDF page 40

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 40 of 90 This is an approved SISO Standard.

### Table 11: Message Type Identifier = 2, RTT Reply

- `Field Size`
- `(bits) Link 16 Message Fields Bits Description`
### 48 RTT Reply RTT Reply Bits 0-34 [7, 8]

Padding Bits 35-47

### Table 12: Message Type Identifier = 3, JTIDS Voice CVSD

- `Field Size`
- `(bits) Link 16 Message Fields Bits Description`
### 48 Link 16

Header Word Time Slot Type Bits 0-2 [7, 8] Relay Transmission Indicator Bit 3 [7, 8] Source Track Number of Sender Bits 4-18 [7, 8] Secure Data Unit Serial Number Bits 19-34 [7, 8] Padding Bits 35-47 225-1860 JTIDS Free Text Voice Data CVSD Encoded Voice Data 225-1860 bits [7, 8]. Size of data area is dependent upon Time Slot Type and Type Modification.

### Table 13: Message Type Identifier = 4, JTIDS Voice LPC10

- `Field Size`
- `(bits) Link 16 Message Fields Bits Description`
### 48 Link 16

Header Word Time Slot Type Bits 0-2 [7, 8] Relay Transmission Indicator Bit 3 [7, 8] Source Track Number of Sender Bits 4-18 [7, 8] Secure Data Unit Serial Number Bits 19-34 [7, 8] Padding Bits 35-47 225-1860 JTIDS Free Text Voice Data LPC10 Encoded Voice Data 225-1860 bits [7, 8]. Size of data area is dependent upon Time Slot Type and Type Modification.

<a id="source-pdf-page-41"></a>

## Source PDF page 41

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 41 of 90 This is an approved SISO Standard.

### Table 14: Message Type Identifier = 5, JTIDS Voice LPC12

- `Field Size`
- `(bits) Link 16 Message Fields Bits Description`
### 48 Link 16

Header Word Time Slot Type Bits 0-2 [7, 8] Relay Transmission Indicator Bit 3 [7, 8] Source Track Number of Sender Bits 4-18 [7, 8] Secure Data Unit Serial Number Bits 19-34 [7, 8] Padding Bits 35-47 225-1860 JTIDS Free Text Voice Data LPC12 Encoded Voice Data 225-1860 bits [7, 8]. Size of data area is dependent upon Time Slot Type and Type Modification.

### Table 15: Message Type Identifier = 6, JTIDS LET

- `Field Size`
- `(bits) Link 16 Message Fields Bits Description`
### 48 LET Header

Word LET ID Symbol Bits 0-3 [12] Relay Transmission Indicator Bit 4 [12] LET Message Packing Type Bits 5-8 [12] Source Track Number of Sender Bits 9-23 [12] Secure Data Unit Serial Number Bits 24-39 [12] Padding Bits 40-47

### 80 Word 1 FWF Message

Data

### 70 Bits [7, 8]

Parity 5 Bits [7, 8] Padding 5 Bits

…

### 80 Word W FWF Message

Data

### 70 Bits [7, 8]. W is the number of J Words in

the Signal PDU. Parity 5 Bits [7, 8] Padding 5 Bits

<a id="source-pdf-page-42"></a>

## Source PDF page 42

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 42 of 90 This is an approved SISO Standard.

### Table 16: Message Type Identifier = 7, VMF

- `Field Size`
- `(bits) Link 16 Message Fields Bits Description`
### 48 Link 16

Header Word Time Slot Type Bits 0-2 [7, 8] Relay Transmission Indicator Bit 3 [7, 8] Source Track Number of Sender Bits 4-18 [7, 8] Secure Data Unit Serial Number Bits 19-34 [7, 8] Padding Bits 35-47 80

Word 1

Word Format 2 Bits [7, 8] VMF Message Data

### 68 Bits

Parity 5 Bits [7, 8] Padding 5 Bits

… 80

Word W

Word Format 2 Bits [7, 8]. W is the number of J Words in the Signal PDU. VMF Message Data

### 68 Bits

Parity 5 Bits [7, 8] Padding 5 bits

### Table 17 below depicts the Signal PDU Data field , showing the Link 16 Simulation Network Header in

- `yellow (for DIS versions that use big endian octet ordering)  followed by a Link 16 Fixed Format Message`
- `(Message Type  Identifier 0). Note that the displayed octet ordering switches after octet 19  due to the`
- `change from octet-oriented data to bit stream data.`
### Table 17: Signal PDU Data field with Link 16 Simulation Network Header and Fixed Format Message

- `Octet 0 Octet 1`
### 15               0

NPG Number

Octet 2

### 7       0

Net Number

Octet 3

### 7       0

### TSEC CVLL

<a id="source-pdf-page-43"></a>

## Source PDF page 43

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 43 of 90 This is an approved SISO Standard. Octet 4

### 7       0

### MSEC CVLL

Octet 5

### 7       0

Message Type Identifier

Octet 6

### 7       0

SISO-STD-002 Version

Octet 7

### 7       0

Link 16 Version

Octet 8 Octet 9 Octet 10 Octet 11

### 31       24 23      17 16                0

Time Slot ID Epoch Number Padding Time Slot Number

Octet 12 Octet 13 Octet 14 Octet 15

### 31                               0

Perceived Transmit Time – Integer Part

Octet 16 Octet 17 Octet 18 Octet 19

### 31                               0

Perceived Transmit Time – Fraction Part

Octet 23 Octet 22 Octet 21 Octet 20

### 31            19 18              4 3 2  0

Secure Data Unit Serial Number (SDUSN) Start Source Track Number of Sender (5 octal values of 3 bits each)

### R

### T

### I

Time Slot Type

Octet 27 Octet 26 Octet 25 Octet 24

### 63  61 60  58 57  55 54    50 48 48 47            35 34  32

Msg Length Indicator J Msg Sub-label J Message Label J Word Format Padding SDUSN End

Octet 31 Octet 30 Octet 29 Octet 28

### 95                               64

First J-Word Continued

Octet 35 Octet 34 Octet 33 Octet 32

### 127    123 122    118 117                     96

Padding Parity First J-Word Continued

Navigation: previous [DIS Transmitter PDU](04-dis-transmitter-pdu-pages-029-033.md) | [coverage index](README.md) | next [HLA requirements](06-hla-requirements-pages-044-051.md)
