# Front matter

Source: `SISO-STD-002-2021.pdf`, PDF pages 1-11.

Navigation: previous none | [coverage index](README.md) | next [Overview](01-overview-pages-012-013.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-1"></a>

## Source PDF page 1

### SISO-STD-002-2021

Standard  for Link 16 Simulation Version 2.0

### 8 November  2021

Prepared by: Tactical Digital Information Link Technical Advice and Lexicon for Enabling Simulation (TADIL TALES) Product Development Group and Product Support Group

<a id="source-pdf-page-2"></a>

## Source PDF page 2

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 2 of 90 This is an approved SISO Standard.

Copyright © 2021 by the Simulation Interoperability Standards Organization, Inc.

### 7901 4th St. N, Suite 300-4043

St. Petersburg, FL 33702, USA

All rights reserved.

Permission is hereby granted for this document to be used for production of both commercial and noncommercial products. Removal of this copyright statement and claiming rights to this document is prohibited. In addition, permission is hereby granted for this document to be distributed in its original or modified format (e.g. as part of a database) provided that no charge is invoked for the provision. Modification only applies to format and does not apply to the content of this document.

SISO Inc. Board of Directors

### 7901 4th St. N, Suite 300-4043

St. Petersburg, FL 33702, USA

<a id="source-pdf-page-3"></a>

## Source PDF page 3

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 3 of 90 This is an approved SISO Standard. Revision History Version Section Date (MM/DD/YYYY) Description

### 1.0 All 7/10/2006 SISO-STD-002-2006

Initial standard

### 2.0 All 11/8/2021 SISO-STD-002-2021

Updated to latest SISO standard template Incorporated several Problem/Change Requests including: - Updated for newer versions of DIS and HLA standards - Updated for newer versions of MIL- STDs and STANAGs - Use bit stream versus byte-swapping in Signal PDU Data field - Allow use of Network Synchronization ID field in Transmitter PDU to model separate Link 16 networks - Clarified the Data Length field in Signal

### PDU

- Clarified that multiple J-messages are allowed in a single Signal PDU - Clarified that Transmitter PDU bracketing is optional - Changed from BOM to FOM module and updated HLA sections - Numerous editorial updates and improvements

<a id="source-pdf-page-4"></a>

## Source PDF page 4

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 4 of 90 This is an approved SISO Standard. Participants At the time this product was submitted to the Standards Activity Committee (SAC) for approval, the Tactical Digital Information Link Technical Advice and Lexicon for Enabling Simulation (TADIL TALES) Product Development Group an d Product Support Group (PDG PSG)  had the following membership and was assigned the following SAC Technical Area Director: Product Development Group Joe Sorroche (Chair) Steve Weiss (Vice-Chair) Pat Merlet (Secretary) ▬ ▬ ▬ Thom McLean (SAC Technical Area Director until February 2020) John Hughes (SAC Technical Area Director after February 2020) ▬ ▬ ▬ Ron Arlund Curtis Blais Larry Boyce Lance Call Aaron Carlson Mary Christopher Peterjohn Gentles Lance Marrou Laurent Mounet Robert Murray Ivar Oswalt Andrew Reed David Ronnfeldt Peter Ross Graham Shanks David Taylor Jonathan Ulrich Rene Verhage Brian Waltersdorf The Product Development Group would like to especially acknowledge those individuals that significantly contributed to the preparation of this product as follows: PDG Drafting  Group Steve Weiss (Editor)

Ron Arlund John Hughes Lance Marrou Pat Merlet Robert Murray Graham Shanks Joe Sorroche Rene Verhage

<a id="source-pdf-page-5"></a>

## Source PDF page 5

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 5 of 90 This is an approved SISO Standard. The following individuals comprised the ballot group for this product: Ballot Group Ron Arlund Curtis Blais Larry Boyce Donald Brutzman Lance Call Bruce Clay Anthony Cramp Peterjohn Gentles Jean-Louis Gougeat John Hughes Patrice Le Leydour James McRae Pat Merlet Laurent Mounet Robert Murray Ivar Oswalt James Quarmyne David Ronnfeldt Peter Ross Graham Shanks Joe Sorroche Jonathan Ulrich Tom van den Berg Rene Verhage Ted Wallace Brian Waltersdorf Steve Weiss

When the Standards Activity Committee approved this product on 20 October 2021, it had the following membership: Standards Activity Committee Michael O'Connor (Chair) Curtis Blais (Vice Chair) Katherine Ruben (Secretary)

Grant Bailey Peggy Gravitz John Hughes Patrice Le Leydour William Oates Simon Skinner Clyde Smithson Keith Snively Fuzzy Wells Michael Woodman

Executive Committee Robert Lutz (Chair) Kenneth Konwin (Vice Chair) Mark McCall (Secretary)

Jeff Abbott Damon Curry Paul Gustavson Kurt Lessmann Lana McGlynn Chris Metevier Katherine Morse Michael O'Connor Robert Siegfried

<a id="source-pdf-page-6"></a>

## Source PDF page 6

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 6 of 90 This is an approved SISO Standard. Introduction Link 16 is a n Integrated  Communications, Navigatio n and Identification ( ICNI) system intended to exchange surveillance and Command and Control (C2) information among various C2 platforms and weapons platforms to enable a  variety of missions that are conducted by  military services. It provides multiple access, high capacity, jam resistant, digital data and secure voice ICNI information to a variety of platforms. Link 16 is the primary tactical data link standard for North Atlantic Treaty Organization (NATO). NATO Standard ization Agreement (STANAG) 5516 [ 8] and MIL -STD-6016 [ 7] describe the Link 16 message formats (Link 16 messages are also known as TADIL -J messages) and Link 16 network instructions. Link 16 uses the Joint Tactical Information Distributi on System (JTIDS) as its  communications component. The terms Link 16 and JTIDS are frequently used interchangeably. The Multi functional Information Distribution System (MIDS) is the NATO equivalent term for JTIDS .

<a id="source-pdf-page-7"></a>

## Source PDF page 7

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 7 of 90 This is an approved SISO Standard.

### Table of Contents

### 1 Overview ........................................................................................................................................ 12

### 1.1 Scope .......................................................................................................................................... 12

### 1.2 Purpose ....................................................................................................................................... 12

### 1.3 Objectives ................................................................................................................................... 12

### 1.4 Intended Audience ...................................................................................................................... 12

### 2 References ..................................................................................................................................... 13

### 3 Definitions, Acronyms, and Abbreviations ..................................................................................... 14

### 3.1 Definitions ................................................................................................................................... 14

### 3.2 Acronyms and Abbreviations ...................................................................................................... 18

### 4 Requirements ................................................................................................................................. 20

### 4.1 JTIDS Operating Characteristics ................................................................................................ 20

### 4.1.1 General Requirements ........................................................................................................... 20

### 4.1.2 TSA Levels of Fidelity ............................................................................................................ 23

### 4.1.2.1 TSA Level 0, Low Fidelity ................................................................................................. 24

### 4.1.2.2 TSA Level 1, Low Fidelity ................................................................................................. 24

### 4.1.2.3 TSA Level 2, Medium Fidelity ........................................................................................... 24

### 4.1.2.4 TSA Level 3, Medium Fidelity ........................................................................................... 25

### 4.1.2.5 TSA Level 4, High Fidelity ................................................................................................ 25

### 4.1.2.6 Fidelity Level Summary .................................................................................................... 25

### 4.1.3 Communication Between JUs with Different Fidelity Levels .................................................. 26

### 4.1.4 Time Synchronization ............................................................................................................ 27

### 4.1.4.1 No Time Synchronization .................................................................................................. 27

### 4.1.4.2 Low-Fidelity Time Synchronization ................................................................................... 27

### 4.1.4.3 Medium-Fidelity Time Synchronization ............................................................................. 27

### 4.1.4.4 General Time Synchronization Provisions ........................................................................ 28

### 4.2 Link 16 Implementation Using DIS .............................................................................................. 29

### 4.2.1 Transmitter PDU .................................................................................................................... 29

### 4.2.2 Signal PDU ............................................................................................................................ 34

### 4.3 Link 16 Implementation Using HLA ............................................................................................. 44

### 4.3.1 The Link 16 FOM Module ...................................................................................................... 44

### 4.3.1.1 Assumptions ..................................................................................................................... 44

### 4.3.1.2 Naming Convention .......................................................................................................... 45

### 4.3.1.3 Representations ................................................................................................................ 45

### 4.3.2 Levels of Fidelity .................................................................................................................... 45

### 4.3.3 Time Synchronization ............................................................................................................ 45

<a id="source-pdf-page-8"></a>

## Source PDF page 8

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 8 of 90 This is an approved SISO Standard.

### 4.3.4 Protocol Implementation Details ............................................................................................ 45

### 4.3.4.1 Object Class Data ............................................................................................................. 45

### 4.3.4.2 Interaction Class Data ...................................................................................................... 46

### 4.3.5 FOM Module Definition .......................................................................................................... 47

### 4.3.6 Adding the Link 16 FOM Module to a Parent FOM ............................................................... 47

### 4.3.7 Adding the Link 16 FOM Module to the RPR FOM ............................................................... 47

### 4.3.7.1 Updating the RPR FOM Communications Module ........................................................... 47

### 4.3.7.2 Updating the RPR FOM Enumerations Module................................................................ 48

### 4.3.7.3 Updating the Link 16 FOM Module ................................................................................... 48

Annex A Link 16 FOM Module (Informative) ........................................................................................... 52

### A.1 Object Model Identification Table ................................................................................................ 52

### A.2 Object Class Structure Table ...................................................................................................... 54

### A.3 Interaction Class Structure Table ................................................................................................ 55

### A.4 Attribute Table ............................................................................................................................. 56

### A.5 Parameter Table ......................................................................................................................... 56

### A.6 Basic Data Representation Table ............................................................................................... 58

### A.7 Simple Datatype Table ................................................................................................................ 58

### A.8 Enumerated Datatype Table ....................................................................................................... 59

### A.9 Array Datatype Table .................................................................................................................. 61

### A.10 Fixed Record Datatype Table ..................................................................................................... 61

### A.11 Notes Table ................................................................................................................................. 65

### A.12 Object Class Definition Table ...................................................................................................... 65

### A.13 Interaction Class Definition Table ............................................................................................... 65

### A.14 Attribute Definition Table ............................................................................................................. 66

### A.15 Parameter Definition Table ......................................................................................................... 66

Annex B DIS to HLA Translations (Informative) ...................................................................................... 69

### B.1 RPR FOM RadioTransmitter Object versus DIS Transmitter PDU ............................................. 69

### B.2 RPR FOM RadioSignal Based Interactions versus DIS Signal PDU .......................................... 69

### B.2.1 Link 16 Common Data ........................................................................................................... 69

### B.2.2 JTIDS Header/Messages ....................................................................................................... 72

### B.2.3 RTT A/B ................................................................................................................................. 76

### B.2.4 RTT Reply .............................................................................................................................. 77

### B.2.5 JTIDS Voice CVSD ................................................................................................................ 78

### B.2.6 JTIDS Voice LPC10 ............................................................................................................... 80

### B.2.7 JTIDS Voice LPC12 ............................................................................................................... 81

### B.2.8 JTIDS LET ............................................................................................................................. 82

### B.2.9 VMF ........................................................................................................................................ 84

<a id="source-pdf-page-9"></a>

## Source PDF page 9

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 9 of 90 This is an approved SISO Standard. Annex C SISO-STD-002 Changes (Informative) ..................................................................................... 89

### C.1 Introduction ................................................................................................................................. 89

### C.2 DIS Changes ............................................................................................................................... 89

### C.3 HLA Changes .............................................................................................................................. 89

<a id="source-pdf-page-10"></a>

## Source PDF page 10

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 10 of 90 This is an approved SISO Standard. List of Tables

### Table 1: JTIDS Communication Modes ...................................................................................................... 22

### Table 2: Link 16 Simulation TSA Levels ..................................................................................................... 23

### Table 3: Transmitter Message Modulation Parameters - Valid Field Values for Different TSA Levels ...... 25

### Table 4: Signal Message Link 16 Simulation Network Header - Valid Field Values for Different TSA Levels

- `.................................................................................................................................................................... 26`
### Table 5: Transmitter PDU for Link 16 ......................................................................................................... 31

### Table 6: Message Type Identifier ................................................................................................................ 35

### Table 7: Signal PDU for Link 16 .................................................................................................................. 36

### Table 8: Link 16 Simulation Network Header .............................................................................................. 38

### Table 9: Message Type Identifier = 0, JTIDS Header/Messages ............................................................... 39

### Table 10: Message Type Identifier = 1, RTT A/B ........................................................................................ 39

### Table 11: Message Type Identifier = 2, RTT Reply .................................................................................... 40

### Table 12: Message Type Identifier = 3, JTIDS Voice CVSD ...................................................................... 40

### Table 13: Message Type Identifier = 4, JTIDS Voice LPC10 ..................................................................... 40

### Table 14: Message Type Identifier = 5, JTIDS Voice LPC12 ..................................................................... 41

### Table 15: Message Type Identifier = 6, JTIDS LET .................................................................................... 41

### Table 16: Message Type Identifier = 7, VMF .............................................................................................. 42

### Table 17: Signal PDU Data field with Link 16 Simulation Network Header and Fixed Format Message  ... 42

### Table 18: JTIDSTransmitterStruct Mapping to DIS Modulation Parameters  .............................................. 46

### Table 19: RPR FOM Link 16 FOM Module Interactions Class Structure Table ......................................... 50

### Table 20: SpreadSpectrumEnum16 with Link 16 FOM Module Modifications  ........................................... 50

### Table 21: SpreadSpectrumVariantStruct with Link 16 FOM Module Modifications  .................................... 51

### Table A-1: Object Model Identification ........................................................................................................ 52

### Table A-2: RadioTransmitter Object ........................................................................................................... 55

### Table A-3: Interaction Class Structure Table .............................................................................................. 56

### Table A-4: Parameter Table ........................................................................................................................ 56

### Table A-5: Basic Data Representation Table .............................................................................................. 58

### Table A-6: Simple Datatype Table .............................................................................................................. 58

### Table A-7: Enumerated Datatype Table ..................................................................................................... 60

### Table A-8: Array Datatype Table ................................................................................................................ 61

### Table A-9: Fixed Record Datatype Table .................................................................................................... 62

### Table A-10: Notes Table ............................................................................................................................. 65

### Table A-11: Interaction Class Definition Table............................................................................................ 65

### Table A-12: Parameter Definition Table ...................................................................................................... 66

### Table B-1: Link 16 Message Type Identifier to HLA Interaction Class Mapping ........................................ 69

<a id="source-pdf-page-11"></a>

## Source PDF page 11

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 11 of 90 This is an approved SISO Standard.

### Table B-2: Link 16 Common Signal PDU to HLA Interaction Mapping ....................................................... 70

### Table B-3: Link 16 Simulation Network Header Data ................................................................................. 71

### Table B-4: JTIDS Header/Messages to JTIDSMessageRadioSignal Mapping  .......................................... 73

### Table B-5: Link 16 Message Data for JTIDS Header/Messages ................................................................ 74

### Table B-6: RTT A/B to RTTABRadioSignal Mapping ................................................................................. 77

### Table B-7: Link 16 Message Data for RTT A/B........................................................................................... 77

### Table B-8: RTT Reply to RTTReplyRadioSignal Mapping .......................................................................... 78

### Table B-9: Link 16 Message Data for RTT Reply ....................................................................................... 78

### Table B-10: JTIDS Voice CVSD to JTIDSVoiceCVSDRadioSignal Mapping ............................................. 79

### Table B-11: Link 16 Message Data for JTIDS Voice .................................................................................. 80

### Table B-12: JTIDS Voice LPC10 to JTIDSVoiceLPC10RadioSignal Mapping ........................................... 81

### Table B-13: JTIDS Voice LPC12 to JTIDSVoiceLPC12RadioSignal Mapping  ........................................... 82

### Table B-14: JTIDS LET to JTIDSLETRadioSignal Mapping ....................................................................... 83

### Table B-15: Link 16 Message Data for JTIDS LET ..................................................................................... 84

### Table B-16: VMF to VMFRadioSignal Mapping .......................................................................................... 85

### Table B-17: Link 16 Message Data for VMF ............................................................................................... 86

Navigation: previous none | [coverage index](README.md) | next [Overview](01-overview-pages-012-013.md)
