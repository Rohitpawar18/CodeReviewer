# Methodology

## Review Pipeline

1. Ingest PR metadata and diff content.
2. Apply ScaleDown compression for large inputs.
3. Run analysis agents on code, docs, and configuration.
4. Aggregate and rank findings.
5. Persist results for API and dashboard access.

## Ranking Approach

- Impact: severity and potential user or security risk.
- Confidence: signal strength, rule certainty, and context coverage.
- Findings are ordered to surface the most actionable items first.

## Quality Principles

- Favor actionable feedback over exhaustive noise.
- Preserve developer context and intent.
- Keep feedback consistent and traceable to sources.

## Metrics

- Review time reduction.
- Coverage of major issue categories.
- Accuracy and ranking quality of findings.
