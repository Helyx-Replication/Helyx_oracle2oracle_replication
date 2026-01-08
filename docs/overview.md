# Getting Started

### Introduction
Helyx is a lightweight, high-performance replication solution designed for real-time heterogeneous database replication. It provides a simple CLI-driven experience and abstracts the complexity of setting up connectors, schema registry, and replication pipelines.

### Key highlights of Helyx

**Heterogeneous Replication** : Supports replication across multiple database systems (e.g., PostgreSQL ↔ PostgreSQL, Oracle ↔ Oracle, Oracle → PostgreSQL, Oracle → MySQL, Oracle → MongoDB, Oracle → Snowflake).

**High Throughput** : Capable of handling hundreds of thousands of transactions per second across distributed data centers.

**Schema Evolution Handling** : Automatically adapts to schema changes like column additions and keeps source and target databases in sync.

**Zero-Downtime Replication** : Supports ad-hoc snapshots and live streaming without interrupting production workloads.

**Monitoring & Control** : Built-in CLI commands allow users to check replication lag, list connectors, view tasks, and monitor end-to-end replication health.

**Deployment Friendly** : Delivered as self-contained executables and RPM packages, making installation and upgrades straightforward.

**Version-Aware Replication** : Helyx supports replication between different versions of the same technology stack (e.g., PostgreSQL 11 → PostgreSQL 15 or EDB 12 → EDB 14 or Oracle11g → Oracle19c). This ensures smooth migrations and upgrades without downtime.

With Helyx, enterprises can achieve enterprise-grade replication with lower operational overhead, faster setup, and proven reliability compared to traditional tools.