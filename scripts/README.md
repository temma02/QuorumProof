# Operational Scripts Index

This directory holds the operational scripts used to build, test, deploy, back up,
migrate, and benchmark the project. Use this index to find the right script and to
see whether it is run automatically by CI or manually by an operator.

Legend for the **Invoked by** column:

- A workflow name refers to a job in `.github/workflows/`.
- `manual` means an operator runs the script by hand.

## Build & Test

| Script | Description | Invoked by |
| --- | --- | --- |
| `build.sh` | Builds the workspace artifacts. | CI (`ci.yml` → `contracts`) |
| `test.sh` | Runs the unit and integration test suites. | CI (`ci.yml` → `contracts`) |
| `pre_upgrade_checks.sh` | Runs pre-upgrade safety checks before an upgrade is scheduled. | manual |
| `mutation_test.sh` | Runs mutation testing to measure test-suite effectiveness. | manual |

## Deploy

| Script | Description | Invoked by |
| --- | --- | --- |
| `deploy.sh` | Deploys the contracts to the target network. | manual |
| `deploy_multi_region.sh` | Deploys across multiple regions for redundancy. | manual |
| `canary_deploy.sh` | Rolls out a canary deployment to a subset of traffic. | manual |
| `canary_test.sh` | Exercises the canary deployment and validates its health. | manual |
| `failover.sh` | Fails traffic over to a healthy region when the primary degrades. | manual |
| `testnet_rollback.sh` | Rolls the testnet back to the previous release. | manual |

## Backup & Disaster Recovery

| Script | Description | Invoked by |
| --- | --- | --- |
| `backup.sh` | Captures a state snapshot for disaster recovery. | manual |
| `restore.sh` | Restores state from a previously captured snapshot. | manual |
| `reconcile_state.sh` | Reconciles on-chain state against the expected snapshot. | manual |

## Migration

| Script | Description | Invoked by |
| --- | --- | --- |
| `migration_orchestrator.py` | Orchestrates the end-to-end migration workflow. | manual |
| `upgrade_scheduler.py` | Schedules and sequences contract upgrades. | manual |

## Benchmarking

| Script | Description | Invoked by |
| --- | --- | --- |
| `benchmark.sh` | Runs the performance benchmark suite. | manual |
| `benchmark_compare.py` | Compares benchmark runs and reports regressions. | manual |

> The tables above cover the scripts currently present in `scripts/`. When adding a
> new script, add a row here with its purpose and how it is invoked.

## Test Coverage

Scripts under `scripts/tests/` provide automated coverage for a subset of the
operational scripts:

| Script | Test coverage |
| --- | --- |
| `migration_orchestrator.py` | `scripts/tests/test_migration_orchestrator.py` |
| `reconcile_state.sh` | `scripts/tests/test_reconcile_state.sh` |
| All other scripts | No automated test coverage — verify manually before use. |

When you add or change a script, prefer adding a matching test under
`scripts/tests/` and update this table.
