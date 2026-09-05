# Annex A - FOM module

Source: `SISO-STD-002-2021.pdf`, PDF pages 52-68.

Navigation: previous [HLA requirements](06-hla-requirements-pages-044-051.md) | [coverage index](README.md) | next [Annex B - DIS-HLA translations](08-annex-b-dis-hla-translations-pages-069-088.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-52"></a>

## Source PDF page 52

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 52 of 90 This is an approved SISO Standard. Annex A Link 16 FOM Module (Informative)

### A.1 Object Model Identification Table

General introduction: The purpose of this table is to document certain key identifying information within the object model description. For detailed information on the table format, see Reference 6.

### Table A-1: Object Model Identification

- `Category Information`
- `Name SISO-STD-002 - Link 16 Simulation FOM module`
- `Type FOM`
- `Version 2.0`
- `Modification Date 2021-11-08`
- `Security Classification Unclassified`
- `Purpose Defines the Link 16 model in an HLA federation`
- `Application Domain C4ISR & C2 platform simulations`
- `Description This module provides the full definition of the SISO-STD-002 Standard for Link 16 Simulation for implementation using`
### HLA.

Note that this Link 16 FOM module relies upon a parent FOM to provide suitable class definitions for radio transmitters and radio signals. Typically, it cannot be directly used within a federation. This module can be considered as a template for creating a concrete FOM module for inclusion in the parent FOM. See SISO-STD-002-2021 section 4.3 for more information. Note also that for HLA Evolved a pre-built RPR FOM 2.0 with Link 16 FOM module can be downloaded from the SISO website.

### POC

POC Type Primary author POC Name TADIL TALES Product Development Group and Product Support Group POC Organization SISO - Simulation Interoperability Standards Organization POC Telephone +1 (407) 882-1348

<a id="source-pdf-page-53"></a>

## Source PDF page 53

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 53 of 90 This is an approved SISO Standard. Category Information POC Email siso-help@sisostds.org References Type Text Document Identification SISO-STD-002-2021 Standard for Link 16 Simulation Version 2.0

### 8 November 2021

Type Text Document Identification SISO-STD-001-2015 Standard for Guidance, Rationale, and Interoperability Modalities for the Real -time Platform Reference Federation Object Model Version 2.0

### 10 August 2015

Type Text Document Identification SISO-STD-001.1-2015 Standard for Real-time Platform Reference Federation Object Model Version 2.0

### 10 August 2015

Type Text Document Identification SISO-REF-010-2020 Reference for Enumerations for Simulation Interoperability Version 29

### 19 May 2021

<a id="source-pdf-page-54"></a>

## Source PDF page 54

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 54 of 90 This is an approved SISO Standard. Category Information Other Copyright © 2021 by the Simulation Interoperability Standards Organization, Inc.

### 7901 4th St. N, Suite 300-4043

St. Petersburg, FL 33702, USA

All rights reserved.

Schema and API: SISO hereby grants a general, royalty-free license to copy, distribute, display, and make derivative works from this material, for all purposes, provided that any use of the material contains the following attribution: “Reprinted with permission from SISO Inc.” Should a reader require additional information, contact the SISO Inc. Board of Directors.

Documentation: SISO hereby grants a general, royalty-free license to copy, distribute, display, and make derivative works from this material, for noncommercial purposes, provided that any use of the material contains the following attribution: “Reprinted with permission from SISO Inc.” The material may not be used for a commercial purpose without express written permission from the SISO Inc. Board of Directors.

SISO Inc. Board of Directors

### 7901 4th St. N, Suite 300-4043

St. Petersburg, FL 33702, USA

### A.2 Object Class Structure Table

General introduction: The object class structure of an object model is defined by a set of relations among classes of objects from the simulation or federation domain. The object class structure table represents the class -subclass hierarchy of o bject classes. It is populated from the most general object classes in the left -most column, followed by all of their immediate subclasses in the next column, and then further levels of subclasses, as required. Finally, the most specific object classes are  specified in the right-most column. Each object class in the object class structure table is followed by information on publication and subscription capabilities enclosed in parentheses:  P (Publish): At least one federate is capable of publishing at least one attribute of the object class.  S (Subscribe): At least one federate is capable of subscribing to at least one attribute of the object class.  PS (PublishSubscribe): At least one federate is capable of publishing at least one attribute and at least on e federate is capable of subscribing to at least one attribute of the object class.  N (Neither): No federate is capable of either publishing or subscribing to any attributes of the object class.

<a id="source-pdf-page-55"></a>

## Source PDF page 55

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 55 of 90 This is an approved SISO Standard. Explanatory information with individual table entries may be included by using a notes pointer. Pointers to notes consist of a uniquely identifying note label (or a series of comma -separated labels) preceded by an asterisk and enclosed by brackets. The notes themselves are included in the notes table. For detailed information on the table format, see Reference 6. There are no Link 16 unique object classes in the Link 16 FOM module. The RadioTransmitter object shown in Table A-1 is a scaffolding class to hold note Link16_1. Refer to this note (see Table A-10) for information on the integration of datatype JTIDSTransmitterStruct.

### Table A-2: RadioTransmitter Object

- `RadioTransmitter (PS) *[Link16_1]`
### A.3 Interaction Class Structure Table

General introduction: The interaction class structure of an object model is defined by a set of relations among classes of interactions from the simulation or federation domain. The interaction class structure table represents the class -subclass hierarchy of interaction classes, in much the same way that objects are described in the object class structure table. Each interaction class in the interaction class structure table is followed by information on publishing and subscribing capabilities enclosed in parentheses:  P (Publish): At least one federate is capable of publishing the interaction class.  S (Subscribe): At least one federate is capable of subscribing to the interaction class.  PS (PublishSubscribe): At least one federate is capable of publishing and at least one federate is capable of subscribing to the interaction class.  N (Neither): No federate is capable of either publishing or subscribing to the interaction  class. Pointers to notes may be included, in the same way as described for the object class structure table. For detailed information on the table format, see Reference 6. Refer to note Link16_2 (see Table A-10) for information on the interpretation of the Parent class.

<a id="source-pdf-page-56"></a>

## Source PDF page 56

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 56 of 90 This is an approved SISO Standard.

### Table A-3: Interaction Class Structure Table

- `Parent (PS)`
- `*[Link16_2]`
- `TDLBinaryRadioSignal (N) Link16RadioSignal (S) JTIDSMessageRadioSignal (PS)`
- `RTTABRadioSignal (PS)`
- `RTTReplyRadioSignal (PS)`
- `JTIDSVoiceCVSDRadioSignal (PS)`
- `JTIDSVoiceLPC10RadioSignal (PS)`
- `JTIDSVoiceLPC12RadioSignal (PS)`
- `JTIDSLETRadioSignal (PS)`
- `VMFRadioSignal (PS)`
### A.4 Attribute Table

General introduction:  Each class of simulation domain objects is characterized by a fixed set of attribute types. These attributes are named portions of their object’s state whose values can change over time. The attribute table describes all object attributes represented in a federation. For detailed information on the table format, see Reference 6. There are no Link 16 unique object classes in the Link 16 FOM module. Refer to note Link16_1 (see Table A-10).

### A.5 Parameter Table

General introduction:  Most interaction classes are characterized according to a list of one or more interaction parameters. Interaction parameters are used to associate relevant and useful information with classes of interactions. The parameter table describes all interaction parameters that may be represented in a federation. For detailed information on the table format, see Reference 6.

### Table A-4: Parameter Table

- `Interaction Parameter Datatype Available`
- `Dimensions`
- `Transportation Order`
- `JTIDSLETRadioSignal LETHeader LETHeaderStruct NA HLAbestEffort Receive`
- `TADILJMessage TADILJWordStructLengthlessArray1Plus`

<a id="source-pdf-page-57"></a>

## Source PDF page 57

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 57 of 90 This is an approved SISO Standard. Interaction Parameter Datatype Available Dimensions Transportation Order JTIDSMessageRadioSignal JTIDSHeader JTIDSHeaderStruct NA HLAbestEffort Receive TADILJMessage TADILJWordStructLengthlessArray1Plus JTIDSVoiceCVSDRadioSignal DataLength BitsUnsignedInteger16 NA HLAbestEffort Receive JTIDSHeader JTIDSHeaderStruct Data OctetLengthlessArray29Plus JTIDSVoiceLPC10RadioSignal DataLength BitsUnsignedInteger16 NA HLAbestEffort Receive JTIDSHeader JTIDSHeaderStruct Data OctetLengthlessArray29Plus JTIDSVoiceLPC12RadioSignal DataLength BitsUnsignedInteger16 NA HLAbestEffort Receive JTIDSHeader JTIDSHeaderStruct Data OctetLengthlessArray29Plus Link16RadioSignal  NPGNumber NetworkParticipationGroupNumber NA HLAbestEffort Receive NetNumber NetworkNumber TSEC_CVLL CryptoVariable MSEC_CVLL CryptoVariable SISOSTD002Version SISOSTD002VersionEnum8 Link16Version Link16VersionEnum8 TimeSlotID TimeSlotIdentifier PerceivedTransmitTime NTPTimestampStruct RTTABRadioSignal RTTAB RTTABStruct NA HLAbestEffort Receive RTTReplySignal RTTReply RTTReplyStruct NA HLAbestEffort Receive VMFRadioSignal  JTIDSHeader JTIDSHeaderStruct NA HLAbestEffort Receive MessageData TADILJWordStructLengthlessArray1Plus

<a id="source-pdf-page-58"></a>

## Source PDF page 58

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 58 of 90 This is an approved SISO Standard.

### A.6 Basic Data Representation Table

General introduction:  Basic data representation is the underpinning of all OMT datatypes. These basic data representations cannot be directly used as a named datatype in any OMT datatype table, but rather are the basis upon which named datatypes are built. For detailed information on the table format, see Reference 6. NOTE – Cells that are shaded in blue are defined in RPR FOM 2.0.

### Table A-5: Basic Data Representation Table

- `Name Size in`
- `bits`
- `Interpretation Endian Encoding`
- `RPRunsignedInteger16BE 16 Integer in the range [0, 2^16-1] Big 16-bit unsigned integer.`
- `RPRunsignedInteger32BE 32 Integer in the range [0, 2^32-1] Big 32-bit unsigned integer.`
### A.7 Simple Datatype Table

General introduction:  The simple datatype table describes simple, scalar data items. For detailed information on the table format, see Reference 6. NOTE – Cells that are shaded in blue are defined in RPR FOM 2.0.

### Table A-6: Simple Datatype Table

- `Name Representation Units Resolutio`
- `n`
- `Accuracy Semantics`
- `BitsUnsignedInteger16 RPRunsignedInteger16BE bit 1 perfect Transmission size, in number of bits.`
- `CryptoVariable HLAoctet NA NA NA An integer identification of the crypto`
- `variable used for JTIDS`
- `transmission and message`
- `encryption. This variable allows for`
- `simulated crypto netting. Valid`
- `range: [0,127] and all bits set to one`
- `indicating no statement/wildcard.`
- `NetworkNumber HLAoctet NA NA NA Used to create virtual sub-circuits`
- `within NPG for stacked nets or`
- `between NPGs for multi-net`
- `operations. Valid range: [0,127].`

<a id="source-pdf-page-59"></a>

## Source PDF page 59

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 59 of 90 This is an approved SISO Standard. Name Representation Units Resolutio n Accuracy Semantics NetworkParticipationGroupNumber RPRunsignedInteger16BE NA NA NA Used to segregate information within a JTIDS/MIDS network. Creates virtual networks of participants. Valid range: [0,511]. Octet HLAoctet NA 1 perfect Uninterpreted 8-bit value. TimeSlotIdentifier RPRunsignedInteger32BE NA NA NA Bits 0-16 indicate the Time Slot Number; valid arrange [0,98303]. Time Slot 0 represents time slot A-1, and Time Slot 98303 represents C- 32767. When the Epoch is 112, the last valid Time Slot is 45151 (end of the day). Bits 17-23 are padding and set to 0. Bits 24-31 indicate the Epoch number; valid range [0,112]. An epoch is 12.8 minutes long, 112.5 epochs in a 24 hour day. All bits set to one (including the padding field) indicate a no statement/wildcard. UnsignedInteger32 RPRunsignedInteger32BE NA 1 perfect Integer in the range [0, 2^32-1].

### A.8 Enumerated Datatype Table

General introduction:  The enumerated datatype table describes data elements that can take on a finite discrete set of possible values. For detailed information on the table format, see Reference 6. NOTE – Cells that are shaded in blue are defined in RPR FOM 2.0.

<a id="source-pdf-page-60"></a>

## Source PDF page 60

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 60 of 90 This is an approved SISO Standard.

### Table A-7: Enumerated Datatype Table

- `Name Representation Enumerator Values Semantics`
- `JTIDSPrimaryModeEnum8 HLAoctet NTR 1 The primary mode of a JTIDS system`
- `[UID 173]. JTIDSUnitParticipant 2`
- `JTIDSSecondaryModeEnum8 HLAoctet None 0 The JTIDS secondary mode of`
- `operation [UID 174]. NetPositionReference 1`
- `PrimaryNavigationController 2`
- `SecondaryNavigationController 3`
- `JTIDSSynchronizationStateEnum`
- `8`
- `HLAoctet NoStatement 0 Describes the state of synchronization`
- `that the JTIDS system has achieved`
- `[UID 175]. InitialNetEntry 1`
- `CoarseSynchronization 2`
- `FineSynchronization 3`
- `Link16VersionEnum8 HLAoctet NoStatement 0 Link 16 version [UID 800].`
### MIL-STD-6016C 1

### MIL-STD-6016D 2

### MIL-STD-6016E 3

### MIL-STD-6016F 4

### MIL-STD-6016FC1 5

STANAG5516Ed3 103 STANAG5516Ed4 104 STANAG5516Ed5 105 STANAG5516Ed6 106 STANAG5516Ed8 108 SISOSTD002VersionEnum8 HLAoctet SISO-STD-002-2006 0 SISO-STD-002 version [UID 736].

### SISO-STD-002-2021 1

<a id="source-pdf-page-61"></a>

## Source PDF page 61

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 61 of 90 This is an approved SISO Standard. Name Representation Enumerator Values Semantics SpreadSpectrumEnum16 RPRunsignedInteger16BE JTIDS_MIDS_SpectrumType 2 The type of spread spectrum characteristics employed by a transmitter. TimeSlotAllocationLevelEnum8 HLAoctet LowFidelityLevel0 0 Time Slot Allocation (TSA) level of fidelity. See SISO-STD-002 for detailed descriptions and requirements [UID 172]. LowFidelityLevel1 1 MediumFidelityLevel2 2 MediumFidelityLevel3 3 HighFidelityLevel4 4

### A.9 Array Datatype Table

General introduction:  The array datatype table describes indexed homogenous collection s of datatypes; these constructs are also known as arrays or sequences. For detailed information on the table format, see Reference 6.

### Table A-8: Array Datatype Table

- `Name Element type Cardinality Encoding Semantics`
- `TADILJWordStructLengthlessArray1Plus TADILJWordStruct [1..2147483647] RPRlengthlessArray Array of at least 1`
- `TADILJWordStruct, encoded without`
- `the number of array elements.`
- `OctetArray6 Octet 6 HLAfixedArray Array of 6 octets.`
- `OctetArray10 Octet 10 HLAfixedArray Array of 10 octets.`
- `OctetLengthlessArray29Plus Octet [29..2147483647] RPRlengthlessArray Array of at least 29 octets, encoded`
- `without the number of array`
- `elements.`
### A.10 Fixed Record Datatype Table

General introduction:  The fixed recor d datatype table shall be used to describe heterogeneous collections of types; these constructs are also known as records or structures. Each entry in the fixed record datatype table may contain fields that are of other types,

<a id="source-pdf-page-62"></a>

## Source PDF page 62

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 62 of 90 This is an approved SISO Standard. such as simple datatypes, fix ed records, arrays, enumerations, or variant records. This enables building “structures of data structures”. For detailed information on the table format, see Reference 6.

### Table A-9: Fixed Record Datatype Table

- `Record name Field Encoding Semantics`
- `Name Type Semantics`
- `JTIDSHeaderStruct Data OctetArray6 In total 48 bits, with the following`
- `fields:`
- `Bits 0-2: Time Slot Type.`
- `Bit 3: Relay Transmission`
- `Indicator.`
- `Bits 4-18: Source Track Number`
- `of Sender.`
- `Bits 19-34: Secure Data Unit`
- `Serial Number.`
- `Bits 35-47: Padding, set to 0.`
- `HLAfixedRecord Link 16 Header`
- `Word (35 bits) for`
- `common`
- `messages, JTIDS`
- `voice, and VMF.`
- `Padded to 48 bits.`

<a id="source-pdf-page-63"></a>

## Source PDF page 63

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 63 of 90 This is an approved SISO Standard. Record name Field Encoding Semantics Name Type Semantics JTIDSTransmitterStruct TimeSlotAllocationLeve l TimeSlotAllocationL evelEnum8 TSA level of fidelity. HLAfixedRecord Contains JTIDS specific information about the JTIDS transmitter system. TransmittingTerminalPri maryMode JTIDSPrimaryMode Enum8 The primary mode of a JTIDS system. TransmittingTerminalSe condaryMode JTIDSSecondaryM odeEnum8 The JTIDS secondary mode of operation. SynchronizationState JTIDSSynchronizati onStateEnum8 The state of synchronization that the JTIDS system has achieved. NetworkSynchronizatio nID UnsignedInteger32 TSA Levels 0-2: may be set to 0 (wildcard) or the unique 32-bit value of a simulated net. TSA Levels 3 and 4: set to the unique 32-bit value of a simulated net. Only an NTR can generate a Network Synchronization ID; all other participants use the ID obtained from the NTR to which they are synchronized. LETHeaderStruct Data OctetArray6 In total 48 bits, with the following fields: Bits 0-3: LET ID Symbol. Bit 4: Relay Transmission Indicator. Bits 5-8: LET Message Packing Type. Bits 9-23: Source Track Number of Sender. Bits 24-39: Secure Data Unit Serial Number. Bits 40-47: Padding, set to 0. HLAfixedRecord Link 16 Enhanced Throughput (LET) Header Word (40 bits). Padded to 48 bits.

<a id="source-pdf-page-64"></a>

## Source PDF page 64

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 64 of 90 This is an approved SISO Standard. Record name Field Encoding Semantics Name Type Semantics NTPTimestampStruct Seconds UnsignedInteger32 Number of seconds since 0 h 1 January 1900 UTC. HLAfixedRecord 64-bit timestamp format according to RFC 5905. All bits set to one in both fields indicate a no statement/wildcard. Fraction UnsignedInteger32 Fraction of a second, in 1/(2^32) resolution (232 picoseconds). RTTABStruct Data OctetArray6 In total 48 bits, with the following fields: Bits 0-2: Time Slot Type. Bit 3: RTT Interrogation Type. Bits 4-18: variable content, see MIL-STD-6016 or STANAG 5516. Bits 19-34: Secure Data Unit Serial Number. Bits 35-47: Padding, set to 0. HLAfixedRecord JTIDS RTT A/B word (35 bits). Padded to 48 bits. RTTReplyStruct Data OctetArray6 In total 48 bits, with the following fields: Bits 0-18: Time of Arrival. Bits 19-34: Secure Data Unit Serial Number. Bits 35-47: Padding, set to 0. HLAfixedRecord JTIDS RTT Reply word (35 bits). Padded to 48 bits. TADILJWordStruct Data OctetArray10 In total 80 bits, with the following fields: Bits 0-1: Word Format. Bits 2-69: variable content, see MIL-STD-6016 or STANAG

### 5516 for FWF J-Words.

Bits 70-74: Parity. Bits 75-79: Padding, set to 0. HLAfixedRecord TADIL-J word (75 bits) used for Fixed Word Format (FWF) messages and the Variable Message Format (VMF). Padded to

### 80 bits.

<a id="source-pdf-page-65"></a>

## Source PDF page 65

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 65 of 90 This is an approved SISO Standard.

### A.11 Notes Table

General introduction:  Any entry within any of the OMT tables may be annotated with additional descriptive inf ormation outside of the immediate

### table structure. The mechanism for attaching one or more notes to an OMT table entry is to include a notes pointer in the

- `appropriate table cell. The notes themselves are associated with the note label and included in the notes table. A single`
- `note may be referenced numerous times in OMT tables`
- `For detailed information on the table format, see Reference 6.`
### Table A-10: Notes Table

- `ID Text`
- `Link16_1 The RadioTransmitter class is a scaffolding class, i.e., it refers to a class (structure) in which the Link 16 FOM module is integrated.`
- `This class is to represent all capabilities as provided with the DIS Transmitter PDU, in accordance with IEEE Std 1278.1(tm) -2012, and`
- `contain an attribute using the JTIDSTransmitterStruct.`
- `Link16_2 The Parent class is a scaffolding class, i.e., it refers to an interaction class (structure) in which the Link 16 FOM module is integrated.`
- `The TDLBinaryRadioSignal class (and its children classes) is to be integrated as a subclass of an interaction class providing the DIS`
- `Signal PDU capabilities, in accordance with IEEE Std 1278.1(tm) -2012.`
### A.12 Object Class Definition Table

General introduction:  The lexicon tables provides a means to define all object  classes, interaction classes, object class attributes, and interaction parameters to achieve a common understanding of the semantics of the data. The object class definition table describes the object classes. For detailed information on the table format, see Reference 6. There are no Link 16 unique object classes in the Link 16 FOM module.

### A.13 Interaction Class Definition Table

General introduction:  The lexicon tables provides a means to define all object classes, interaction clas ses, object class attributes, and interaction parameters to achieve a common understanding of the semantics of the data. The interaction class definition table describes the interactions. For detailed information on the table format, see Reference 6.

### Table A-11: Interaction Class Definition Table

- `Class Definition`
- `JTIDSLETRadioSignal Link 16 radio signal containing Link 16 Enhanced Throughput (LET) encoded`
- `messages.`

<a id="source-pdf-page-66"></a>

## Source PDF page 66

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 66 of 90 This is an approved SISO Standard. Class Definition JTIDSMessageRadioSignal Link 16 radio signal containing Fixed Word Format (FWF) TADIL-J messages. JTIDSVoiceCVSDRadioSignal Link 16 radio signal containing a voice message encoded using CVSD. JTIDSVoiceLPC10RadioSignal Link 16 radio signal containing a voice message encoded using LPC10. JTIDSVoiceLPC12RadioSignal Link 16 radio signal containing a voice message encoded using LPC12. Link16RadioSignal  Link 16 radio signal common base class. RTTABRadioSignal Link 16 radio signal containing an RTT/A or RTT/B message. RTTReplySignal Link 16 radio signal containing an RTT Reply message. TDLBinaryRadioSignal Parent class for all TDL radio signals. VMFRadioSignal  Link 16 radio signal containing Variable Message Format (VMF) messages.

### A.14 Attribute Definition Table

General introduction:  The lexic on tables provides a means to define all object classes, interaction classes, object class attributes, and interaction parameters to achieve a common understanding of the semantics of the data. The attribute definition table describes the attributes that characterize object classes. For detailed information on the table format, see Reference 6. There are no Link 16 unique object classes in the Link 16 FOM module.

### A.15 Parameter Definition Table

General introduction:  The lexicon table s provides a means to define all object classes, interaction classes, object class attributes, and interaction parameters to achieve a common understanding of the semantics of the data. The parameter definition table describes the parameters that are associated with interaction classes. For detailed information on the table format, see Reference 6.

### Table A-12: Parameter Definition Table

- `Class Parameter Definition`
- `JTIDSLETRadioSignal LETHeader LET Header Word. Not optional.`
- `TADILJMessage LET message data words. Not optional.`

<a id="source-pdf-page-67"></a>

## Source PDF page 67

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 67 of 90 This is an approved SISO Standard. Class Parameter Definition JTIDSMessageRadioSignal JTIDSHeader Link 16 Header Word. Not optional. TADILJMessage Link 16 message data words. Not optional. JTIDSVoiceCVSDRadioSignal DataLength The length of the encoded voice in the Data parameter, in bits. Not optional. JTIDSHeader Link 16 Header Word. Not optional. Data JTIDS CVSD encoded voice data. Not optional. JTIDSVoiceLPC10RadioSignal DataLength The length of the encoded voice in the Data parameter, in bits. Not optional. JTIDSHeader Link 16 Header Word. Not optional. Data JTIDS LPC10 encoded voice data. Not optional. JTIDSVoiceLPC12RadioSignal DataLength The length of the encoded voice in the Data parameter, in bits. Not optional. JTIDSHeader Link 16 Header Word. Not optional. Data JTIDS LPC12 encoded voice data. Not optional.

<a id="source-pdf-page-68"></a>

## Source PDF page 68

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 68 of 90 This is an approved SISO Standard. Class Parameter Definition Link16RadioSignal  NPGNumber Network/Needline Participation Group (NPG) number. Not optional. NetNumber Network Number. Not optional. TSEC_CVLL Transmission Security Crypto Variable Logic Label. Optional for TSA Levels 0-2; default value: all bits set to one (no statement/wildcard). MSEC_CVLL Message Security Crypto Variable Logic Label. Optional for TSA Levels 0-2; default value: all bits set to one (no statement/wildcard). SISOSTD002Version Indicates which SISO-STD-002 version was used, i.e., whether byte swapping has or has not been used in the Message Data field (0 = SISO-STD-002-2006, legacy byte swapping employed; 1 = SISO-STD-002-2021, new method, bit stream, no byte swapping employed). Not optional. Link16Version Indicates which version of MIL-STD-6016 or STANAG 5516 is being used. Optional; default value: NoStatement. TimeSlotID Time slot identification. Optional for low-fidelity TSA Levels (0, 1); default value: all bits set to one (no statement/wildcard). PerceivedTransmitTime The time at which the radio signal is transmitted. Optional for low-fidelity synchronization (TSA Levels 0-3); default value: all bits set to one (no statement/wildcard). RTTABRadioSignal RTTAB JTIDS RTT A/B message word. Not optional. RTTReplySignal RTTReply JTIDS RTT reply message word. Not optional. VMFRadioSignal  JTIDSHeader Link 16 Header Word. Not optional. MessageData Link 16 message data words with VMF information fields. Not optional.

Navigation: previous [HLA requirements](06-hla-requirements-pages-044-051.md) | [coverage index](README.md) | next [Annex B - DIS-HLA translations](08-annex-b-dis-hla-translations-pages-069-088.md)
