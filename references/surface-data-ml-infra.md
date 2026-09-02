# Data, ML, Infra, And Automation Surface Guide

Read this file when the repository is heavy on data processing, notebooks, ML artifacts, infrastructure, shell automation, CI workflows, or operational tooling.

## What To Record In Repository Guidance

- dataset locations, schemas, sampling strategy, cache directories, and artifact outputs;
- model-training or inference entrypoints, reproducibility constraints, and hardware assumptions;
- infrastructure commands such as `terraform`, `helm`, `kubectl`, container builds, or workflow runners;
- shell or PowerShell script entrypoints, dry-run modes, and destructive operations to avoid by default;
- secrets handling, environment segregation, and approval points for live systems.

## Editing Priorities

- Document what can be run locally, what is only safe in a staging environment, and what must never be run without explicit approval.
- Preserve reproducibility notes, pinned versions, and artifact-generation steps.
- Treat generated data, trained models, migration outputs, and deployment manifests as first-class repository artifacts that need provenance.
- If notebooks exist, separate exploratory notebooks from productionized jobs in the guidance.

## Testing Guidance

- Use fast local validation per edit when possible, such as unit tests, dry-run commands, schema checks, `terraform validate`, or workflow linting.
- Keep broader pipeline, training, deployment, or environment smoke tests separate and run them after a coherent work batch.
- If the repository lacks end-to-end or pipeline tests, create a mock skeleton first and ask the user before implementing the full version.
- Ask the user before treating dummy datasets, fake secrets, or synthetic production-like examples as acceptable fixtures.

## Typical Subtypes

Repository-local type files often need a separate note for:

- ETL or data pipeline;
- notebook or analytics workspace;
- ML training or inference system;
- infrastructure-as-code repo;
- CI or release automation repo;
- shell or PowerShell utility collection.
