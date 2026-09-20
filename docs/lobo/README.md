# LOBO Virtual World Platform

LOBO is a development initiative built on top of OpenSimulator with the goal of creating a modern, easier-to-operate virtual world platform and grid management system.

This branch intentionally keeps the upstream OpenSimulator codebase recognizable so that future upstream fixes can still be merged.

## Project goals

- Keep OpenSimulator as the simulation engine.
- Build a modern management layer instead of requiring operators to manage every service manually.
- Support Linux first for server deployment, with Windows support where practical.
- Make grid setup, region management, backups, monitoring, recovery, and upgrades easier.
- Preserve Hypergrid compatibility.
- Avoid vendor lock-in.
- Keep deployment reproducible and auditable.
- Make it possible to operate a small personal grid or scale to multiple region servers.

## Initial product scope

The first LOBO control plane is expected to manage:

1. Grid installation and configuration.
2. Robust services.
3. Region creation, start, stop, restart, and deletion.
4. Estate and user administration.
5. MariaDB/MySQL configuration.
6. Hypergrid configuration.
7. OAR/IAR backup and restore.
8. Health checks and automatic recovery.
9. Centralized logs.
10. Firewall and port diagnostics.
11. SSL/domain configuration.
12. Safe OpenSimulator updates with rollback.
13. Multi-server region management.
14. Web-based administration.

## Repository strategy

- `master` remains as close as possible to upstream `opensim/opensim`.
- `lobo-development` is the active integration branch for LOBO work.
- Core OpenSimulator changes should be minimized unless a feature truly belongs in the simulator.
- Management features should live outside the simulator core whenever possible.

## Staging environment

The project will be tested on a dedicated Contabo server before any production deployment. The staging environment will be used for build verification, database tests, region tests, Hypergrid tests, backups, restore tests, failure recovery, and upgrade testing.

## Current phase

Phase 0: repository and architecture foundation.

No production behavior has been changed yet.
