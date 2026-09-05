# Overview

Source: `SISO-STD-002-2021.pdf`, PDF pages 12-13.

Navigation: previous [Front matter](00-front-matter-pages-001-011.md) | [coverage index](README.md) | next [Definitions](02-definitions-pages-014-019.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-12"></a>

## Source PDF page 12

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 12 of 90 This is an approved SISO Standard.

### 1 Overview

### 1.1 Scope

This standard applies only to Link 16/JTIDS/MIDS. It does not ad dress Link 16 over Satellite Communications (SATCOM). In developing a protocol for simulating Link 16 in Distributed Interactive Simulation (DIS) and High Level Architecture (HLA), it is recognized that there are widely varying requirements for achieving needed fidelity among different users. This standard establishes procedures that may be used by the vast majority of users, by establishing discrete, scalable, interoperable levels of fidelity for different users. This, in turn, allows for low cost initial implementation with a path toward upgrading to detailed Link 16 emulation as requirements evolve. The DIS simulation protocol for Link 16 is described in terms of the established DIS Transmitter and Signal Protocol Data Units (PDUs). There has been no chan ge to the Transmitter or Signal PDUs described in Reference 4. Link 16 specific enumerations have been created to populate the standard fields and records. The implementation of Link 16 exploits the fact that both these PDUs are  variable length. In the case of the Transmitter PDUs, this protocol sets forth how the variable length Modulation Parameters field must be populated. In the case of the Signal PDU, Link 16 specific information is relegated to the variable length Data field. The Link 16 HLA specification is defined in the form of a Federation Object Model ( FOM) module, in compliance with Reference 6. For actual exchange within an HLA federation, it should be incorporated into a FOM; in particular , the Real -time Platform Reference (RPR) FOM. Furthermore, a mapping is provided between the DIS PDU implementations and the corresponding HLA objects and interactions .

### 1.2 Purpose

There are immediate operational requirements for existing military simulations to exchange Link 16 data using a single interoperable standard. Several protocols have evolved to satisfy specific needs. The NATO STANAG 5602 Standard Interface for Multiple Platform Link Evaluation (SIMPLE) Link 16 standard [9] is one such protocol. As military distributed simulation evolves further in mission scale and complexity, tactical data link implementations need to interoperate.

### 1.3 Objectives

The objective of this document is to establish a standard for Link 16 message ex change and JTIDS network simulation in the DIS and HLA interoperability frameworks. The intent is to prescribe the content of the standard fields of the Transmitter and Signal PDUs (and the corresponding Link 16 FOM module interactions) and establish proce dures for their use. Compliance with these procedures will facilitate interoperability among Link 16 simulation systems.

### 1.4 Intended Audience

This standard is intended to be used by implementers of Link 16 data link message exchange over DIS or HLA protocols.

<a id="source-pdf-page-13"></a>

## Source PDF page 13

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 13 of 90 This is an approved SISO Standard.

### 2 References

The following documents are referenced herein. For undated references, the latest published version of the document applies, including any amendments. If a conflict exists with a referenced document, this document shall take precedence. Ref # Document Number Title

### 1  SISO-STD-001.1 Standard for Real-time Platform Reference Federation Object Model,

Version 2.0, 10 August 2015

### 2  SISO-STD-001 Standard for Guidance, Rationale, and Interoperability Modalities for the

Real-time Platform Reference Federation Object Model, Version 2.0, 10 August 2015

### 3 5 SISO-REF-010 Reference for Enumerations for Simulation Interoperability

### 4  IEEE Std 1278.1™ IEEE Standard for Distributed Interactive Simulation – Application

Protocols

### 5  IEEE Std 1516™ IEEE Standard for Modeling and Simulation (M&S) High Level

Architecture (HLA)

### 6  IEEE Std 1516.2™ IEEE Standard for Modeling and Simulation (M&S) High Level

Architecture (HLA) – Object Model Template (OMT) Specification

### 7  MIL-STD-6016 Department Of Defense Interface Standard Tactical Data Link (TDL) 16

Message Standard

### 8  STANAG 5516 NATO STANAG 5516, Tactical Data Exchange - Link 16

### 9  STANAG 5602 NATO STANAG 5602, Standard Interface for Multiple Platform Link

Evaluation (SIMPLE)

### 10  ISBN-10:

0877798095 Merriam-Webster's Collegiate Dictionary, Eleventh Edition forward

### 11  RFC 5905 Network Time Protocol Version 4: Protocol and Algorithms

Specification, June 2010

### 12  SSS-M-10201 System Segment Specification for the Multifunctional Information

Distribution System (MIDS) Low-Volume Terminal and Ancillary Equipment for Block Upgrade 2

### 13  135-02-005 Understanding Voice and Data Link Networking, Northrop Grumman’s

Guide to Secure Tactical Data Links

Navigation: previous [Front matter](00-front-matter-pages-001-011.md) | [coverage index](README.md) | next [Definitions](02-definitions-pages-014-019.md)
