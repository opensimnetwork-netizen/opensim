# LOBO Architecture

## Design principle

OpenSimulator remains the world simulation engine. LOBO adds an external control plane around it.

This separation is deliberate: it lowers the risk of breaking simulator behavior and makes upstream OpenSimulator updates easier to consume.

## High-level architecture

```text
                    +---------------------------+
                    |      LOBO Web Console     |
                    +-------------+-------------+
                                  |
                                  v
                    +---------------------------+
                    |       LOBO API Layer      |
                    +-------------+-------------+
                                  |
               +------------------+------------------+
               |                  |                  |
               v                  v                  v
      +----------------+ +----------------+ +----------------+
      | Grid Manager   | | Region Manager | | Backup Manager |
      +----------------+ +----------------+ +----------------+
               |                  |                  |
               +------------------+------------------+
                                  |
                                  v
                    +---------------------------+
                    |   LOBO Service/Agent      |
                    +-------------+-------------+
                                  |
          +-----------------------+-----------------------+
          |                       |                       |
          v                       v                       v
   +-------------+        +---------------+       +---------------+
   | ROBUST      |        | OpenSim       |       | MariaDB/MySQL |
   | services    |        | regions       |       | database      |
   +-------------+        +---------------+       +---------------+
```

## Components

### 1. LOBO Web Console

Browser-based administration interface.

Planned capabilities include grid status, region management, user administration, logs, backups, alerts, server metrics, Hypergrid configuration, and upgrades.

### 2. LOBO API

The API exposes authenticated management operations to the web console and, later, other clients.

The API should not directly execute arbitrary shell commands supplied by a browser client.

### 3. LOBO Service / Agent

A privileged service installed on each managed server.

Responsibilities may include:

- start/stop/restart services;
- write validated configuration;
- inspect process health;
- gather metrics;
- collect logs;
- execute backup/restore jobs;
- manage approved firewall rules;
- perform controlled upgrade/rollback actions.

### 4. OpenSimulator

The simulation engine.

LOBO should prefer documented configuration files, console interfaces, service APIs, and database interfaces rather than invasive core modifications.

### 5. ROBUST

Grid services remain separated from region simulator processes where appropriate.

### 6. Database

MariaDB/MySQL is the initial target for production-style grid deployments.

Database credentials must never be committed to Git.

## Security model

- Secrets stay outside source control.
- API authentication is mandatory.
- Privileged operations are allow-listed.
- Destructive actions require explicit authorization.
- Backups are created before automated upgrades.
- Configuration changes should be versioned and reversible.
- Remote administration should use TLS.
- Server agents should run with the minimum privileges required.

## Deployment model

### Single-server mode

Suitable for development and small grids:

```text
Contabo server
  ├── MariaDB
  ├── ROBUST
  ├── OpenSim region processes
  ├── LOBO API
  └── LOBO Web Console
```

### Multi-server mode

Planned for later phases:

```text
Control server
  ├── LOBO API
  ├── LOBO Web Console
  └── central monitoring

Database server
  └── MariaDB

Region server A
  ├── LOBO Agent
  └── regions

Region server B
  ├── LOBO Agent
  └── regions
```

## Compatibility objective

LOBO must not intentionally break standard OpenSimulator viewers, Hypergrid behavior, OAR files, IAR files, or normal region content.

## First technical milestone

Deploy an unmodified build from this fork to the staging server, prove that it can run correctly, and only then begin adding the LOBO management layer.
