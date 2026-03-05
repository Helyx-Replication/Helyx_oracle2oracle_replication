
# Helyx Oracle to Oracle Replication

This repository contains the **Helyx Oracle to Oracle replication tool**
along with **step-by-step documentation** and an installable **RPM package**.

---

# Getting Started

## Introduction

Helyx is a lightweight, high-performance replication solution designed for real-time **heterogeneous database replication**. It provides a simple **CLI-driven** experience and abstracts the complexity of setting up replication pipelines.

## Key highlights of Helyx

### Heterogeneous Replication

Supports replication across **multiple database systems** (e.g., **PostgreSQL ↔ PostgreSQL**, **Oracle ↔ Oracle**, **Oracle → PostgreSQL**, **Oracle → MySQL**, **Oracle → MongoDB**, **Oracle → Snowflake**).


### High Throughput

Capable of handling hundreds of thousands of transactions per second across distributed data centers.


### Schema Evolution Handling

Automatically adapts to **schema changes** like __column additions__ and keeps __source and target databases in sync__.


### Zero-Downtime Replication

Supports **ad-hoc snapshots** and **live streaming** without interrupting production workloads.


### Monitoring & Control

Built-in __CLI commands__ allow users to check replication **lag**, **list connectors**, **view tasks**, and monitor end-to-end replication health.


### Deployment Friendly

Delivered as containerized application making installation and upgrades straightforward.


### Version-Aware Replication 

Helyx supports replication between different versions of the same technology stack (e.g., **PostgreSQL 11 → PostgreSQL 15** or **EDB 12 → EDB 14** or **Oracle11g → Oracle19c**). This ensures smooth migrations and upgrades without downtime.

With Helyx, enterprises can achieve **enterprise-grade** replication with lower operational overhead, faster setup, and proven reliability compared to traditional tools.

# Deployment Architecture

Helyx is deployed as a **containerized distributed** replication platform running on Docker. The architecture consists of a **helyx-Sync-Manager** for durable event streaming, a **Helyx-Schema-Registry-manager** for schema management, **Helyx-broker-manager** for managing services and a **Helyx-Connect-service-manager** as a replication service.

The Oracle source database operates in **ARCHIVELOG** mode with supplemental logging, enabling real-time change data captutr **[CDC]**. Captured changes flow through topics and are applied to the Oracle target database with automatic schema evolution and fault-tolerant, zero-downtime streaming.

<div style="text-align: center;"> <img src="images\image.png" alt="Centered image"> </div>

---

# 🔹 Pre-requisites

- [Pre-requisites for Source Database](docs/prerequisite.md)


# Docker Environment Setup

- [Docker Environment Setup](docs/docker-env-setup.md)


# Set Up

- [Setting Up Destination Subscription](docs/setup-destination-database.md)


# Security

- [Security & Privilege Justification](docs/security.md)

