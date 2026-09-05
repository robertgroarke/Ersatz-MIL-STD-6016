# Internet Protocol (IP) Over Link-16

## Source identity

| Field | Value |
| --- | --- |
| Author | Clinton W. Stinson |
| Institution | Air Force Institute of Technology |
| Date | 2003 |
| Type | Master's thesis |
| Original file | `AFIT-IP-Over-Link16.pdf` |
| Original length | 87 PDF pages |
| SHA-256 | `6ad879c768f9b0b83dcde987333a9af060a7f86d8d26e3d41670aad362f3cf3c` |
| Catalog record | [AFIT Scholar](https://scholar.afit.edu/etd/4196) |
| Release | Approved for public release; distribution unlimited |

## Research question

The thesis evaluates the modeled performance impact of carrying Internet Protocol traffic over Link 16, with emphasis on IPv6 and IPsec overhead. It uses an OPNET simulation rather than an operational network trial.

The reported model found that IPv6/IPsec overhead did not significantly change end-to-end delay or effective throughput when cryptographic preprocessing was assumed. Once offered load rose above roughly 90 percent in the modeled cases, performance degraded significantly. Those findings belong to the stated simulation boundaries and early-2000s protocol assumptions; they are not a current operational capacity claim.

## Source map

- Introduction and research framing.
- Background on joint battlespace information, information assurance, IP, IPsec, Link 16, and CORBA-era integration.
- Methodology: system boundaries, services, metrics, factors, and parameters.
- Model implementation and verification.
- Results, statistical analysis, and interpretation.
- Conclusions and recommendations.
- Appendices containing analysis-of-variance output, plots, and MATLAB material.

## Relevance to this repository

This is historical architectural context for packet carriage over a constrained tactical data link. It supports cautious reasoning about encapsulation overhead, latency, throughput, queue saturation, and the difference between application-layer content and bearer behavior.

It does not disclose MIL-STD-6016 message definitions and does not justify creating J-series fields absent from public sources. Do not turn its modeled results into a TACSIT performance requirement without reproducing the assumptions and validating them against the intended environment.

## Conversion note

All 87 pages were text-extracted with no failed or low-text content pages. Representative prose, tables, plots, and appendix pages were rendered and inspected. Equations and plots are summarized rather than reproduced; use the cataloged thesis when their exact form is required.

## Detailed converted content

- [Section and chapter coverage](AFIT-IP-Over-Link16-content/README.md)
- [Page-to-output audit](AFIT-IP-Over-Link16-content/COVERAGE.md)
- [Tables, figures, and visual-content audit](AFIT-IP-Over-Link16-content/TABLES-AND-FIGURES.md)
