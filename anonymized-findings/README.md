# Anonymized AI red-team findings

Structured, machine-readable version of the findings already published on
<https://hiltlock.com/evidence>. One JSON object per line in `findings.jsonl`.

## Schema

| Field | Meaning |
| --- | --- |
| `id` | Stable identifier |
| `finding_class` | The failure category (e.g. broken object-level authorization) |
| `surface` | The AI surface where it was found (anonymized) |
| `severity` | Published severity, or `null` where the source did not state one |
| `technique` | How it was exploited (anonymized) |
| `control_status` | Whether the relevant control held or failed |
| `evidence` | One-sentence paraphrase of the published finding |
| `source_url` | The published case study it comes from |

## Anonymization

- No client, vendor, or partner names.
- No endpoints, hostnames, tool names, or field names.
- No payloads or strings that could identify a target.
- No unpublished numbers. Every row traces to a published case study.

## Scope

The mobile-app case study published six findings; the rows here are a
representative subset (one high, one medium, two low). The LMS row is one
aggregate row because the case study reports totals (28 findings, 3 critical,
8 high) rather than per-finding detail.
