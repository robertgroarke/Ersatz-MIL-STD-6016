# Front matter

Source: `AFIT-IP-Over-Link16.pdf`, PDF pages 1-11.

Navigation: previous none | [coverage index](README.md) | next [Introduction and background](01-introduction-and-background-pages-012-034.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-1"></a>

## Source PDF page 1

Air Force Institute of Technology Air Force Institute of Technology AFIT Scholar AFIT Scholar Theses and Dissertations Student Graduate Works 3-2003 Internet Protocol (IP) Over Link-16 Internet Protocol (IP) Over Link-16 Clinton W. Stinson Follow this and additional works at: https://scholar.afit.edu/etd Part of the Computer Engineering Commons Recommended Citation Recommended Citation Stinson, Clinton W., "Internet Protocol (IP) Over Link-16" (2003). Theses and Dissertations. 4196. https://scholar.afit.edu/etd/4196 This Thesis is brought to you for free and open access by the Student Graduate Works at AFIT Scholar. It has been accepted for inclusion in Theses and Dissertations by an authorized administrator of AFIT Scholar. For more information, please contact AFIT.ENWL.Repository@us.af.mil.

<a id="source-pdf-page-2"></a>

## Source PDF page 2

### INTERNET PROTOCOL (IP) OVER LINK-16

### THESIS

Clinton W. Stinson, Captain, USAF

### AFIT/GCE/ENG/03-04

### DEPARTMENT OF THE AIR FORCE

### AIR UNIVERSITY

### AIR FORCE INSTITUTE OF TECHNOLOGY

Wright-Patterson Air Force Base, Ohio

### APPROVED FOR PUBLIC RELEASE; DISTRIBUTION UNLIMITED.

<a id="source-pdf-page-3"></a>

## Source PDF page 3

The views expressed in this thesis are those of the author and do not reflect the official policy or position of the United States Air Force, Department of Defense, or the United States Government.

<a id="source-pdf-page-4"></a>

## Source PDF page 4

### AFIT/GCE/ENG/03-04

### INTERNET PROTOCOL (IP) OVER LINK-16

### THESIS

Presented to the Faculty Department of Electrical and Computer Engineering Graduate School of Engineering and Management Air Force Institute of Technology Air University Air Education and Training Command In Partial Fulfillment of the Requirements for the Degree of Master of Science in Computer Engineering Clinton W. Stinson, B.S. Captain, USAF March 2003

### APPROVED FOR PUBLIC RELEASE; DISTRIBUTION UNLIMITED.

<a id="source-pdf-page-5"></a>

## Source PDF page 5

- AFlT/GCFJENG/O3-04

### INTERNET PROTOCOL (IP) OVER LINK-16

Clinton W. Stinson, B.S. Captain, USAF 1. Approved: .J .-!)-c{;J, .I) I!/. J<- JUC(("'~3~ L~r ~st~ t~~~~~~:===~::::==- date Thesis Advisor n ~ n n .1'2- ""'Ail...Oj -'(::f:::~ ~~g H~~~~=~~~-- date Committee Member r ~ 0 ~ I :L1>1£.t 0'; Dr. Richard A. Raines date Committee Member ---t:1~~~~ : . -~. L J- AQ,... </:; 2L Dr. Michael A emple date Committee Member

<a id="source-pdf-page-6"></a>

## Source PDF page 6

Acknowledgements

I would like to express my sin cere appreciation to my thesis advisor, Major Baldwin, for his guidance and support throughout the course of this thesis effort.  His insight, technical knowledge, and experience were greatly appreciated.  I would also like to recognize my thesis committee members, Dr. Raines, Dr. Gunsch, and Dr. Temple, for their assistance and suggestions throughout this process.  In addition, I would like to thank my sponsor, Mr. Todd Reinhart, from the Air Force Research Lab Sensors Directorate (AFRL/IFTA) for his support provided during this endeavor and to Mrs. Gotfried of Raytheon, who provided timely information concerning the EISA program. 1Lt Dooley, of the AFRL Sensors Directorate (AFRL/IFSD), also provided invaluable assistance to questions that arose concerning the Link-16 OPNET model.

Clinton W. Stinson

<a id="source-pdf-page-7"></a>

## Source PDF page 7

i

### Table of Contents

- `Page`

- `List of Figures...................................................................................................................................... v`
- `List of Tables..................................................................................................................................... vii`
- `Abstract............................................................................................................................................... ix`
- `I. Intr oduction.......................................................................................................................... 1-1`
### 1.1 Back ground .......................................................................................................... 1-1

### 1.2 Goals.................................................................................................................... .1 -3

### 1.3 Document Overview ............................................................................................ 1-4

II. Literatu re Review ................................................................................................................ 2-1

### 2.1 Intr oduction .......................................................................................................... 2-1

### 2.2 Scenario ................................................................................................................ 2 -1

### 2.3 Notional Communica tions Architecture.............................................................. 2-4

### 2.4 Information Assu rance Capabilities .................................................................... 2-6

### 2.4.1 Security Threat s and Countermeasures ............................................ 2-6

### 2.5 Multi-Platform Common Data Link (MP-CDL)................................................. 2-9

### 2.5.1 MP-CDL Main Goals......................................................................2-10

### 2.5.2 MP-CDL Data Rates .......................................................................2-11

### 2.5.3 Standard ization Issues .....................................................................2-12

### 2.6 IPSec/IPv6 ..........................................................................................................2-12

### 2.6.1 Authentication H eader (AH) Protocol ............................................2-14

### 2.6.2 Encapsulating Security  Payload Protocol (ESP) ............................2-15

<a id="source-pdf-page-8"></a>

## Source PDF page 8

ii

### 2.7 Li nk-16 ...............................................................................................................2-16

### 2.7.1 Data Ex change Rates.......................................................................2-17

### 2.7.2 Link-16 Data Security .....................................................................2-19

### 2.8 Common Object Request Br oker Architecture (CORBA) ...............................2-19

### 2.9 Current Research................................................................................................2-20

### 2.9.1 TADIL-J Range Extension (JRE)...................................................2-20

### 2.9.2 ATM Network-Based Integrated Battlespace Simulation With

Multiple UAV-AWACS-Fighter Platforms ...................................2-21

### 2.9.3 IP Mobility Management for the Airborne Communications Node

(ACN) Platform...............................................................................2-22

### 2.9.4 Surveillance and Control Da ta Link Network (SCDLN) for Joint

### STARS.............................................................................................2-23

### 2.10 Summary ............................................................................................................2-24

III. Methodology............................................................................................................... ......... 3-1

### 3.1 Problem Definition............................................................................................... 3-1

### 3.1.1 Goals an d Hypothesis........................................................................ 3-1

### 3.1.2 Approach ........................................................................................... 3-2

### 3.2 System Boundaries............................................................................................... 3-2

### 3.3 System Services ................................................................................................... 3-3

### 3.4 Performance Metrics ............................................................................................3-4

### 3.5 Parameters ............................................................................................................ 3- 5

### 3.5.1 System Parameters ............................................................................3-5

### 3.5.2 Workload  Parameters ........................................................................3-6

<a id="source-pdf-page-9"></a>

## Source PDF page 9

iii

### 3.6 Factors ............................................................................................................ 3-6

### 3.6.1 Da ta Rate ........................................................................................... 3-6

### 3.6.2 Internet Protocol ................................................................................ 3-6

### 3.7 Evaluation Technique .......................................................................................... 3-7

### 3.8 Workload .............................................................................................................. 3-7

### 3.9 Experimental Design............................................................................................ 3-8

### 3.10 Summary .............................................................................................................. 3-8

IV. Implementation and Analysis.............................................................................................. 4- 1

### 4.1 Overview .............................................................................................................. 4-1

### 4.2 Link-16 Verifica tion and Validation ................................................................... 4-1

### 4.2.1 Verificati on Implementation ............................................................. 4-5

### 4.2.2 Sample Size for Determining Mean.................................................. 4-5

### 4.2.3 Verifi cation Results........................................................................... 4-6

### 4.3 JTIDS Baseline..................................................................................................... 4-8

### 4.3.1 Baseline Implementation................................................................... 4-9

### 4.3.2 Baseline Re sults (ETE Delay)........................................................... 4-9

### 4.3.3 Baseline Results (Effective Throughput)........................................4-10

### 4.4 JTIDS Security Feat ure Additions (IPSec) .......................................................4-12

### 4.4.1 Authentication Header (AH) Protocol – ETE Delay......................4-12

### 4.4.2 AH Protocol – Effective Throughput .............................................4-12

<a id="source-pdf-page-10"></a>

## Source PDF page 10

iv

### 4.4.3 ESP Protocol – Ef fective Throughput ...........................................4-14

### 4.4.4 Baseline, AH and ESP – ETE Delay .............................................4-14

### 4.4.5 Baseline, AH and ESP – Effective Throughput .............................4-15

### 4.5 Result Analysis...................................................................................................4-16

### 4.5.1 End-to-End  Delay Analysis ............................................................4-16

### 4.5.2 Effective Th roughput Analysis .......................................................4-17

### 4.5.3 Raw Thro ughput Analysis ..............................................................4-18

### 4.6 Confidence Inte rval Analysis.............................................................................4-19

### 4.7 Summ ary ..........................................................................................................4-19

V. Conclusions and Future Work............................................................................................. 5-1

### 5.1 Overview ............................................................................................................ 5-1

### 5.2 Conclusions .......................................................................................................... 5-1

### 5.3 Contri butions........................................................................................................ 5-2

### 5.4 Future Work ......................................................................................................... 5-2

Appendix A – ETE Delay Allocation of Variation (ANOVA) Worksheet................................... A-1 Appendix B – Effective Throughput ANOVA Worksheet............................................................ B-1 Appendix C – Raw Throughput Charts.......................................................................................... C-1 Appendix D – Sample Size for Determining Mean Calculations.................................................. D-1 Appendix E – Exponential Distribution Matlab File ...................................................................E-1 Bibliography................................................................................................................................ BIB-1 Vita ........................................................................................................................................... VITA-1

<a id="source-pdf-page-11"></a>

## Source PDF page 11

v List of Figures

### Figure Page

### 2.1 A Notional Deployed Joint Ba ttlespace Infosphere (JBI) .................................................. 2-2

### 2.2 Linking the F-15E Airc raft into the JBI.............................................................................. 2-4

### 2.3 AOC Notional Hardware Architecture and JBI Server Gateway Software Arch.............. 2-5

### 2.4 Authentication Header (AH) Format ................................................................................2-14

### 2.5 Encapsulating Security Payload (ESP) Format ................................................................2-16

### 2.6 The Global Archit ecture of CORBA ................................................................................2-20

### 3.1 F-15E JBI Connectivity So ftware Architecture.................................................................. 3-3

### 4.1 Mission Model – Link-16 Communication System ........................................................... 4-2

### 4.2 dls_JTIDS_host Node Model .............................................................................................. 4-3

### 4.3 dls_radio_JTIDS Node Model ............................................................................................ 4-4

### 4.4 Average ETE Delay (2160 Byte  Packet, 3000 Samples) ................................................... 4-7

### 4.5 Baseline End-to-End  (ETE) Delay....................................................................................4-10

### 4.6 Baseline Effec tive Throughput..........................................................................................4-11

### 4.7 Baseline and AH ETE Delay.............................................................................................4-13

### 4.8 Baseline and AH – Ef fective Throughput.........................................................................4-13

### 4.9 Baseline, AH, and ESP ETE Delay...................................................................................4-15

### 4.10 Baseline, AH, and ESP Effective Throughput..................................................................4-16

### 4.11 Baseline, AH, and ESP Raw Throughput .........................................................................4-18

Navigation: previous none | [coverage index](README.md) | next [Introduction and background](01-introduction-and-background-pages-012-034.md)
