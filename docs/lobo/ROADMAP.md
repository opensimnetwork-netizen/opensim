# LOBO Development Roadmap

## Phase 0 — Foundation

- [x] Create GitHub account connection.
- [x] Fork `opensim/opensim`.
- [x] Create `lobo-development` branch.
- [x] Document initial product direction.
- [x] Capture staging server specifications.
- [x] Establish build verification.
- [ ] Tag a known-good upstream baseline.

## Phase 1 — Clean OpenSimulator staging deployment

- [x] Inspect Contabo OS, CPU, RAM, disk, and network configuration.
- [x] Install required .NET runtime and dependencies.
- [ ] Install/configure MariaDB.
- [x] Build OpenSimulator from `lobo-development`.
- [ ] Launch a test ROBUST instance.
- [ ] Launch at least one test region.
- [ ] Verify viewer login.
- [ ] Verify asset and inventory persistence.
- [ ] Verify Hypergrid connectivity.
- [ ] Create first automated backup.

Exit criterion: an unmodified LOBO fork runs reliably on the staging server.

## Phase 2 — LOBO service foundation

- [ ] Define service configuration format.
- [ ] Build process supervisor interface.
- [ ] Add health/status endpoint.
- [ ] Add structured logs.
- [ ] Add region discovery.
- [ ] Add controlled start/stop/restart operations.
- [ ] Add authentication.

Exit criterion: LOBO can safely observe and control a test OpenSimulator deployment without modifying simulator core code.

## Phase 3 — Web control panel

- [ ] Dashboard.
- [ ] Grid status.
- [ ] Region list.
- [ ] Region start/stop/restart.
- [ ] Log viewer.
- [ ] Resource utilization.
- [ ] Backup controls.
- [ ] User/estate administration.

## Phase 4 — Installer and configuration engine

- [ ] Detect supported Linux distributions.
- [ ] Validate ports and firewall.
- [ ] Generate ROBUST configuration.
- [ ] Generate OpenSim configuration.
- [ ] Configure database.
- [ ] Configure domain/TLS.
- [ ] Add configuration validation.
- [ ] Add repair mode.

## Phase 5 — Backups and disaster recovery

- [ ] Database snapshots.
- [ ] OAR automation.
- [ ] IAR automation.
- [ ] Configuration backups.
- [ ] Scheduled retention.
- [ ] One-click restore workflow.
- [ ] Recovery testing.

## Phase 6 — Safe updates

- [ ] Track upstream OpenSimulator changes.
- [ ] Pre-upgrade backup.
- [ ] Build/test updated code.
- [ ] Controlled rollout.
- [ ] Health validation.
- [ ] Automatic rollback on failure.

## Phase 7 — Multi-server grid management

- [ ] Remote LOBO agents.
- [ ] Region placement.
- [ ] Centralized monitoring.
- [ ] Cross-server deployment.
- [ ] Capacity reporting.
- [ ] Failure isolation.

## Phase 8 — Migration tooling

- [ ] Import existing OpenSimulator configuration.
- [ ] Detect DreamGrid-style installations where technically feasible.
- [ ] Import regions and service settings.
- [ ] Validate migrated grid before cutover.

## Rules for development

1. Do not commit passwords, API keys, database credentials, or private certificates.
2. Do not make experimental changes directly on `master`.
3. Prefer management-layer features over modifying OpenSimulator core.
4. Every destructive operation needs a recovery path.
5. Staging validation comes before production deployment.
