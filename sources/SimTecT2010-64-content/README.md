# Structured content - SimTecT2010-64

This directory maps all 4 pages of `SimTecT2010-64.pdf` into navigable Markdown. The concise technical entry point is [`../SimTecT2010-64.md`](../SimTecT2010-64.md).

## Section coverage

| Source PDF pages | Output | Extracted words | Images reported by parser |
| --- | --- | ---: | ---: |
| 1-4 | [Complete paper](00-complete-paper-pages-001-004.md) | 2,180 | 9 |

## Audits

- [`COVERAGE.md`](COVERAGE.md) maps every source page to its output anchor and records extraction/visual density.
- [`TABLES-AND-FIGURES.md`](TABLES-AND-FIGURES.md) inventories extracted table/figure captions and every page containing embedded images or a caption-inferred vector/table/figure layout.
- Hash and source identity are retained in the concise entry point and the repository-wide `docs/PDF-CONVERSION-INDEX.md`.

This structure preserves recoverable text and locators. Parser image counts do not detect PDF vector paths, so caption-inferred visual pages are also flagged. The conversion does not claim that text extraction recreates a glyph, diagram, map, line style, or exact table cell geometry.
