# Annex C - Version changes

Source: `SISO-STD-002-2021.pdf`, PDF pages 89-90.

Navigation: previous [Annex B - DIS-HLA translations](08-annex-b-dis-hla-translations-pages-069-088.md) | [coverage index](README.md) | next none

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-89"></a>

## Source PDF page 89

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 89 of 90 This is an approved SISO Standard. Annex C SISO-STD-002 Changes (Informative)

### C.1 Introduction

SISO-STD-002-2021 (Version 2.0) supersedes SISO -STD-002-2006 (Version 1.0). The principal DIS and HLA changes between these versions are described in the following sections of this annex. Due to the significant changes between Version 1.0 and Version 2.0, the two versions are not compatible. DIS or HLA interoperability betwe en the two versions will require special implementations (e.g., translators, gateways, special programming) to address these differences as needed. As with Version 1.0, implementation of Version 2.0 does not depend on any particular version of IEEE Std 127 8.1™ or IEEE Std 1516™. However, it should be noted that Version 2.0 was developed using IEEE Std 1278.1™ -

### 2012 (DIS Version 7) and IEEE Std 1516™-2010 (HLA Evolved).

### C.2 DIS Changes

The principal DIS changes between Version 1.0 and Version 2.0 are as follows: 1. For the Transmitter PDU, Version 2.0 is based on DIS Version 7 and includes changes in the PDU Header and support for multiple Variable Transmitter Parameters Records. 2. For the Signal PDU: A. Version 2.0 is based on DIS Version 7 and includes changes in the PDU Header. B. The Link 16 Message Data portion of the Data field in Version 2.0 uses a stream of bits, whereas in Version 1.0 the entire Data field is composed of a big endian array of 32-bit unsigned integers which may require byte swapping. C. Version 2.0 incl udes a new “SISO -STD-002 Version” field (within the Link 16 Simulation Network Header of the Data field) which specifies the version of SISO - STD-002 in use (value 0 for Version 1.0, value 1 for Version 2.0). In Version 1.0 the corresponding bits of the PDU are part of a padding field. D. Version 2.0 includes a new “Link 16 Version” field (within the Link 16 Simulation Network Header of the Data field) to aid in troubleshooting Link 16 issues. In Version

### 1.0 the corresponding bits of the PDU are part of a padding field.

E. Version 2.0 clarifies/changes the definition of the Data Length field. In Version 2.0 this field contains the number of bits in the Data field and the Data field may end on a non-byte boundary. Padding that follows the Data field to end the PDU  on a 32 -bit boundary is not included in the Data Length. Version 1.0 did not specify if padding was included in the Data Length field.

### C.3 HLA Changes

The principal HLA changes between Version 1.0 and Version 2.0 are as follows: 1. In Version 2.0, the HLA design  for Link 16 implementation is defined in a FOM module in the HLA 1516 -2010 FOM format. In Version 1.0 it is defined as a Base Object Model (BOM). Note that with Version 2.0 it is still required to adjust the FOM module to integrate it into a parent FOM. F or RPR FOM 2.0 this has already been done and is available for download from the SISO website. 2. Version 2.0 includes the new parameter SISOSTD002Version in the interaction class Link16RadioSignal. Since this is the parent class to all classes representing L ink 16 message types, and this parameter is not optional, each Link 16 message must contain this parameter. 3. Version 2.0 includes the parameter Link16Version in the interaction class Link16RadioSignal. However, since the parameter is optional, interactions may be published without it.

<a id="source-pdf-page-90"></a>

## Source PDF page 90

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 90 of 90 This is an approved SISO Standard. 4. Version 2.0 includes the new parameter DataLength in the interaction classes JTIDSVoiceCVSDRadioSignal, JTIDSVoiceLPC10RadioSignal, and JTIDSVoiceLPC12RadioSignal. This non -optional parameter contains the valid data length (in bits) of the Data parameter. 5. In Version 2.0 the datatype for the Link16RadioSignal parameter PerceivedTransmitTime has changed to a structure of two unsigned 32 -bit integers. This could cause compatibility issues because in Version 1.0 it was incorrectly defined as a signed 64-bit integer. 6. Version 2.0 includes changes in the capitalization of class names and parameter names.

Navigation: previous [Annex B - DIS-HLA translations](08-annex-b-dis-hla-translations-pages-069-088.md) | [coverage index](README.md) | next none
