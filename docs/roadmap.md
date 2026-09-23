# Project Roadmap

## Vision

Develop a hands-on Splunk Enterprise SIEM environment that demonstrates security monitoring architecture, telemetry ingestion, SPL analysis, detection engineering, alerting, correlation, and investigation.

The roadmap tracks both implemented capabilities and areas intended for future expansion.

---

## Phase 0 – Architecture & Planning

**Status: Implemented**

Completed work includes:

- Repository structure
- Security and operational requirements
- Environmental constraints
- Architecture principles
- Architecture tradeoffs
- Environment assessment
- Architecture Decision Record (ADR)
- SIEM architecture diagram
- Implementation roadmap

---

## Phase 1 – Splunk Environment

**Status: Implemented**

Implemented capabilities include:

- Splunk Enterprise environment
- Local deployment using Ubuntu under WSL2
- Dedicated security index
- Validation of Splunk operation
- Exploration of Splunk architecture and configuration concepts

The environment provides the SIEM platform used for subsequent telemetry, search, and detection exercises.

---

## Phase 2 – Linux Data Onboarding

**Status: Implemented**

Implemented capabilities include:

- Linux authentication telemetry collection
- `/var/log/auth.log` ingestion
- Dedicated `security_lab` index
- `linux_secure` sourcetype
- Verification of ingested authentication events
- Review of raw security events

This phase established the telemetry foundation for authentication investigations and detection development.

---

## Phase 3 – SPL Fundamentals

**Status: Implemented**

Hands-on SPL work includes:

- Event searching
- Filtering
- Field selection
- Statistical analysis
- Time-based analysis
- Event counts
- Authentication searches
- Investigation-oriented queries

Examples and architectural context are documented in the architecture guide.

---

## Phase 4 – Windows Security Monitoring

**Status: Planned / Future Expansion**

Target capabilities include:

- Windows Security Event Logs
- Sysmon telemetry
- Windows authentication monitoring
- Endpoint security visibility
- Windows-focused detections

The current documented implementation focuses primarily on Linux authentication telemetry.

---

## Phase 5 – Dashboards & Visualization

**Status: Partial / Future Expansion**

Dashboard and visualization concepts are documented within the architecture guide.

Future implementation can expand the lab with reusable security dashboards covering:

- Authentication activity
- Detection trends
- Endpoint activity
- Security event volume
- Investigation metrics

---

## Phase 6 – Detection Engineering

**Status: Implemented – Initial Capability**

The lab progressed from manual authentication investigation into detection engineering.

Implemented work includes:

- Controlled SSH authentication failure generation
- Failed authentication search development
- Detection metadata
- Business objective definition
- MITRE ATT&CK mapping
- Severity considerations
- False-positive analysis
- Threshold design
- Tuning considerations
- Response workflow documentation

The initial detection focuses on failed SSH authentication activity.

Future work can expand the detection library to additional behaviors and telemetry sources.

---

## Phase 7 – Alerting, Correlation & Investigation

**Status: Implemented – Initial Capability**

The lab demonstrates the progression from individual security events toward investigation-ready monitoring.

Implemented work includes:

- Authentication event investigation
- Failed and successful authentication analysis
- Alert lifecycle analysis
- Authentication event correlation
- Five-minute correlation window
- Multi-event investigation using SPL
- Review of correlation scalability tradeoffs

Example correlation:

```spl
index=security_lab sourcetype=linux_secure earliest=-15m
("Failed password" OR "Accepted password")
| transaction host maxspan=5m
| search eventcount>1
| table _time host eventcount duration _raw
```

This phase demonstrates how individual events can be transformed into contextual information that supports security investigation.

---

## Phase 8 – Future Expansion

Potential future enhancements include:

- Windows and Sysmon telemetry
- Additional Linux detections
- Identity-focused detection scenarios
- Expanded dashboard implementation
- Additional alert actions
- More scalable correlation using `stats` or `streamstats`
- Detection-as-code concepts
- Detection validation and regression testing
- Cloud telemetry integration
- Additional MITRE ATT&CK coverage
- Incident response playbooks

---

## Current Capability

The lab currently demonstrates the following security monitoring lifecycle:

```text
Linux System
     |
     v
Authentication Event
     |
     v
/var/log/auth.log
     |
     v
Splunk Ingestion
     |
     v
security_lab Index
     |
     v
SPL Search
     |
     v
Authentication Investigation
     |
     v
Detection Logic
     |
     v
Alerting / Correlation
     |
     v
Investigation Context
```

The project will continue to evolve as additional telemetry sources and detection scenarios are implemented.
