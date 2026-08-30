# MIRAGE CanaryDocs

MIRAGE CanaryDocs is an English synthetic enterprise-document dataset for structured privacy-unit,
canary, and ordered multi-chunk evaluation. It is the companion dataset for the EMNLP 2026 paper
*When Metadata Remembers: Ordered Provenance Enables Document-Level Embedding Inversion*.

## Release

- Version: `1.0.0`
- Release date: `2026-08-30`
- Documents: `20,700` (`20,000` shadow / `100` dev / `600` test)
- Gold units: `286,240`
- Canary units: `33,379`
- Occurrences: `319,887`
- Chunks: `113,332`

All three splits intentionally publish both inputs and Gold annotations. The test split is an openly
labeled reference split, not a hidden test set or evaluation-server split.

## Data availability

The complete dataset is hosted on Hugging Face:

**[LevenKoko/MIRAGE-CanaryDocs](https://huggingface.co/datasets/LevenKoko/MIRAGE-CanaryDocs)**

This GitHub repository contains documentation, schemas, and release metadata only. It intentionally
does not duplicate the JSONL, Parquet, or SQLite payloads.

Clone the complete dataset repository with Git LFS:

```bash
git lfs install
git clone https://huggingface.co/datasets/LevenKoko/MIRAGE-CanaryDocs
```

Or download a snapshot from Python:

```python
from huggingface_hub import snapshot_download

snapshot_download(
    repo_id="LevenKoko/MIRAGE-CanaryDocs",
    repo_type="dataset",
    local_dir="MIRAGE-CanaryDocs",
)
```

## Dataset layout

The following paths are in the Hugging Face dataset repository:

- `data/`: normalized canonical JSONL entities.
- `views/bundled/`: one self-contained document per line.
- `views/canaries/`: canary-focused materialized views.
- `views/benchmark/`: nested Parquet views for dev and test.
- `database/canarydocs.sqlite`: release-only relational mirror with foreign keys.
- `metadata/`: schemas, taxonomy, statistics, chunk semantics, file inventory, and checksums.

## Relationship model

`document -> section -> paragraph`, `document -> chunk`, and
`document -> unit -> occurrence <-> chunk`. Repeated occurrences are linked through the
`dependencies` layer.

## Quick start

Run this example from the root of a downloaded dataset snapshot:

```python
import json

with open("views/bundled/test.jsonl", encoding="utf-8") as handle:
    first_document = json.loads(next(handle))

print(first_document["title"])
print(len(first_document["gold_units"]))
```

```sql
SELECT d.document_id, u.surface, c.chunk_index
FROM units u
JOIN occurrences o USING (unit_id)
JOIN alignments a USING (occurrence_id)
JOIN chunks c USING (chunk_id)
JOIN documents d USING (document_id)
WHERE u.is_canary = 1
ORDER BY d.document_id, c.chunk_index;
```

The test split contains `600` documents, `3744` actual chunks,
`8878` Gold units, and `1181` canaries.

## Associated paper

**When Metadata Remembers: Ordered Provenance Enables Document-Level Embedding Inversion**

EMNLP 2026.

## License

CC BY 4.0. See `LICENSE`.
