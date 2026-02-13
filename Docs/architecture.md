# Architecture

## Overview

Code Review Agent is organized as a small set of services and shared packages that work together to ingest pull requests, run analysis agents, and surface ranked findings.

## Components

- API service (apps/api)
  - Ingests reviews and exposes REST endpoints.
  - Persists review data to PostgreSQL.
  - Enqueues background work to Redis-backed queues.
- Worker service (apps/worker)
  - Pulls jobs from queues.
  - Runs analysis agents and ranking.
- Dashboard (apps/dashboard)
  - React UI for summaries, findings, and surveys.
- Shared packages (packages/*)
  - Agents, ScaleDown compression, types, and repository utilities.

## Data Flow

1. Client submits a review request to the API.
2. API stores metadata and enqueues analysis jobs.
3. Worker executes agents and writes findings back to storage.
4. Dashboard reads summaries and findings via the API.

## Storage and Queueing

- PostgreSQL: primary data store for reviews, findings, and surveys.
- Redis: job queue for background analysis (optional when API runs inline).

## Extensibility

- New analysis tools can be added in packages/agents.
- ScaleDown can be tuned to preserve additional signals.
