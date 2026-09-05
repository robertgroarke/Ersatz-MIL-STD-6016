# HLA requirements

Source: `SISO-STD-002-2021.pdf`, PDF pages 44-51.

Navigation: previous [DIS Signal PDU and Link 16 data](05-dis-signal-pdu-and-link-16-data-pages-034-043.md) | [coverage index](README.md) | next [Annex A - FOM module](07-annex-a-fom-module-pages-052-068.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-44"></a>

## Source PDF page 44

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 44 of 90 This is an approved SISO Standard. Octet 39 Octet 38 Octet 37 Octet 36

### 159                             130 129 128

Second J-Word J-Word Format

Octet 43 Octet 42 Octet 41 Octet 40

### 191                               160

Second J-Word Continued

Octet 47 Octet 46 Octet 45 Octet 44

### 223             210 209 208 207    203 202    198 197     192

Third J-Word (bits 15--2) J Word Format Padding Parity Second J-Word Continued (bits 69-64)

Octet 51 Octet 50 Octet 49 Octet 48

### 255                               224

Third J-Word Continued

Octet 55 Octet 54 Octet 53 Octet 52

### 287    283 282    278 277                     256

Padding Parity Third J-Word Continued

### 4.3 Link 16 Implementation Using HLA

Link 16 TDL simulation is typically part of a larger distributed federation, where the HLA implementation of the Link 16 protocol will be part of the Federation Object Model (FOM). Such federations are used for many purposes including system development, test and evaluation, and training. The HLA design for Link 16 implementation is defined in a FOM module  in the HLA 1516 -2010 FOM format [ 6]. However, not every federation that will use the Link 16 FOM module has the same FOM. FOMs that incorporate the Link 16 FOM module may already have definitions for basic concepts such as radio transmitters and radio signals, or their equivalents. If these definitions were included in the Link 16 FOM module then there would be dupl ication and potentially incompatibilities with existing definitions in the “parent” FOM in which the Link 16 module is incorporated. Therefore the Link 16 FOM module does not include definitions for some basic concepts, and relies on the parent FOM to prov ide suitable definitions. The Link 16 FOM module can be considered as a “template” for creating a concrete FOM module for inclusion in the parent FOM. In addition, the Link 16 FOM module is designed to build upon existing datatypes and classes in the RPR FOM [1], allowing an integration with the RPR FOM 2.0 without changing any of its existing capabilities. See section 4.3.7 for a detailed description.

### 4.3.1 The Link 16 FOM Module

### 4.3.1.1 Assumptions

The Link 16 FOM module assumes that the parent FOM contains: 1. An object class that represents a radio transmitter with the general transmitter capabilities as described in section 4.1. 2. An interaction class that represents a tactical data link c apable radio signal. This class will act as a base class for the TDLBinaryRadioSignal defined in the Link 16 FOM module with the general transmission capabilities as described in section 4.1.

<a id="source-pdf-page-45"></a>

## Source PDF page 45

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 45 of 90 This is an approved SISO Standard. 3. A mechanism for determining the numb er of TDL messages contained in the signal interaction. 4. A mechanism for associating any instance of the radio signal interaction class with an instance of the radio transmitter object class that it emanated from.

### 4.3.1.2 Naming Convention

Conventions within the Li nk 16 FOM module follow those adopted by the RPR FOM version 2.0 [ 1]. These conventions are described in more detail in the RPR FOM GRIM, section 6.8.1 [ 2].

### 4.3.1.3 Representations

The Link 16 FOM module file  (named Link_16_v2.0.xml and available on the SISO website), in compliance with the HLA Evolved FOM schema, shall be considered normative, while the human readable tables in Annex A  shall be considered informative. If any statem ent in this document is interpreted to be in conflict with the Link 16 FOM module in XML format, the content of the XML file shall take precedence.

### 4.3.2 Levels of Fidelity

The HLA levels of fidelity are directly equivalent to the corresponding DIS levels of fid elity as defined in section 4.1.2. The requirements for mixed TSA Levels as defined in section  4.1.3 also apply to the usage of the Link 16 FOM module.

### 4.3.3 Time Synchronization

For time-managed HLA federations the logical time shall be used as a time source for all time references. For non -time managed HLA federations the system time shall be used as a time source for all time references. See also section 4.1.1 requirement 12. In this case the HLA time synchronization mechanism is directly equivalent to the corresponding mechanism for DIS as defined in section 4.1.4 A time -managed HLA federation requires a common understandi ng of logical time by all federates. According to the description of rule 10 in the HLA standard (IEEE Std 1516 -2010, section 6.5): "Federation designers will identify their time management approach as part of their implementation design. Federates shall a dhere to the time management approach of the federation." Federation designers need to make agreements on the mapping of the HLA logical time to the time value in Link16RadioSignal messages, including agreements on the time value that corresponds with the HLA logical time zero (the start time of the federation execution). A federate shall implement these agreements and shall provide the HLA logical time in the RTI time management service calls for which the data in the Link16RadioSignal message is valid.

### 4.3.4 Protocol Implementation Details

This section defines how Link 16 FOM module-compliant federates shall implement the Link 16 protocol. The HLA protocol implementation details are directly equivalent to the corresponding details for DIS as defined in section 4.2.

### 4.3.4.1 Object Class Data

The Link 16 FOM module defines no new object classes. Instead, the FOM module defines a single fixed record datatype ( JTIDSTransmitterStruct, see section A.10) that corresponds t o the modulation parameters in the DIS Transmitter PDU defined in section 4.2.1. This datatype should be added to the parent FOM either directly into the radio transmitter object class or into a suitable subclass of the radio transmitter object class. The datatype can be added as an attribute or into another data structure in an existing attribute.

<a id="source-pdf-page-46"></a>

## Source PDF page 46

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 46 of 90 This is an approved SISO Standard. The modulation parameters requirements as specified under item 10 in section 4.2.1 also apply to the usage of the JTIDSTransmitterStruct. Refer to Table 18 for a mapping between the JTIDSTransmitterStruct fields and the DIS Transmitter PDU fields. All other requirements defined in section 4.2.1 apply to the equivalent attributes of this object class.

### Table 18: JTIDSTransmitterStruct Mapping to DIS Modulation Parameters

- `JTIDSTransmitterStruct Transmitter PDU Field`
- `Field Name`
- `TimeSlotAllocationLevel Modulation Parameter #1 Time Slot Allocation Level`
- `TransmittingTerminalPrimaryMode Modulation Parameter #2 Transmitting Terminal Primary`
- `Mode`
- `TransmittingTerminalSecondaryMode Modulation Parameter #3 Transmitting Terminal Secondary`
- `Mode`
- `SynchronizationState Modulation Parameter #4 Synchronization State`
- `NetworkSynchronizationID Modulation Parameter #5 Network Synchronization ID`
### 4.3.4.2 Interaction Class Data

The Link 16 FOM module includes a family of interactions that have been developed to support other data link implementations. The family of interactions is a hierarchy in which the base class for the Link 16 interactions is a generic class, the TDLBinaryRadioSignal interaction. This class is a class without parameters, and this class cannot be published nor sub scribed to. The specific parameters are properties of the various subclasses of this generic base class, and these are the subclasses that are published and subscribed to. This hierarchy of interaction classes provides for Declaration Management (DM) filte ring, enabling the federate to only receive the data link messages it is interested in. The Link16RadioSignal interaction, a subclass of the TDLBinaryRadioSignal interaction (see Table A-3), contains parameters for the Link 16 Simu lation Network Header fields (see Table 8) as shown in Table A- 4. The field ‘Message Type Identifier’ is represented in the Link 16 FOM module by the eight subclasses of Link16RadioSignal. These subclasses,  JTIDSMessageRadioSignal, RTTABRadioSignal, RTTReplyRadioSignal, JTIDSVoiceCVSDRadioSignal, JTIDSVoiceLPC10RadioSignal, JTIDSVoiceLPC12RadioSignal, JTIDSLETRadioSignal, and VMFRadioSignal are the actual interactions that can be published within the HLA federation. These classes contain the Link 16 message data as shown in Table 9 through Table 16 respectively. It is uncommon in HLA FOMs to use datatypes with sizes other than 8, 16, 32, or 64 bits. Since it i s required that the content of the Link 16 message is exactly bit encoded as per the TADIL J specification (see section 4.1.1), a field identification as per the aforementioned tables has not been applied to the datatypes used b y the interaction class parameters. Instead, arrays of octets are used, either directly for the parameter datatype or indirectly in a fixed record datatype. However, the 48 bits (6 octets) of the headers are separated from the rest of the message data. Als o, due to the requirement for encoding as per the TADIL J messages, the IEEE Std 1516.2™ [ 6] variable array encoding cannot be used, as this includes the number of elements in the array. Instead, the RPRlengthlessArray is used, an encoding without the array length, as defined in the RPR FOM GRIM, section 6.8.5.1 [ 2]. The TDLBinaryRadioSignal interaction class (and its child classes) shall be integrated in a FOM as a subclass equivalent of the DIS Signa l PDU (see 4.3.1.1). All other requirements defined in section 4.2.2 apply to the equivalent parameters, when present, of this interaction class .

<a id="source-pdf-page-47"></a>

## Source PDF page 47

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 47 of 90 This is an approved SISO Standard.

### 4.3.5 FOM Module Definition

The complete Link 16 FOM module is defined in Link_16_ v2.0.xml and can be downloaded from the SISO website. It is also represented in human-readable form in Annex A. For the special case where the parent FOM is the RPR FOM version 2.0 , a complete set of pre-built FOM modules can be downloaded from the SISO website.

### 4.3.6 Adding the Link 16 FOM Module to a Parent FOM

Note: If the parent FOM is the RPR FOM then see section 4.3.7 instead. Adding the Link 16 FOM module to a parent FOM consists of the following steps: 1. Identify the object class representing a radio transmitter. A. If the parent FOM does not contain such a class then a Radio Transmitter object class should be added to the parent FOM. B. If the parent FOM already contains such a class an d is designed to support subscription based filter using declaration management then it may be desirable to create a subclass to act as a Link 16 Radio Transmitter. 2. Add the usage of the JTIDSTransmitterStruct structure to the object class identified above. 3. Identify the interaction class representing a radio signal. A. If the parent FOM does not contain such a class then a Radio Signal interaction class should be added to the parent FOM. B. If the parent FOM does contain a suitable interaction class then add the TDLBinaryRadioSignal as a subclass. 4. Add the datatypes defined in Table A-6 through Table A-9.

### 4.3.7 Adding the Link 16 FOM Module to the RPR FOM

If an unmodified RPR FOM 2.0 [ 1] for HLA Evolved is being used, then it is recommended that the pre built RPR FOM with Link 16 FOM modules provided are used. However, if the RPR FOM has been modified for some other federation -specific reason then it will be necessary to integrate  the Link 16 FOM module as follows: Adding the Link 16 FOM module to the RPR FOM consists of the following steps: 1. Update the RPR FOM Communications module to add Link 16 specific types and extend the RPR FOM SpreadSpectrumVariantStruct variant record to in clude the JTIDSTransmitterStruct structure as one of the alternatives. 2. Update the RPR FOM Enumerations module to add Link 16 specific enumerations and the JTIDS_MIDS_SpectrumType enumerator value. 3. Update the Link 16 FOM module to: A. Add the TDLBinaryRadioSig nal as a subclass of the RPR FOM RawBinaryRadioSignal. The resulting RadioSignal interaction class hierarchy is shown in Table 19, with the Link 16 FOM module classes shaded in yellow. B. Remove elements included elsewhere in the modified RPR FOM modules. Detailed instructions are contained in the following sections.

### 4.3.7.1 Updating the RPR FOM Communications Module

1. Add the fixed record datatype JTIDSTransmitterStruct from Table A-9.

<a id="source-pdf-page-48"></a>

## Source PDF page 48

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 48 of 90 This is an approved SISO Standard. 2. Add the alternative for enumerato r JTIDS_MIDS_SpectrumType, using the JTIDSTransmitterStruct, to the variant record datatype SpreadSpectrumVariantStruct, as shown in yellow in Table 21. 3. Update the modelIdentification name, version, modificationDate, and descriptio n, and add a useHistory as appropriate. The RawBinaryRadioSignal parameter SignalData shall not be used to publish the Link 16 messages. Consequently, the RawBinaryRadioSignal parameter SignalDataLength shall either not be published or shall be set to 0. A s per the DIS requirement in section 4.2.2 item 3, the RawBinaryRadioSignal parameter DataRate shall be set to 0. NOTE: DIS to HLA gateways respecting this standard cannot simply forward Signal PDUs a s corresponding RPR FOM RadioSignal based interactions based on the Encoding Class, copying ‘Raw Binary Data’ into the SignalData parameter of a RawBinaryRadioSignal interaction. See Annex B for a detailed guide for DIS-HLA gateway implementation.

### 4.3.7.2 Updating the RPR FOM Enumerations Module

1. Add the following enumerated datatypes from Table A-7: A. JTIDSPrimaryModeEnum8 B. JTIDSSecondaryModeEnum8 C. JTIDSSynchronizationStateEnum8 D. Link16VersionEnum8 E. SISOSTD002VersionEnum8 F. TimeSlotAllocationLevelEnum8 2. Add the enumerator JTIDS_MIDS_SpectrumType (value 2) to the enumerated datatype SpreadSpectrumEnum16 as shown in yellow in Table 20. 3. Update the modelIdentification name, version, modificationDate, a nd description, and add a useHistory as appropriate. Alternatively, the Enumerations module (RPR -Enumerations_v2.0.xml) can be used as provided with SISO-REF-010 from version 30 onwards.

### 4.3.7.3 Updating the Link 16 FOM Module

1. Remove the object class RadioTransmitter. 2. Replace the interaction class parent by scaffolding classes for HLAinteractionRoot.RadioSignal.RawBinaryRadioSignal, i.e., replace: <interactions> <interactionClass notes="Link16_2"> <name>Parent</name> <sharing>PublishSubscribe</sharing> <transportation>HLAbestEffort</transportation> <order>Receive</order> <interactionClass> <name>TDLBinaryRadioSignal</name> ... </interactionClass> </interactionClass> </interactions> With the following:

<a id="source-pdf-page-49"></a>

## Source PDF page 49

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 49 of 90 This is an approved SISO Standard. <interactions> <interactionClass> <name>HLAinteractionRoot</name> <interactionClass> <name>RadioSignal</name> <interactionClass> <name>RawBinaryRadioSignal</name> <interactionClass> <name>TDLBinaryRadioSignal</name> ... </interactionClass> </interactionClass> </interactionClass> </interactionClass> </interactions> 3. Delete the RPR FOM datatypes RPRunsignedInteger16BE, RPRunsignedInteger 32BE, BitsUnsignedInteger16, Octet, and UnsignedInteger32 (it is assumed that these datatypes have not been modified in the base RPR FOM Foundation and Base modules). 4. Delete the datatypes added to the Enumerations and Communication modules: A. JTIDSPrimaryModeEnum8 B. JTIDSSecondaryModeEnum8 C. JTIDSSynchronizationStateEnum8 D. Link16VersionEnum8 E. SISOSTD002VersionEnum8 F. SpreadSpectrumEnum16 G. TimeSlotAllocationLevelEnum8 H. JTIDSTransmitterStruct 5. Delete the notes Link16_1 and Link16_2. 6. Add a Dependency to the Real -time Platform Reference Communication FOM module in the modelIdentification. 7. Update the modelIdentification name, version, modificationDate, and description, and add a useHistory as appropriate.

<a id="source-pdf-page-50"></a>

## Source PDF page 50

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 50 of 90 This is an approved SISO Standard.

### Table 19: RPR FOM Link 16 FOM Module Interactions Class Structure Table

- `RadioSignal`
### (N)

ApplicationSpecifcRadioSignal (PS) DatabaseIndexRadioSignal (PS) EncodedAudioRadioSignal (PS) RawBinaryRadioSignal (PS) TDLBinaryRadioSignal (N) Link16RadioSignal (S) JTIDSMessageRadioSignal (PS) RTTABRadioSignal (PS) RTTReplyRadioSignal (PS) JTIDSVoiceCVSDRadioSignal (PS) JTIDSVoiceLPC10RadioSignal (PS) JTIDSVoiceLPC12RadioSignal (PS) JTIDSLETRadioSignal (PS) VMFRadioSignal (PS)

### Table 20: SpreadSpectrumEnum16 with Link 16 FOM Module Modifications

- `Name Representation Enumerator Values Semantics`
- `SpreadSpectrumEnum16 RPRunsignedInteger16BE None 0 The type of spread spectrum characteristics`
- `employed by a transmitter. SINCGARSFrequencyHop 1`
- `JTIDS_MIDS_SpectrumType 2`

<a id="source-pdf-page-51"></a>

## Source PDF page 51

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 51 of 90 This is an approved SISO Standard.

### Table 21: SpreadSpectrumVariantStruct with Link 16 FOM Module Modifications

- `Record name`
- `Discriminant Alternative`
- `Encoding Semantics`
- `Name Type Enumerator Name Type Semantics`
- `SpreadSpectrum`
- `VariantStruct`
- `SpreadSpectr`
- `umType`
- `SpreadSpectr`
- `umEnum16`
- `SINCGARSFr`
- `equencyHop`
- `SINCGARSMo`
- `dulation`
- `SINCGARSMo`
- `dulationStruct`
- `Modulation`
- `parameters for`
### SINCGARS

radio system. HLAvariant Record Identifies the actual spread spectrum technique in use.

### JTIDS_MIDS_

SpectrumType JTIDSTransmi tterData JTIDSTransmi tterStruct Modulation parameters for Link 16 radio system according to

### SISO-STD-

002.

Navigation: previous [DIS Signal PDU and Link 16 data](05-dis-signal-pdu-and-link-16-data-pages-034-043.md) | [coverage index](README.md) | next [Annex A - FOM module](07-annex-a-fom-module-pages-052-068.md)
