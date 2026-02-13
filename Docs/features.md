# Features

## Core Capabilities

- Pull request ingestion for GitHub and GitLab.
- Automated analysis across style, security, documentation, and performance.
- Ranked feedback based on impact and confidence.
- Snippet review UI for fast decision-making.

## ScaleDown Compression

- Compresses large diffs and commit history.
- Preserves key signals such as TODOs, signatures, and security-relevant lines.
- Reduces review time without losing critical context.

## Developer Workflow

- Dashboard views for snippet reviews and ranked feedback.

## Operational Features

- Background job processing with Redis.
- Clear separation of API, worker, and UI.
- Workspace-based monorepo with shared packages.
