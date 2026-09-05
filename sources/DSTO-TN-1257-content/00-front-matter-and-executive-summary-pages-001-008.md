# Front matter and executive summary

Source: `DSTO-TN-1257.pdf`, PDF pages 1-8.

Navigation: previous none | [coverage index](README.md) | next [Link 16 and distribution protocols](01-link-16-and-distribution-protocols-pages-009-015.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-1"></a>

## Source PDF page 1

### UNCLASSIFIED

### UNCLASSIFIED

Extending the Wireshark Network Protocol Analyser to Decode Link 16 Tactical Data Link Messages

William Robertson and Peter Ross

Aerospace Division Defence Science and Technology Organisation

### DSTO-TN-1257

### ABSTRACT

This technical note describes the development of a tactical data link message dissector for the Wireshark network protocol analyser.  Link 16 is a United States and North Atlantic Treaty Organization standard for secure real-time exchange of tactical information between warfighting units. Concurrent with military adoption of Link 16 equipment, training simulators are be ing fitted with simulated tactical data links. The extensions made to Wireshark provide simulation engineers with a tool to troubleshoot Link 16 simulations.

### RELEASE LIMITATION

Approved for public release

<a id="source-pdf-page-2"></a>

## Source PDF page 2

### UNCLASSIFIED

### UNCLASSIFIED

Published by

Aerospace Division DSTO  Defence Science and Technology Organisation

### 506 Lorimer St

Fishermans Bend, Victoria 3207   Australia

Telephone: 1300 333 362 Fax:  (03) 9626 7999

© Commonwealth of Australia 2014

### AR-015-847

January 2014

### APPROVED FOR PUBLIC RELEASE

<a id="source-pdf-page-3"></a>

## Source PDF page 3

### UNCLASSIFIED

### UNCLASSIFIED

Extending the Wireshark Network Protocol Analyser to Decode Link 16 Tactical Data Link Messages

Executive Summary

Tactical Data Links (TDLs) enable the m ilitary to exchange tactical information in a precise, efficient and timely manner. They complement, and in many instances substitute, traditional voice-based communication bearers such as VHF radio. Wireshark is an opensource network protocol analyser  that provides a comprehensive filtering and query system, utilities for performing statistical analysis, and dissector modules to decode and analyse protocol content.

This technical note describes modifications to Wireshark enabling it to analyse Link 16 tactical data link messages. A dissector module was written to decode J-series messages communicated using the Simulation Interoperability Standards Organization’s Standard for Link 16 Simulations. This work was completed as a summer vacation student project over a

### 10 week period, using sources from the open literature on Link 16. It has been used to

develop and test distributed mission training simulators.

<a id="source-pdf-page-4"></a>

## Source PDF page 4

### UNCLASSIFIED

### UNCLASSIFIED

This page is intentionally blank

<a id="source-pdf-page-5"></a>

## Source PDF page 5

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

Contents

### 1. INTRODUCTION ............................................................................................................... 1

### 2. LINK 16 ................................................................................................................................. 1

### 2.1 J-series Message Format........................................................................................... 1

### 2.2 Distribution System ................................................................................................. 2

### 3. LINK 11/ 11B ........................................................................................................................ 3

### 3.1 M-series Message Format ........................................................................................ 4

### 3.2 Distribution System ................................................................................................. 4

### 4. WIRESHARK ....................................................................................................................... 5

### 5. REQUIREMENTS ............................................................................................................... 6

### 6. DEVELOPMENT ................................................................................................................. 6

### 6.1 Environment .............................................................................................................. 6

### 6.2 Implementation ......................................................................................................... 6

### 6.3 Testing ......................................................................................................................... 7

### 6.4 Development Observations .................................................................................... 8

### 6.5 Software Patch ........................................................................................................... 8

### 7. CONCLUSION AND FURTHER WORK....................................................................... 8

### 8. REFERENCES ...................................................................................................................... 9

### APPENDIX A: REFERENCE CAPTURE FILE ................................................................ 11

### APPENDIX B: SOFTWARE PATCH................................................................................ 14

<a id="source-pdf-page-6"></a>

## Source PDF page 6

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

This page is intentionally blank

<a id="source-pdf-page-7"></a>

## Source PDF page 7

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

Acronyms

bps Bits per second DIS Distributed Interactive Simulation DTS Data Terminal Set GCCS Global Command and Control System HLA High Level Architecture JREAP Joint Range Extension Application Protocol JTIDS Joint Tactical Information Distribution System LSB Least Significant Bit MSB Most Significant Bit MTC Multi-TADIL Capability NATO North Atlantic Treaty Organization PDU Protocol Data Unit PPLI Precise Participant Location and Identification QPSK Quadrature Phased-Shift Keying RPR-FOM Real-time Platform Reference Federation Object Model SIMPLE Standard Interface for Multiple Platform Link Evaluation STANAG Standardisation Agreement (NATO) TADIL Tactical Digital Information Link TCP Transmission Control Protocol TDL Tactical Data Link TDMA Time Division Multiple Access UDP User Datagram Protocol

<a id="source-pdf-page-8"></a>

## Source PDF page 8

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

This page is intentionally blank

Navigation: previous none | [coverage index](README.md) | next [Link 16 and distribution protocols](01-link-16-and-distribution-protocols-pages-009-015.md)
