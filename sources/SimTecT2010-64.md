# An Open Source Network Protocol Analyser for SISO-J TDL Simulation

## Source identity

| Field | Value |
| --- | --- |
| Authors | William Robertson, Andrew Ross, and others |
| Venue | SimTecT 2010 |
| Original file | `SimTecT2010-64.pdf` |
| Original length | 4 PDF pages |
| SHA-256 | `d1fb12c8b2fd4ed73765e661fe270239f2b600ae99d175c75e79211d16dabaa6` |
| Archived source URL | [SimTecT paper PDF](http://pross.sdf.org/simtect2010-64.pdf) |

## Summary

This short paper presents an open-source Wireshark approach for inspecting SISO-J tactical data link simulation traffic. It distinguishes two common transports:

- SISO-J/DIS traffic carried over UDP; and
- SIMPLE traffic carried over TCP.

Neither protocol has a universally assigned transport port in the described environment, so dissector selection cannot rely on a standard port alone. The work focuses on transport recognition, packet framing, and the J-series label/sublabel. Message content beyond label and sublabel was deliberately not decoded.

The paper also discusses typical network stacks and proposes future work such as visualization and network characterization. Those proposals are not implemented evidence.

## Relevance and limitations

This is a concise design overview for the same public dissector lineage documented more fully in [`DSTO-TN-1257.md`](DSTO-TN-1257.md). It is useful for understanding the envelope and operator workflow, but it is not an independent field-level specification and does not replace SISO-STD-002-2021.

## Conversion note

All four pages were text-extracted and rendered for visual inspection. The paper's figures and screenshots are summarized rather than reproduced.

## Detailed converted content

- [Section and chapter coverage](SimTecT2010-64-content/README.md)
- [Page-to-output audit](SimTecT2010-64-content/COVERAGE.md)
- [Tables, figures, and visual-content audit](SimTecT2010-64-content/TABLES-AND-FIGURES.md)
