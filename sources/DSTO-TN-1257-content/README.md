# Structured content - DSTO-TN-1257

This directory maps all 41 pages of `DSTO-TN-1257.pdf` into navigable Markdown. The concise technical entry point is [`../DSTO-TN-1257.md`](../DSTO-TN-1257.md).

## Section coverage

| Source PDF pages | Output | Extracted words | Images reported by parser |
| --- | --- | ---: | ---: |
| 1-8 | [Front matter and executive summary](00-front-matter-and-executive-summary-pages-001-008.md) | 536 | 1 |
| 9-15 | [Link 16 and distribution protocols](01-link-16-and-distribution-protocols-pages-009-015.md) | 2,777 | 0 |
| 16-24 | [Wireshark dissector design and implementation](02-wireshark-dissector-design-and-implementation-pages-016-024.md) | 2,721 | 1 |
| 25-29 | [Testing and conclusions](03-testing-and-conclusions-pages-025-029.md) | 1,423 | 0 |
| 30-41 | [Appendices and sample capture](04-appendices-and-sample-capture-pages-030-041.md) | 2,960 | 0 |

## Audits

- [`COVERAGE.md`](COVERAGE.md) maps every source page to its output anchor and records extraction/visual density.
- [`TABLES-AND-FIGURES.md`](TABLES-AND-FIGURES.md) inventories extracted table/figure captions and every page containing embedded images or a caption-inferred vector/table/figure layout.
- Hash and source identity are retained in the concise entry point and the repository-wide `docs/PDF-CONVERSION-INDEX.md`.

This structure preserves recoverable text and locators. Parser image counts do not detect PDF vector paths, so caption-inferred visual pages are also flagged. The conversion does not claim that text extraction recreates a glyph, diagram, map, line style, or exact table cell geometry.
