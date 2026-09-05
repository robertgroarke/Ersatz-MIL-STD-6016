# Annex B - DIS-HLA translations

Source: `SISO-STD-002-2021.pdf`, PDF pages 69-88.

Navigation: previous [Annex A - FOM module](07-annex-a-fom-module-pages-052-068.md) | [coverage index](README.md) | next [Annex C - Version changes](09-annex-c-version-changes-pages-089-090.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-69"></a>

## Source PDF page 69

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 69 of 90 This is an approved SISO Standard. Annex B DIS to HLA Translations (Informative)

### B.1 RPR FOM RadioTransmitter Object versus DIS Transmitter PDU

See the RPR FOM GRIM [ 2], sections 7.10.1.1 and 9.6.1, for the cross references between the RPR FOM 2.0 RadioTransmitter object class attributes and the DIS Transmitter PDU fields.

### B.2 RPR FOM RadioSignal Based Interactions versus DIS Signal PDU

The RPR FOM defines four interaction classes, one for each of the encoding classes, as subclasses of the common par ent class RadioSignal. Since the encoding class for the Link 16 DIS Signal PDU messages is set to Raw Binary Data, RawBinaryRadioSignal interactions are used in HLA federations based on the RPR FOM. In addition, compliance to the Link 16 FOM module requires the Link 16 messages to be sent using one of the subclasses of the Link16RadioSignal, as per the Link 16 Message Type  Identifier. Table B-1 shows the interaction class to be generated for each of the allowed values of the Message  Type Identifier field [UID 176]. See Table B-3 in the next section for the location of the Message Type Identifier field, bits 40 -

### 47 (octet #5) of the Signal PDU Data field.

### Table B-1: Link 16 Message Type Identifier to HLA Interaction Class Mapping

- `Message Type Identifier`
- `HLA Interaction Class`
- `Description Value`
- `JTIDS Header/Messages  0 JTIDSMessageRadioSignal`
- `RTT A/B 1 RTTABRadioSignal`
- `RTT Reply 2 RTTReplyRadioSignal`
- `JTIDS Voice CVSD 3 JTIDSVoiceCVSDRadioSignal`
- `JTIDS Voice LPC10 4 JTIDSVoiceLPC10RadioSignal`
- `JTIDS Voice LPC12 5 JTIDSVoiceLPC12RadioSignal`
- `JTIDS LET 6 JTIDSLETRadioSignal`
- `VMF 7 VMFRadioSignal`
- `The following sections describe the translations of the DIS Signal PDU fiel ds to the corresponding`
- `interaction class parameters. The first section covers the data common to all Link 16 Message Type`
- `Identifiers. Subsequent sections cover the specifics for each of the eight Message Type  Identifiers, i.e.,`
- `each of the Link16RadioSignal interaction subclasses.`
- `The same tables can be used for the reverse translation from an HLA interaction to a DIS Signal PDU .`
- `Translating from HLA to DIS does not require selection of the appropriate PDU as it will always be to the`
- `Signal PDU. For fields not mapped (N/A), see the requirements from section 4.2.2 and the DIS standard`
- `for the values to be set.`
### B.2.1 Link 16 Common Data

### Table B-2 shows the translations of the DIS Signal PDU field s to the corresponding RPR FOM and Link

### 16 FOM module interaction class parameters common to each of the Link 16 Message Type  Identifiers.

Most of the mapping of the Signal PDU fields to the RawBinaryRadioSignal parameters is as per the RPR FOM standard. The Data field however is not published in the parameter SignalData. Instead, the content of the Data field is to be extracted and published in parameters of the Link 16 FOM module interaction classes.

<a id="source-pdf-page-70"></a>

## Source PDF page 70

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 70 of 90 This is an approved SISO Standard. The first 160 bits of the Data field, the Link 16 Simul ation Network Header, is split into individual parameters of the Link16RadioSignal class. The subsequent Message Type Identifier-specific content of the Data field is covered in the next sections.

### Table B-2: Link 16 Common Signal PDU to HLA Interaction Mapping

- `Signal PDU fields HLA interaction`
- `Size`
- `(bits)  Class Parameter`
### 96 PDU Header N/A

### 48 Radio Reference ID

RawBinaryRadioSignal HostRadioIndex

### 16 Radio Number

### 16 Encoding Scheme Bits 0-13:

TDLMessageCount

### 16 TDL Type  TacticalDataLinkType

### 32 Sample Rate  DataRate

### 16 Data Length  N/A 3

### 16 Samples N/A

160 16 Data Link 16 Simulation Network Header NPG Number Link16RadioSignal NPGNumber

### 8 Net Number NetNumber

### 8 TSEC CVLL TSEC_CVLL

### 8 MSEC CVLL MSEC_CVLL

### 8 Message Type Identifier See section B.2

### 8 SISO-STD-002 Version

Link16RadioSignal SISOSTD002Version

### 8 Link 16 Version Link16Version

### 32 Time Slot ID TimeSlotID

### 64 Perceived Transmit Time PerceivedTransmitTime

≥ 48 Link 16 Message data See sections B.2.2 to B.2.9 0-31 Padding (if needed) Padding in the highest 0-7 bits of the last array element (if needed)

### Table B -3 provides another perspective of the fields of the Link 16 Simulation Network Header in the

- `Signal PDU Data field. The Link 16 Simulation Network Header occupies the first 160 bits, 20 octets, of`
- `the Data field. The lines below the DIS Data display the m apping of these bits/octets to the`





### 3 Data Length is NOT mapped to SignalDataLength as the RawBinaryRadioSignal parameter SignalData

is not used; see section 4.3.7.1. See Table B-10, Table B-12, and Table B-13 for a mapping of the PDU field to the JTIDS voice message interactions.

<a id="source-pdf-page-71"></a>

## Source PDF page 71

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 71 of 90 This is an approved SISO Standard. Link16RadioSignal interaction parameters.  Note that, in accordance with IEEE Std 1278.1™ -2012 [ 4] section 6.1.2, the Data octet ordering is not strictly from right to left, but follows the big  endian scheme. Since also the Link 16 FOM module basic datatypes are defined as big endian, it would be possible for DIS to HLA gateways to perform a datatype agnostic memory or buffer copy. However, care must be taken to check the endianness of future DIS versions or modifications to the RPR FOM basic datatypes in Link 16 parent FOMs.

### Table B-3: Link 16 Simulation Network Header Data

- `Bit # 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0`
- `NPG Number`
- `Bit #`
### 7 6 5 4 3 2 1 0

### 15 14 13 12 11 10 9 8

DIS Data octet #0 Data octet #1 Bit # 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 HLA NPGNumber

Bit # 7 6 5 4 3 2 1 0 Net Number Bit # 23 22 21 20 19 18 17 16 DIS Data octet #2 Bit # 7 6 5 4 3 2 1 0 HLA NetNumber

Bit # 7 6 5 4 3 2 1 0

### TSEC CVLL

Bit # 31 30 29 28 27 26 25 24 DIS Data octet #3 Bit # 7 6 5 4 3 2 1 0

### HLA TSEC_CVLL

Bit # 7 6 5 4 3 2 1 0

### MSEC CVLL

Bit # 39 38 37 36 35 34 33 32 DIS Data octet #4 Bit # 7 6 5 4 3 2 1 0

### HLA MSEC_CVLL

Bit # 7 6 5 4 3 2 1 0 Message Type Identifier Bit # 47 46 45 44 43 42 41 40 DIS Data octet #5 Bit #

### HLA

<a id="source-pdf-page-72"></a>

## Source PDF page 72

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 72 of 90 This is an approved SISO Standard. Bit # 7 6 5 4 3 2 1 0 SISO-STD-002 Version Bit # 55 54 53 52 51 50 49 48 DIS Data octet #6 Bit # 7 6 5 4 3 2 1 0 HLA SISOSTD002Version

Bit # 7 6 5 4 3 2 1 0 Link 16 Version Bit # 63 62 61 60 59 58 57 56 DIS Data octet #7 Bit # 7 6 5 4 3 2 1 0 HLA Link16Version

Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 Time Slot ID Bit #

### 71 70 69 68 67 66 65 64

### 79 78 77 76 75 74 73 72

### 87 86 85 84 83 82 81 80

### 95 94 93 92 91 90 89 88

DIS Data octet #8 Data octet #9 Data octet #10 Data octet #11 Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 HLA TimeSlotID

Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 Perceived Transmit Time - Integer Part Bit #

### 103 102 101 100 99 98 97 96

### 111 110 109 108 107 106 105 104

### 119 118 117 116 115 114 113 112

### 127 126 125 124 123 122 121 120

DIS Data octet #12 Data octet #13 Data octet #14 Data octet #15 Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 HLA PerceivedTransmitTime.Seconds

Bit # 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 Perceived Transmit Time - Fraction Part Bit #

### 135 134 133 132 131 130 129 128

### 143 142 141 140 139 138 137 136

### 151 150 149 148 147 146 145 144

### 159 158 157 156 155 154 153 152

DIS Data octet #16 Data octet #17 Data octet #18 Data octet #19 Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 HLA PerceivedTransmitTime.Fraction

### B.2.2 JTIDS Header/Messages

### Table B-4 shows the translations of the remainder of the DIS Signal PDU Data field to the corresponding

- `Link 16 FOM module interaction class parameters for the Message Type Identifier JTIDS`
- `Header/Messages. The Link 16 FOM module splits the Link 16 Message data across two parameters of`
- `the JTIDSMessageRadioSignal class: JTIDSHeader and TADILJMessage.`

<a id="source-pdf-page-73"></a>

## Source PDF page 73

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 73 of 90 This is an approved SISO Standard. Note that  Table B -4 provides a generic example of a JTIDS Header/Message. The J -Words that may follow the first  J-Message Initial Word, be they an Extension Word, a Continuation Word, or a next J - Message starting with an Initial Word, are specified in the Link 16 standards [ 7, 8]. The example shows that following the Link 16 Header Word (padded to 48 bits), the Data field contains one or more J -Words (padded to 80 bits).

### Table B-4: JTIDS Header/Messages to JTIDSMessageRadioSignal Mapping

- `Signal PDU fields HLA interaction`
- `Size`
- `(bits)  Class Parameter`
- `160`
- `Data`
- `Link 16 Simulation Network Header See section B.2.1`
- `48`
- `3`
- `Link 16 Message data`
- `Link 16 Header`
- `Word`
- `Time Slot Type`
- `JTIDSMessageRadioSignal`
- `JTIDSHeader`
### 1 Relay Transmission

Indicator

### 15 Source Track Number

of Sender

### 16 Secure Data Unit

Serial Number

### 13 Padding

80 2 1st J-Message, Initial Word Word Format TADILJMessage

### 5 Label, J-Series

### 3 Sublabel, J-Series

### 3 Message Length

Indicator

### 57 Information fields

### 5 Parity

### 5 Padding

80 2 1st J-Message, Extension Word Word Format

### 68 Information fields

### 5 Parity

### 5 Padding

80 2 1st J-Message, Continuation Word Word Format

### 5 Continuation Word

Label

### 63 Information fields

### 5 Parity

### 5 Padding

80 2 2nd J-Message, Initial Word Word Format

### 5 Label, J-Series

### 3 Sublabel, J-Series

<a id="source-pdf-page-74"></a>

## Source PDF page 74

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 74 of 90 This is an approved SISO Standard. Signal PDU fields HLA interaction Size (bits)  Class Parameter

### 3 Message Length

Indicator

### 57 Information fields

### 5 Parity

### 5 Padding

… … 80

### 75 Nth J-Message

### 5 Data Field Padding

0/16 Signal PDU Padding (if needed) N/A

### Table B-5 provides another perspective of the fields of the Link 16 Message data for the Message Type

- `Identifier JTIDS Heade r/Messages in the Signal PDU Data field. Table B -5 illustrates the mapping`
- `between the content of the real Link 16 data, the DIS Signal PDU Data field, and the equivalent HLA`
- `interaction parameters. The same generic example as in  Table B-4 is used, up to the 4th J -Word (2nd J-`
- `Message, Initial Word). As the Link 16 Message data follows the Link 16 Simulation Network Header, the`
- `Signal PDU Data starts at Bit #160 (Data octet #20). The lines below the DIS Data display the mapping of`
- `these bits/octets to the array elements of the JTIDSMessageRadioSignal interaction parameters. The first`
### 6 octets of the Link 16 Message data (Signal PDU Data octets #20 -25) are to be published in the

JTIDSHeader para meter, a fixed array of 6 octets. Each of the subsequent J -Words, each 80 bits, 10 octets, in size, is to be published as an element of the TADILJMessage parameter. As each element of the TADILJMessage dynamic array is a fixed array of 10 octets, the resul t is a two-dimensional array with the first index indicating the J -Word number and the second index indicating the octet within the J - Message.

### Table B-5: Link 16 Message Data for JTIDS Header/Messages

- `Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0`
- `Secure Data Unit Serial Number (SDUSN) Source Track Number of Sender`
- `RTI Time Slot`
- `Type`
- `Bit # 191 190 189 188 187 186 185 184 183 182 181 180 179 178 177 176 175 174 173 172 171 170 169 168 167 166 165 164 163 162 161 160`
- `DIS Data octet #23 Data octet #22 Data octet #21 Data octet #20`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA JTIDSHeader[3] JTIDSHeader[2] JTIDSHeader[1] JTIDSHeader[0]`

- `Bit # 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0              34 33 32`
- `Inform.`
- `fields`
- `Message`
- `Length`
- `Indicator`
- `Sublabel,`
- `J-Series Label, J-Series Word`
- `Format Padding SDUSN`
- `(cont’d)`
- `Bit # 223 222 221 220 219 218 217 216 215 214 213 212 211 210 209 208 207 206 205 204 203 202 201 200 199 198 197 196 195 194 193 192`
- `DIS Data octet #27 Data octet #26 Data octet #25 Data octet #24`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA TADILJMessage[0][1] TADILJMessage[0][0] JTIDSHeader[5] JTIDSHeader[4]`

<a id="source-pdf-page-75"></a>

## Source PDF page 75

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 75 of 90 This is an approved SISO Standard. Bit # 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 Information fields (cont’d) Bit # 255 254 253 252 251 250 249 248 247 246 245 244 243 242 241 240 239 238 237 236 235 234 233 232 231 230 229 228 227 226 225 224 DIS Data octet #31 Data octet #30 Data octet #29 Data octet #28 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[0][5] TADILJMessage[0][4] TADILJMessage[0][3] TADILJMessage[0][2]

Bit #      74 73 72 71 70 69 68 67 66 65 64 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 Padding Parity Information fields (cont’d) Bit # 287 286 285 284 283 282 281 280 279 278 277 276 275 274 273 272 271 270 269 268 267 266 265 264 263 262 261 260 259 258 257 256 DIS Data octet #35 Data octet #34 Data octet #33 Data octet #32 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[0][9] TADILJMessage[0][8] TADILJMessage[0][7] TADILJMessage[0][6]

Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 Information fields Word Format Bit # 319 318 317 316 315 314 313 312 311 310 309 308 307 306 305 304 303 302 301 300 299 298 297 296 295 294 293 292 291 290 289 288 DIS Data octet #39 Data octet #38 Data octet #37 Data octet #36 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[1][3] TADILJMessage[1][2] TADILJMessage[1][1] TADILJMessage[1][0]

Bit # 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 Information fields (cont’d) Bit # 351 350 349 348 347 346 345 344 343 342 341 340 339 338 337 336 335 334 333 332 331 330 329 328 327 326 325 324 323 322 321 320 DIS Data octet #43 Data octet #42 Data octet #41 Data octet #40 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[1][7] TADILJMessage[1][6] TADILJMessage[1][5] TADILJMessage[1][4]

Bit # 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0      74 73 72 71 70 69 68 67 66 65 64 Information fields Continuation Word Label Word Format Padding Parity Information fields (cont’d) Bit # 383 382 381 380 379 378 377 376 375 374 373 372 371 370 369 368 367 366 365 364 363 362 361 360 359 358 357 356 355 354 353 352 DIS Data octet #47 Data octet #46 Data octet #45 Data octet #44 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[2][1] TADILJMessage[2][0] TADILJMessage[1][9] TADILJMessage[1][8]

Bit # 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 Information fields (cont’d) Bit # 415 414 413 412 411 410 409 408 407 406 405 404 403 402 401 400 399 398 397 396 395 394 393 392 391 390 389 388 387 386 385 384 DIS Data octet #51 Data octet #50 Data octet #49 Data octet #48 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[2][5] TADILJMessage[2][4] TADILJMessage[2][3] TADILJMessage[2][2]

<a id="source-pdf-page-76"></a>

## Source PDF page 76

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 76 of 90 This is an approved SISO Standard. Bit #      74 73 72 71 70 69 68 67 66 65 64 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 Padding Parity Information fields (cont’d) Bit # 447 446 445 444 443 442 441 440 439 438 437 436 435 434 433 432 431 430 429 428 427 426 425 424 423 422 421 420 419 418 417 416 DIS Data octet #55 Data octet #54 Data octet #53 Data octet #52 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[2][9] TADILJMessage[2][8] TADILJMessage[2][7] TADILJMessage[2][6]

Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 Information fields Message Length Indicator Sublabel, J-Series Label, J-Series Word Format Bit # 479 478 477 476 475 474 473 472 471 470 469 468 467 466 465 464 463 462 461 460 459 458 457 456 455 454 453 452 451 450 449 448 DIS Data octet #59 Data octet #58 Data octet #57 Data octet #56 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[3][3] TADILJMessage[3][2] TADILJMessage[3][1] TADILJMessage[3][0]

Bit # 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 Information fields (cont’d) Bit # 511 510 509 508 507 506 505 504 503 502 501 500 499 498 497 496 495 494 493 492 491 490 489 488 487 486 485 484 483 482 481 480 DIS Data octet #63 Data octet #62 Data octet #61 Data octet #60 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[3][7] TADILJMessage[3][6] TADILJMessage[3][5] TADILJMessage[3][4]

Bit #       74 73 72 71 70 69 68 67 66 65 64 Padding Parity Information fields (cont’d) Bit #                 527 526 525 524 523 522 521 520 519 518 517 516 515 514 513 512 DIS Padding Data octet #65 Data octet #64 Bit #  7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA  TADILJMessage[3][9] TADILJMessage[3][8]

### B.2.3 RTT A/B

### Table B-6 shows the translations of the remainder of the DIS Signal PDU Data field to the corresponding

- `Link 16 FOM module interaction class parameters for the Message Type Identifier RTT A/B. In the Link 16`
- `FOM module the data is captured in the RTTABRadioSignal parameter RTTAB.`

<a id="source-pdf-page-77"></a>

## Source PDF page 77

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 77 of 90 This is an approved SISO Standard.

### Table B-6: RTT A/B to RTTABRadioSignal Mapping

### Table B-7 provides another perspective of the fields of the Link 16 Message data for the Message Type

- `Identifier RTT A/B in the Signal PDU Data field.`
- `As the Link 16 Message data follows the Link 16 Simulation Network Header, the Signal PDU Data starts`
- `at Bit #160 (Data octet #20). The lines below the DIS Data display the mapping of these bits/octets to the`
- `array elements of the RTTABRadioSignal interaction parameter RTTAB.`
### Table B-7: Link 16 Message Data for RTT A/B

- `Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0`
- `Secure Data Unit Serial Number (SDUSN) RTT A/B specific content`
- `RTI Time Slot`
- `Type`
- `Bit # 191 190 189 188 187 186 185 184 183 182 181 180 179 178 177 176 175 174 173 172 171 170 169 168 167 166 165 164 163 162 161 160`
- `DIS Data octet #23 Data octet #22 Data octet #21 Data octet #20`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
### HLA RTTAB[3] RTTAB[2] RTTAB[1] RTTAB[0]

Bit #               34 33 32 Padding SDUSN (cont’d) Bit #                 207 206 205 204 203 202 201 200 199 198 197 196 195 194 193 192 DIS Padding Data octet #25 Data octet #24 Bit #  7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0

### HLA  RTTAB[5] RTTAB[4]

### B.2.4 RTT Reply

### Table B-8 shows the translations of the remainder of the DIS Signal PDU Data field to the corresponding

- `Link 16 FOM module interaction class parameters for the Message Type Identifier RTT Reply. In the Link`
### 16 FOM module the data is captured in the RTTReplyRadioSignal parameter RTTReply.

Signal PDU fields HLA interaction Size (bits)  Class Parameter 160 Data Link 16 Simulation Network Header See section B.2.1 48 3 Link 16 Message data

### RTT A/B

Time Slot Type RTTABRadioSignal RTTAB

### 1 RTT Interrogation

Type

### 15 RTT A/B specific

content

### 16 Secure Data Unit

Serial Number

### 13 Padding

### 16 Padding N/A

<a id="source-pdf-page-78"></a>

## Source PDF page 78

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 78 of 90 This is an approved SISO Standard.

### Table B-8: RTT Reply to RTTReplyRadioSignal Mapping

### Table B-9 provides another perspective of the fields of the Link 16 Message data for the Message Type

- `Identifier RTT Reply in the Signal PDU Data field. As the Link 16 Message data fo llows the Link 16`
- `Simulation Network Header, the Signal PDU Data starts at Bit #160 (Data octet #20). The lines below the`
- `DIS Data display the mapping of these bits/octets to the array elements of the RTTReplyRadioSignal`
- `interaction parameter RTTReply.`
### Table B-9: Link 16 Message Data for RTT Reply

- `Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0`
- `Secure Data Unit Serial Number (SDUSN) Time of Arrival`
- `Bit # 191 190 189 188 187 186 185 184 183 182 181 180 179 178 177 176 175 174 173 172 171 170 169 168 167 166 165 164 163 162 161 160`
- `DIS Data octet #23 Data octet #22 Data octet #21 Data octet #20`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA RTTReply[3] RTTReply[2] RTTReply[1] RTTReply[0]`

- `Bit #               34 33 32`
- `Padding SDUSN`
- `(cont’d)`
- `Bit #                 207 206 205 204 203 202 201 200 199 198 197 196 195 194 193 192`
- `DIS Padding Data octet #25 Data octet #24`
- `Bit #  7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA  RTTReply[5] RTTReply[4]`
### B.2.5 JTIDS Voice CVSD

### Table B-10 shows the translations of the field Data Length and remainder of the DIS Signal PDU Data

- `field to the corresponding Link 16 FOM module interaction class parameters for the Message Type`
- `Identifier JTIDS Voice CVSD. The Link 16 FOM module splits the Link 16 Message data across two`
- `parameters of the JTIDSVoiceCVSDRadioSignal class: JTIDSHeader and Data.`
- `Signal PDU fields HLA interaction`
- `Size`
- `(bits)  Class Parameter`
- `160`
- `Data`
- `Link 16 Simulation Network Header See section B.2.1`
- `48`
- `19`
- `Link 16`
- `Message data`
- `RTT Reply`
- `Time of Arrival`
- `RTTReplyRadioSignal RTTReply 16 Secure Data Unit`
- `Serial Number`
### 13 Padding

### 16 Padding N/A

<a id="source-pdf-page-79"></a>

## Source PDF page 79

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 79 of 90 This is an approved SISO Standard.

### Table B-10: JTIDS Voice CVSD to JTIDSVoiceCVSDRadioSignal Mapping

### Table B-11 provides another perspective of the fields of the Link 16 Message data for the JT IDS Voice

- `Message Type Identifiers in the Signal PDU Data field. As the Link 16 Message data follows the Link 16`
- `Simulation Network Header, the Signal PDU Data starts at Bit #160 (Data octet #20). The lines below the`
- `DIS Data display the mapping of these b its/octets to the array elements of the interaction class`
- `parameters. The first 6 octets of the Link 16 Message data (Signal PDU Data octets #20 -25) are to be`
- `published in the JTIDSHeader parameter, a fixed array of 6 octets. The encoded voice data that fo llows is`
- `to be published in Data parameter, a dynamic array of at least 29 octets. The table shows an example of`
- `a minimum sized message, with only 225 bits of JTIDS Free Text Voice Data (but omitting a large center`
- `portion of it).`





### 4 Note that the HLA parameter DataLength contains the length (in bits) of  the encoded voice in the HLA

Data parameter, whereas the PDU field Data Length contains the number of bits of the entire PDU Data field. Therefore, the value from the PDU field Data Length cannot be copied directly  into the parameter DataLength. The difference is 208 bits, 160 bits for the Link 16 Simulation Network Header and 48 bits for the Link 16 Header Word. Signal PDU fields HLA interaction Size (bits)  Class Parameter …

### 16 Data Length JTIDSVoiceCVSD

RadioSignal DataLength 4 …

160 Data Link 16 Simulation Network Header See section B.2.1 48 3 Link 16 Message data Link 16 Header Word Time Slot Type JTIDSVoiceCVSDRadioSignal JTIDSHeader

### 1 Relay Transmission

Indicator

### 15 Source Track Number

of Sender

### 16 Secure Data Unit

Serial Number

### 13 Padding

### 225 -

1860 JTIDS Free Text Voice Data CVSD Encoded Voice Data Data 0-31 Padding (if needed) Padding in the highest 0-7 bits (if needed)

<a id="source-pdf-page-80"></a>

## Source PDF page 80

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 80 of 90 This is an approved SISO Standard.

### Table B-11: Link 16 Message Data for JTIDS Voice

- `Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0`
- `Secure Data Unit Serial Number (SDUSN) Source Track Number of Sender`
- `RTI Time Slot`
- `Type`
- `Bit # 191 190 189 188 187 186 185 184 183 182 181 180 179 178 177 176 175 174 173 172 171 170 169 168 167 166 165 164 163 162 161 160`
- `DIS Data octet #23 Data octet #22 Data octet #21 Data octet #20`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA JTIDSHeader[3] JTIDSHeader[2] JTIDSHeader[1] JTIDSHeader[0]`

- `Bit # 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0              34 33 32`
- `JTIDS Free Text Voice Data Padding SDUSN`
- `(cont’d)`
- `Bit # 223 222 221 220 219 218 217 216 215 214 213 212 211 210 209 208 207 206 205 204 203 202 201 200 199 198 197 196 195 194 193 192`
- `DIS Data octet #27 Data octet #26 Data octet #25 Data octet #24`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA Data[1] Data[0] JTIDSHeader[5] JTIDSHeader[4]`

- `Bit # 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16`
- `JTIDS Free Text Voice Data`
- `Bit # 255 254 253 252 251 250 249 248 247 246 245 244 243 242 241 240 239 238 237 236 235 234 233 232 231 230 229 228 227 226 225 224`
- `DIS Data octet #31 Data octet #30 Data octet #29 Data octet #28`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA Data[5] Data[4] Data[3] Data[2]`

- `Bit #`
- `JTIDS Free Text Voice Data`
- `Bit #`
- `DIS Data octet #... Data octet #... Data octet #... Data octet #...`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA Data[…] Data[…] Data[…] Data[…]`

- `Bit #  224 223 222 221 220 219 218 217 216 215 214 213 212 211 210 209 208`
- `JTIDS Free Text Voice Data`
- `Bit #                432 431 430 429 428 427 426 425 424 423 422 421 420 419 418 417 416`
- `DIS Padding D Data octet #53 Data octet #52`
- `Bit #  7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
### HLA

Data[28] Data[27] Data[26] Padding

### B.2.6 JTIDS Voice LPC10

### Table B-12 shows the translations field Data L ength and of the remainder of the DIS Signal PDU Data

- `field to the corresponding Link 16 FOM module interaction class parameters for the Message Type`
- `Identifier JTIDS Voice LPC10. The Link 16 FOM module splits the Link 16 Message data across two`
- `parameters of the JTIDSVoiceLPC10RadioSignal class: JTIDSHeader and Data.`

<a id="source-pdf-page-81"></a>

## Source PDF page 81

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 81 of 90 This is an approved SISO Standard.

### Table B-12: JTIDS Voice LPC10 to JTIDSVoiceLPC10RadioSignal Mapping

- `The three different JTIDS Voice Message Type  Identifiers only differ in the encoding used for the voice.`
- `See section B.2.5, Table B -11 for the bit mapping perspective that also applies to the Message Type`
- `Identifier JTIDS Voice LPC10.`
### B.2.7 JTIDS Voice LPC12

### Table B-13 shows the translations field Data Length and of the remainder of the DIS Signal PDU Data

- `field to the corresponding Link 16 FOM module interaction class parameters for the Messa ge Type`
- `Identifier JTIDS Voice LPC12. The Link 16 FOM module splits the Link 16 Message data across two`
- `parameters of the JTIDSVoiceLPC12RadioSignal class: JTIDSHeader and Data.`





### 5 Note that the HLA parameter DataLength contains the length (in bits) of the encoded voice in the HLA

Data parameter, whereas the PDU field Data  Length contains the number of bits of the entire PDU Data field. Therefore, the value from the PDU field Data Length cannot be copied directly into the parameter DataLength. The difference is 208 bits, 160 bits for the Link 16 Simulation Network Header an d 48 bits for the Link 16 Header Word. Signal PDU fields HLA interaction Size (bits)  Class Parameter …

### 16 Data Length JTIDSVoiceLPC10

Radio Signal DataLength 5 …

160 Data Link 16 Simulation Network Header See section B.2.1 48 3 Link 16 Message data Link 16 Header Word Time Slot Type JTIDSVoiceLPC10RadioSignal JTIDSHeader

### 1 Relay Transmission

Indicator

### 15 Source Track Number

of Sender

### 16 Secure Data Unit

Serial Number

### 13 Padding

### 225 -

1860 JTIDS Free Text Voice Data LPC10 Encoded Voice Data Data 0-31 Padding (if needed) Padding in the highest 0-7 bits (if needed)

<a id="source-pdf-page-82"></a>

## Source PDF page 82

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 82 of 90 This is an approved SISO Standard.

### Table B-13: JTIDS Voice LPC12 to JTIDSVoiceLPC12RadioSignal Mapping

- `The three different JTIDS Voice Message Type  Identifiers only differ in the encoding used for the voice.`
- `See section B.2.5, Table B -11 for the bit mapping perspective that also applies to the Message Type`
- `Identifier JTIDS Voice LPC12.`
### B.2.8 JTIDS LET

### Table B-14 shows the translations of the remainder of the DIS Signal PDU Data fiel d to the corresponding

- `Link 16 FOM module interaction class parameters for the Message Type Identifier JTIDS LET. The Link`
### 16 FOM module splits the Link 16 Message data across two parameters of the JTIDSLETRadioSignal

class: LETHeader and TADILJMessage. Note that Table B-14 provides an example of a JTIDS LET message with just one J -Word. See section

### B.2.2 for an example with more J-Words following the first J-Message Initial Word.

### 6 Note that the HLA parameter DataLength contains the length (in bits) of the encoded voice in the HLA

Data parameter, whereas the PDU field Data Length contains the number of bits of the entire PDU Data field. Therefore, the value from the PDU field Data Length cannot be copied directly into the parameter DataLength. The difference is 208 bits, 160 bits for the Link 16 Simulation Network Header and 48 bits for the Link 16 Header Word. Signal PDU fields HLA interaction Size (bits)  Class Parameter …

### 16 Data Length JTIDSVoiceLPC12

RadioSignal DataLength 6 …

160 Data Link 16 Simulation Network Header See section B.2.1 48 3 Link 16 Message data Link 16 Header Word Time Slot Type JTIDSVoiceLPC12RadioSignal JTIDSHeader

### 1 Relay Transmission

Indicator

### 15 Source Track Number

of Sender

### 16 Secure Data Unit

Serial Number

### 13 Padding

### 225 -

1860 JTIDS Free Text Voice Data LPC12 Encoded Voice Data Data 0-31 Padding (if needed) Padding in the highest 0-7 bits (if needed)

<a id="source-pdf-page-83"></a>

## Source PDF page 83

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 83 of 90 This is an approved SISO Standard.

### Table B-14: JTIDS LET to JTIDSLETRadioSignal Mapping

- `Signal PDU fields HLA interaction`
- `Size`
- `(bits)  Class Parameter`
- `160`
- `Data`
- `Link 16 Simulation Network Header See section B.2.1`
- `48`
- `4`
- `Link 16 Message data`
- `LET Header`
- `Word`
- `LET ID Symbol`
- `JTIDSLETRadioSignal`
- `LETHeader`
### 1 Relay Transmission

Indicator

### 4 LET Message

Packing Type

### 15 Source Track Number

of Sender

### 16 Secure Data Unit

Serial Number

### 8 Padding

80 2 1st J-Message, Initial Word Word Format TADILJMessage

### 5 Label, J-Series

### 3 Sublabel, J-Series

### 3 Message Length

Indicator

### 57 Information fields

### 5 Parity

### 5 Padding

… … 80

### 75 Nth J-Message

### 5 Padding

0/16 Padding (if needed) N/A

### Table B-15 provides another perspective of the fields of the Link 16 Message data for the Message Type

- `Identifier JTIDS LET in the Signal PDU Data field. Just as in  Table B-14, only one J -Word is included. As`
- `the Link 16 Message data follows the Link 16 Simulation Network Header, the Signal PDU Data starts at`
- `Bit #160 (Data octet # 20). The lines below the DIS Data display the mapping of these bits/octets to the`
- `array elements of the JTIDSLETRadioSignal interaction par ameters. The first 6 octets of the Link 16`
- `Message data (Signal PDU Data octets #20 -25) are to be published in the LETHeader parameter, a fixed`
- `array of 6 octets. Each of the subsequent J -Words, each 80 bits, 10 octets, in size, is to be published as`
- `an element of the TADILJMessage parameter. As each element of the TADILJMessage dynamic array is`
- `a fixed array of 10 octets, the result is a two -dimensional array with the first index indicating the J -Word`
- `number and the second index indicating the octet within  the J-Message. See Table B-5 for an example`
- `with multiple J-Words.`

<a id="source-pdf-page-84"></a>

## Source PDF page 84

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 84 of 90 This is an approved SISO Standard.

### Table B-15: Link 16 Message Data for JTIDS LET

- `Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0`
- `Secure Data Unit Serial`
- `Number Source Track Number of Sender LET Message`
- `Packing Type`
### RTI LET ID

Symbol Bit # 191 190 189 188 187 186 185 184 183 182 181 180 179 178 177 176 175 174 173 172 171 170 169 168 167 166 165 164 163 162 161 160 DIS Data octet #23 Data octet #22 Data octet #21 Data octet #20 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA LETHeader[3] LETHeader[2] LETHeader[1] LETHeader[0]

Bit # 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0         39 38 37 36 35 34 33 32 Inform. fields Message Length Indicator Sublabel, J-Series Label, J-Series Word Format Padding Secure Data Unit Serial Number (cont’d) Bit # 223 222 221 220 219 218 217 216 215 214 213 212 211 210 209 208 207 206 205 204 203 202 201 200 199 198 197 196 195 194 193 192 DIS Data octet #27 Data octet #26 Data octet #25 Data octet #24 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[0][1] TADILJMessage[0][0] LETHeader[5] LETHeader[4]

Bit # 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 Information fields (cont’d) Bit # 255 254 253 252 251 250 249 248 247 246 245 244 243 242 241 240 239 238 237 236 235 234 233 232 231 230 229 228 227 226 225 224 DIS Data octet #31 Data octet #30 Data octet #29 Data octet #28 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[0][5] TADILJMessage[0][4] TADILJMessage[0][3] TADILJMessage[0][2]

Bit #      74 73 72 71 70 69 68 67 66 65 64 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 Padding Parity Information fields (cont’d) Bit # 287 286 285 284 283 282 281 280 279 278 277 276 275 274 273 272 271 270 269 268 267 266 265 264 263 262 261 260 259 258 257 256 DIS Data octet #35 Data octet #34 Data octet #33 Data octet #32 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA TADILJMessage[0][9] TADILJMessage[0][8] TADILJMessage[0][7] TADILJMessage[0][6]

### B.2.9 VMF

### Table B-16 shows the translations of the remainder of the DIS Signal PDU Data field to the corresponding

- `Link 16 FOM module interaction class parameters for the Message Type Identifier VMF. The Link 16 FOM`
- `module splits the Link 16 Message data across two parameters of the VMFRadioSignal class :`
- `JTIDSHeader and MessageData.`
- `Note that Table B -16 provides a generic example for VMF messages. As the payload of the VMF`
- `messages is not part of the Link 16 standard, one or more VMF messages may be needed to constitute`
- `one complete message in the payload protocol. Similarly, it may be that (parts of) multiple messages in`
- `the payload protocol are present within one VMF message (not sho wn in the example). The example`
- `shows that following the Link 16 Header Word (padded to 48 bits), the Data field contains one or more`
- `Link 16 words containing the VMF message data (padded to 80 bits).`

<a id="source-pdf-page-85"></a>

## Source PDF page 85

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 85 of 90 This is an approved SISO Standard.

### Table B-16: VMF to VMFRadioSignal Mapping

- `Signal PDU fields HLA interaction`
- `Size`
- `(bits)  Class Parameter`
- `160`
- `Data`
- `Link 16 Simulation Network Header See section B.2.1`
- `48`
- `3`
- `Link 16 Message data`
- `Link 16 Header`
- `Word`
- `Time Slot Type`
- `VMFRadioSignal`
- `JTIDSHeader`
### 1 Relay Transmission

Indicator

### 15 Source Track Number

of Sender

### 16 Secure Data Unit

Serial Number

### 13 Padding

80 2 1st Word Word Format MessageData

### 68 VMF information fields

### 5 Parity

### 5 Padding

80 2 2nd Word Word Format

### 68 VMF information fields

### 5 Parity

### 5 Padding

80 2 3rd Word Word Format

### 68 VMF information fields

### 5 Parity

### 5 Padding

80 2 4th Word Word Format

### 68 VMF information fields

### 5 Parity

### 5 Padding

… … 80

### 75 Nth Word

### 5 Padding

0/16 Padding (if needed) N/A

<a id="source-pdf-page-86"></a>

## Source PDF page 86

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 86 of 90 This is an approved SISO Standard.

### Table B-17 provides another perspective of the fields of the Link 16 Message data for the Message Type

- `Identifier VMF in the Signal PDU  Data field. The same generic example as in  Table B-16 is used, up to`
- `the 4th Link 16 word . As the Link 16 Message data follows the Link 16 Simulation Network Header, the`
- `Signal PDU Data starts at Bit #160 (Data octet #20). The lines below the DIS Data display the mapping of`
- `these bits/octets to the array elements of the VMFRadioSignal interaction parameters. The first 6 octets of`
- `the Link 16 Message data (Signal PDU Data octets #20 -25) are to be published in the JTIDSHeader`
- `parameter, a fixed array of 6 octets. Each of the subsequent Link 16 words , each 80 bits, 10 octets, in`
- `size, is to be published as an element of the MessageData parameter. As each element of the`
- `MessageData dynamic array is a fixed array of 10 octets, the result  is a two -dimensional array with the`
- `first index indicating the Link 16 word number and the second index indicating the octet within the Link 16`
- `word.`
### Table B-17: Link 16 Message Data for VMF

- `Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0`
- `Secure Data Unit Serial Number (SDUSN) Source Track Number of Sender`
- `RTI Time Slot`
- `Type`
- `Bit # 191 190 189 188 187 186 185 184 183 182 181 180 179 178 177 176 175 174 173 172 171 170 169 168 167 166 165 164 163 162 161 160`
- `DIS Data octet #23 Data octet #22 Data octet #21 Data octet #20`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA JTIDSHeader[3] JTIDSHeader[2] JTIDSHeader[1] JTIDSHeader[0]`

- `Bit # 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0              34 33 32`
- `VMF information fields Word`
- `Format Padding SDUSN`
- `(cont’d)`
- `Bit # 223 222 221 220 219 218 217 216 215 214 213 212 211 210 209 208 207 206 205 204 203 202 201 200 199 198 197 196 195 194 193 192`
- `DIS Data octet #27 Data octet #26 Data octet #25 Data octet #24`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA MessageData[0][1] MessageData[0][0] JTIDSHeader[5] JTIDSHeader[4]`

- `Bit # 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16`
- `VMF information fields (cont’d)`
- `Bit # 255 254 253 252 251 250 249 248 247 246 245 244 243 242 241 240 239 238 237 236 235 234 233 232 231 230 229 228 227 226 225 224`
- `DIS Data octet #31 Data octet #30 Data octet #29 Data octet #28`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA MessageData[0][5] MessageData[0][4] MessageData[0][3] MessageData[0][2]`

- `Bit #      74 73 72 71 70 69 68 67 66 65 64 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48`
- `Padding Parity VMF information fields (cont’d)`
- `Bit # 287 286 285 284 283 282 281 280 279 278 277 276 275 274 273 272 271 270 269 268 267 266 265 264 263 262 261 260 259 258 257 256`
- `DIS Data octet #35 Data octet #34 Data octet #33 Data octet #32`
- `Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0`
- `HLA MessageData[0][9] MessageData[0][8] MessageData[0][7] MessageData[0][6]`

<a id="source-pdf-page-87"></a>

## Source PDF page 87

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 87 of 90 This is an approved SISO Standard. Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 VMF information fields Word Format Bit # 319 318 317 316 315 314 313 312 311 310 309 308 307 306 305 304 303 302 301 300 299 298 297 296 295 294 293 292 291 290 289 288 DIS Data octet #39 Data octet #38 Data octet #37 Data octet #36 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA MessageData[1][3] MessageData[1][2] MessageData[1][1] MessageData[1][0]

Bit # 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 VMF information fields (cont’d) Bit # 351 350 349 348 347 346 345 344 343 342 341 340 339 338 337 336 335 334 333 332 331 330 329 328 327 326 325 324 323 322 321 320 DIS Data octet #43 Data octet #42 Data octet #41 Data octet #40 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA MessageData[1][7] MessageData[1][6] MessageData[1][5] MessageData[1][4]

Bit # 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0      74 73 72 71 70 69 68 67 66 65 64 VMF information fields Word Format Padding Parity VMF information fields (cont’d) Bit # 383 382 381 380 379 378 377 376 375 374 373 372 371 370 369 368 367 366 365 364 363 362 361 360 359 358 357 356 355 354 353 352 DIS Data octet #47 Data octet #46 Data octet #45 Data octet #44 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA MessageData[2][1] MessageData[2][0] MessageData[1][9] MessageData[1][8]

Bit # 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 VMF information fields (cont’d) Bit # 415 414 413 412 411 410 409 408 407 406 405 404 403 402 401 400 399 398 397 396 395 394 393 392 391 390 389 388 387 386 385 384 DIS Data octet #51 Data octet #50 Data octet #49 Data octet #48 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA MessageData[2][5] MessageData[2][4] MessageData[2][3] MessageData[2][2]

Bit #      74 73 72 71 70 69 68 67 66 65 64 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 Padding Parity VMF information fields (cont’d) Bit # 447 446 445 444 443 442 441 440 439 438 437 436 435 434 433 432 431 430 429 428 427 426 425 424 423 422 421 420 419 418 417 416 DIS Data octet #55 Data octet #54 Data octet #53 Data octet #52 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA MessageData[2][9] MessageData[2][8] MessageData[2][7] MessageData[2][6]

Bit # 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 VMF information fields Word Format Bit # 479 478 477 476 475 474 473 472 471 470 469 468 467 466 465 464 463 462 461 460 459 458 457 456 455 454 453 452 451 450 449 448 DIS Data octet #59 Data octet #58 Data octet #57 Data octet #56 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA MessageData[3][3] MessageData[3][2] MessageData[3][1] MessageData[3][0]

<a id="source-pdf-page-88"></a>

## Source PDF page 88

### SISO-STD-002-2021

Link 16 Simulation Copyright © 2021 SISO. All rights reserved. Page 88 of 90 This is an approved SISO Standard. Bit # 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 VMF information fields (cont’d) Bit # 511 510 509 508 507 506 505 504 503 502 501 500 499 498 497 496 495 494 493 492 491 490 489 488 487 486 485 484 483 482 481 480 DIS Data octet #63 Data octet #62 Data octet #61 Data octet #60 Bit # 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA MessageData[3][7] MessageData[3][6] MessageData[3][5] MessageData[3][4]

Bit #       74 73 72 71 70 69 68 67 66 65 64 Padding Parity VMF information fields (cont’d) Bit #                 527 526 525 524 523 522 521 520 519 518 517 516 515 514 513 512 DIS Padding Data octet #65 Data octet #64 Bit #  7 6 5 4 3 2 1 0 7 6 5 4 3 2 1 0 HLA  MessageData[3][9] MessageData[3][8]

Navigation: previous [Annex A - FOM module](07-annex-a-fom-module-pages-052-068.md) | [coverage index](README.md) | next [Annex C - Version changes](09-annex-c-version-changes-pages-089-090.md)
