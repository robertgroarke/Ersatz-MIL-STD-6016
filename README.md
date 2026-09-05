# Ersatz MIL-STD-6016

Open-source reconstruction of the Link 16 / TADIL-J message schema, built entirely from publicly available sources.

**This is NOT a substitute for MIL-STD-6016 or STANAG 5516.** The actual standards are export-controlled. This project reconstructs what can be inferred from open literature for use in simulation, education, and interoperability research.

## Browse online

The interactive HTML reference is published via GitHub Pages:

**https://liotier.github.io/Ersatz-MIL-STD-6016/**

## Contents

| File | Description |
|------|-------------|
| `link16-schema.json` | Machine-readable JSON schema — message types, NPGs, physical/link layer parameters |
| `link16-reference.html` | Self-contained HTML reference with search, filtering, and deep-linking |
| `sources/` | Markdown references derived from the public source set; each records the exact original's hash and length |

### Schema coverage

- **78 message types** across labels J0–J31 with confidence ratings
- **23 Network Participation Groups** (NPGs) with message associations
- Physical layer (frequency hopping, modulation, pulse structure)
- Link layer (header/message word formats, packing modes)
- SISO-STD-002 simulation network header
- JTIDS/MIDS terminal types

### HTML reference sections

1. Coverage index and statistics
2. Physical layer
3. TDMA structure
4. Link layer (word formats, packing modes)
5. Simulation network header (SISO-STD-002)
6. Network Participation Groups
7. Terminal types
8. Label categories
9. Full message schema (collapsible, searchable)
10. Gaps and limitations
11. Sources and citations

## Sources

- [**SISO-STD-002-2021**](sources/SISO-STD-002-2021.md) — Standard for Link 16 Simulation Version 2.0
- [**DSTO-TN-1257**](sources/DSTO-TN-1257.md) — Extending the Wireshark Network Protocol Analyser to Decode Link 16 Tactical Data Link Messages
- [**SimTecT 2010-64**](sources/SimTecT2010-64.md) — An Open Source Network Protocol Analyser for SISO-J TDL Simulation
- [**AFIT IP-Over-Link16**](sources/AFIT-IP-Over-Link16.md) — Air Force Institute of Technology thesis

## License

[Unlicense](LICENSE) — public domain.
