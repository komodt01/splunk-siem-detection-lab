# Splunk SIEM Detection Lab

## Overview

This project is a hands-on security monitoring lab focused on the architecture, implementation, and evaluation of a Splunk-based SIEM environment.

The lab is being developed incrementally, beginning with requirements, constraints, architecture principles, environment assessment, and design tradeoffs before progressing into telemetry ingestion, SPL searches, detection engineering, dashboards, and simulated security investigations.

The objective is not to represent a production Splunk deployment. The project is intended to demonstrate how security monitoring requirements can be translated into architecture decisions and then validated through hands-on implementation.

---

## Security Architecture Objective

A SIEM is more than a centralized log repository.

An effective monitoring architecture must connect:

```text
Security Requirements
        |
        v
Telemetry Sources
        |
        v
Log Collection
        |
        v
Normalization / Search
        |
        v
Detection Logic
        |
        v
Alert / Investigation
        |
        v
Security Response
```

The lab explores this lifecycle while considering security, operational complexity, scalability, maintainability, cost, and risk.

---

## Business Problem

Organizations generate security telemetry across identity systems, endpoints, servers, applications, networks, and cloud platforms.

Without centralized visibility, security teams may have difficulty correlating activity across systems, identifying suspicious behavior, investigating incidents, retaining useful evidence, and supporting security and compliance reporting.

A SIEM architecture provides a centralized capability for collecting, searching, correlating, and analyzing security telemetry.

The architectural challenge is determining:

- Which telemetry provides meaningful security value
- How logs should be collected and retained
- Which behaviors should generate detections
- How detection logic should be validated
- How alerts support investigation and response
- How monitoring capability can scale without unnecessary operational complexity or cost

---

## Lab Objectives

The planned lab progresses from architecture into hands-on SIEM implementation.

Objectives include:

- Define SIEM security and operational requirements
- Document environmental constraints
- Evaluate architecture tradeoffs
- Deploy a local Splunk Enterprise environment
- Ingest representative Windows and Linux telemetry
- Develop SPL searches
- Build security-focused dashboards
- Create and test detection logic
- Generate simulated security activity
- Investigate resulting events and detections
- Document lessons learned and architecture decisions

Implementation status is tracked separately so planned capabilities are not represented as completed work.

---

## Architecture

![Splunk SIEM Detection Lab Architecture](architecture/splunk-siem-detection-lab-architecture.png)

The architecture documentation captures the design considerations that guide implementation.

Current architecture artifacts include:

```text
architecture/
├── constraints.md
├── environment-assessment.md
├── principles.md
├── requirements.md
├── tradeoffs.md
├── decisions/
└── splunk-siem-detection-lab-architecture.png
```

These documents establish the reasoning behind the environment before detection content is added.

---

## Architecture Lens

Major design decisions are evaluated across several dimensions:

- Business value
- Security
- Cost
- Operational complexity
- Scalability
- Maintainability
- Vendor dependency
- Risk

The objective is to evaluate not only whether a technical solution works, but whether it represents an appropriate security architecture decision.

---

## Design Principles

### Security Outcomes Before Tooling

Security requirements and monitoring objectives should determine the telemetry and detection strategy rather than allowing available tooling to define the security program.

### Detection Requires Useful Telemetry

A detection is only as effective as the data supporting it.

Telemetry selection therefore needs to consider visibility, fidelity, retention, performance, and cost.

### Architecture Should Support Investigation

Alerts alone are insufficient.

Security telemetry should provide enough context to help an analyst understand what occurred and determine whether additional investigation is required.

### Operational Complexity Matters

A technically capable monitoring platform can still fail if its operational requirements exceed the organization's ability to maintain it.

### Cost Is an Architecture Constraint

SIEM cost can be influenced heavily by data volume, retention, ingestion strategy, and platform design.

Logging everything indefinitely is not automatically the best security architecture.

### Detection Logic Must Be Tested

A search or detection rule should not be assumed effective simply because it executes successfully.

Detection logic should be tested against expected and simulated activity to determine whether it produces useful security signals.

---

## Planned Detection Workflow

The implementation phases are intended to demonstrate the complete path from telemetry generation to investigation.

```text
Windows / Linux Systems
          |
          v
Security Telemetry
          |
          v
Splunk Ingestion
          |
          v
Indexed Events
          |
          v
SPL Search
          |
          v
Detection Logic
          |
          v
Security Finding
          |
          v
Investigation
```

As implementation progresses, detection artifacts and validation evidence will be added to the repository.

---

## Technologies

The lab is designed around:

- Splunk Enterprise
- Windows
- Ubuntu Linux
- Sysmon
- SPL
- Docker where appropriate
- Git
- GitHub

Technologies will be documented as they are implemented rather than assumed to be present solely because they are part of the target design.

---

## Repository Structure

```text
splunk-siem-detection-lab/
├── README.md
├── CHANGELOG.md
├── architecture/
│   ├── constraints.md
│   ├── environment-assessment.md
│   ├── principles.md
│   ├── requirements.md
│   ├── tradeoffs.md
│   ├── decisions/
│   └── splunk-siem-detection-lab-architecture.png
└── docs/
    ├── architecture-guide/
    └── roadmap.md
```

Additional implementation directories will be added as the lab progresses.

---

## Current Status

The repository currently contains the architecture and planning foundation for the SIEM detection environment.

Completed documentation includes:

- Environment assessment
- Architecture requirements
- Architecture principles
- Constraints
- Design tradeoffs
- Architecture diagram
- Project roadmap

Hands-on Splunk deployment, telemetry ingestion, SPL development, detection engineering, and investigation artifacts should be considered planned work until the corresponding implementation evidence is added to the repository.

---

## Scope

This repository represents a controlled learning and architecture environment.

It is not intended to represent:

- A production Splunk deployment
- A complete SOC implementation
- A production-ready detection library
- A certified compliance monitoring solution
- An enterprise-scale SIEM deployment

The purpose is to develop and demonstrate practical understanding of SIEM architecture, telemetry, detection engineering, and security investigation while documenting the architecture decisions behind the implementation.

---

## Key Takeaway

Effective SIEM architecture connects security requirements to telemetry and telemetry to actionable detection.

```text
Requirement
    ↓
Telemetry
    ↓
Collection
    ↓
Search
    ↓
Detection
    ↓
Investigation
    ↓
Security Decision
```

The goal of this lab is to demonstrate that lifecycle incrementally and provide evidence for each capability as it is implemented.
