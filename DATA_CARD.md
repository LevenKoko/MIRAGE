# Dataset Card

## Summary

MIRAGE CanaryDocs contains `20,700` synthetic English enterprise documents with
ordered chunks and document-level structured Gold annotations. Gold units cover nine mutually
exclusive types, including synthetic canaries. It accompanies the EMNLP 2026 paper
*When Metadata Remembers: Ordered Provenance Enables Document-Level Embedding Inversion*.

## Composition

| Split | Documents | Chunks | Gold units | Canaries | Occurrences |
|---|---:|---:|---:|---:|---:|
| Shadow | 20,000 | 108,953 | 275,920 | 32,000 | 308,385 |
| Dev | 100 | 635 | 1,442 | 198 | 1,608 |
| Test | 600 | 3,744 | 8,878 | 1,181 | 9,894 |

## Intended uses

- Structured privacy-unit recovery evaluation.
- Canary recovery and ordered-context analysis.
- Chunk/document alignment and long-context retrieval research.
- Synthetic benchmark development and parser evaluation.

## Evaluation policy

All document text, Gold units, canary values, spans, alignments, and dependencies are intentionally
public for all three splits. The test split is an openly labeled reference split rather than a hidden
test set or evaluation-server split.

## Distribution

The complete dataset is distributed through
[LevenKoko/MIRAGE-CanaryDocs](https://huggingface.co/datasets/LevenKoko/MIRAGE-CanaryDocs).
The GitHub repository contains documentation, schemas, and release metadata only.

## Data characteristics

- Language: English.
- Domain: synthetic enterprise requests, reviews, approvals, finance, locations, and releases.
- All email domains and hosted URLs use non-routable `.invalid` namespaces.
- Character and token spans are included for every occurrence.

## Limitations

The text is synthetic and may contain formulaic phrasing or intentionally unusual identifiers. It
should not be used as evidence about real people, organizations, credentials, or operational systems.

## Associated paper

**When Metadata Remembers: Ordered Provenance Enables Document-Level Embedding Inversion**

EMNLP 2026.

## License

Creative Commons Attribution 4.0 International (CC BY 4.0).
