# DSTO-TN-1257 - Extending Wireshark to Decode Link 16 Messages

## Source identity

| Field | Value |
| --- | --- |
| Full title | Extending the Wireshark Network Protocol Analyser to Decode Link 16 Tactical Data Link Messages |
| Authors | William Robertson and others, Defence Science and Technology Organisation |
| Date | January 2014 |
| Report | DSTO-TN-1257 |
| Original file | `DSTO-TN-1257.pdf` |
| Original length | 41 PDF pages |
| SHA-256 | `c8c015869565a74e61acb0a227a73c3f0432522ae5864d25e8266b6ea4d51bcd` |
| Archived source URL | [DSTO-TN-1257 PDF](https://willrobertson.id.au/resources/wireshark/DSTO-TN-1257.pdf) |
| Classification | Unclassified; approved for public release |

## Technical summary

The report documents a Wireshark dissector for Link 16 traffic transported by publicly described simulation and distribution protocols. A native J-series word has 75 bits: 70 message-data bits plus 5 parity bits. The label and sublabel in the initial word identify the message family.

Two carriage formats require different normalization:

- SIMPLE stores an 80-bit representation in little-endian order.
- SISO-J stores the message across three interleaved, big-endian 32-bit values.

The implementation normalizes these inputs to an 80-bit little-endian representation before decoding. The public dissector described here resolves label and sublabel; it does not expose the unavailable payload semantics of every J-series message.

## Validation described by the report

- Decoding was compared with the SISO standard's informative examples and available equipment output.
- Little- and big-endian systems and 32- and 64-bit platforms were exercised.
- More than 2,000 fuzzing iterations were reported without a crash.
- Appendix A provides a base64-encoded packet capture containing a J2.2 initial-extension/continuation sequence and related traffic.

These are historical results for the documented code and environment. They are useful provenance, not evidence that the current TACSIT implementation has passed the same tests.

## Source map

The report covers Link 16/J-series word structure, distribution protocols, Wireshark architecture, dissector design, implementation, testing, conclusions, a sample capture, and a historical patch. Appendix B is code-lineage evidence; its presence does not remove the need to review license and correctness before reusing code.

## Provenance caution

DSTO-TN-1257, the SimTecT paper, and the historical Wireshark dissector share authorship and implementation lineage. Treat them as complementary explanations of one public implementation, not as three independent confirmations of a field definition.

## TACSIT boundary

The report supports public parsing of the distribution envelope and explicitly documented header/label information. Unknown J-series payload data must stay opaque. TACSIT must not invent track fields, trajectories, weapon assignments, intercepts, or fire-control solutions from an undecoded payload.

## Conversion note

All 41 pages were text-extracted with no failed pages. Representative architecture figures, byte-layout diagrams, test tables, and appendices were rendered and inspected. Exact packet bytes and historical source code are not duplicated here.

## Detailed converted content

- [Section and chapter coverage](DSTO-TN-1257-content/README.md)
- [Page-to-output audit](DSTO-TN-1257-content/COVERAGE.md)
- [Tables, figures, and visual-content audit](DSTO-TN-1257-content/TABLES-AND-FIGURES.md)
