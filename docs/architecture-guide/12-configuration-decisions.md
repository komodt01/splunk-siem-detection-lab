# Splunk Configuration Decisions

## Purpose

This document captures the significant configuration decisions made while building the Splunk SIEM Detection Lab. Rather than documenting only what was configured, it explains why each decision was made, what alternatives were considered, and the operational impact. The intent is to demonstrate architectural thinking, not simply installation steps.

## Decision 1 – Dedicated Security Index

### Problem

Linux authentication events needed to be stored without mixing them with Splunk's default data.

### Decision

Create and use the `security_lab` index.

### Alternatives Considered

- main index
- Dedicated security index

### Why This Was Chosen

A dedicated security index separates security telemetry from system data, simplifies searches, supports future retention policies, enables role-based access control (RBAC), and reflects common enterprise SIEM practices.

### Business Value

Separating security data improves operational efficiency, simplifies investigations, and prepares the environment for future scaling.

## Decision 2 – Linux Secure Source Type

### Problem

Ubuntu authentication logs were initially detected using the generic `default` source type.

### Decision

Use the built-in `linux_secure` source type.

### Alternatives Considered

- default
- linux_secure
- custom source type

### Why This Was Chosen

The built-in Linux parser provides vendor-supported field extraction, timestamp handling, CIM alignment, and compatibility with Splunk Enterprise Security and Security Essentials.

### Validation

Preview confirmed:

- Correct timestamps
- Correct event boundaries
- One authentication event per Splunk event
- Automatic Linux field extractions

### Business Value

Using supported parsers reduces operational maintenance while improving detection accuracy.

## Decision 3 – Preserve Automatic Parsing

### Problem

Several parser settings could be manually overridden.

### Decision

Retain the default parser configuration supplied by the `linux_secure` source type.

### Alternatives Considered

- Manual timestamp extraction
- Manual line breaking
- Manual field extraction
- Built-in parser

### Why This Was Chosen

The preview showed that Splunk correctly parsed the data without customization.

### Business Value

Avoiding unnecessary customization reduces future maintenance and lowers operational risk.

## Decision 4 – Validate Before Ingestion

### Problem

Incorrect parsing can permanently affect indexed data.

### Decision

Always validate data using the preview before enabling ingestion.

### Why This Was Chosen

Preview verifies:

- Event boundaries
- Timestamp recognition
- Character encoding
- Source type behavior
- Parsing quality

### Business Value

Finding parsing issues before indexing reduces troubleshooting time and prevents corrupted production data.

## Guiding Principles

Throughout this project the following architectural principles will be followed:

- Prefer built-in capabilities before custom development.
- Minimize configuration complexity.
- Validate before deploying.
- Separate security telemetry from operational data.
- Choose maintainability over unnecessary customization.
- Design for future scale rather than immediate convenience.
