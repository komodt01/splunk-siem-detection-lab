# Splunk Detection Engineering

## Purpose

Detection Engineering is the process of designing, implementing, validating, tuning, and maintaining security detections that identify malicious or suspicious activity. Within Splunk, detections are typically implemented using SPL searches, scheduled alerts, dashboards, and supporting knowledge objects.

This document explains how Detection Engineering supports modern Security Operations and why it is a critical capability within a mature SIEM program.

---

# What Is Detection Engineering?

Detection Engineering is the discipline of creating reliable methods for identifying behaviors associated with cyber threats.

Rather than relying solely on signatures, modern detections often identify suspicious behaviors using log analysis, event correlation, and threat intelligence.

Detection Engineering is an ongoing lifecycle rather than a one-time implementation.

---

# Detection Lifecycle

A typical detection lifecycle includes:

1. Define the security objective
2. Identify required telemetry
3. Develop detection logic
4. Validate against known scenarios
5. Tune false positives
6. Deploy
7. Monitor effectiveness
8. Continuously improve

Detections should evolve as threats and environments change.

---

# Detection Sources

Effective detections rely on quality telemetry such as:

- Windows Event Logs
- Sysmon
- Linux authentication logs
- Active Directory
- Cloud audit logs
- Firewall logs
- Endpoint Detection and Response (EDR)
- Identity providers
- Threat intelligence

The quality of detections depends on the quality and completeness of the data.

---

# Detection Types

Organizations commonly implement:

- Signature-based detections
- Behavioral detections
- Threshold detections
- Correlation rules
- Anomaly detections
- Threat intelligence matching
- Risk-based detections

Each technique has strengths and limitations.

---

# Detection Logic

Detection logic should answer:

- What behavior is suspicious?
- What evidence supports the finding?
- Which data sources are required?
- What confidence level exists?
- What action should occur?

Effective detections minimize unnecessary complexity while maximizing reliability.

---

# False Positives and False Negatives

Detection tuning should balance:

False Positives

- Benign activity identified as malicious

False Negatives

- Malicious activity that is not detected

Neither objective can be eliminated entirely. Detection engineering seeks an acceptable operational balance.

---

# MITRE ATT&CK

Many organizations align detections with the MITRE ATT&CK framework.

Benefits include:

- Standardized terminology
- Threat coverage analysis
- Detection mapping
- Gap identification
- Improved reporting

MITRE mapping improves communication between analysts, engineers, and architects.

---

# Security Considerations

Architects should consider:

- Detection coverage
- Data integrity
- Telemetry quality
- Threat intelligence
- Alert prioritization
- Investigation context
- Continuous validation

Poor telemetry produces unreliable detections.

---

# Operational Considerations

Organizations should monitor:

- Alert volume
- Detection accuracy
- Mean Time to Detect (MTTD)
- False positive rates
- Detection coverage
- Rule maintenance
- Search performance

Detection quality should be measured continuously.

---

# Architecture Considerations

Architectural decisions include:

- Required telemetry
- Detection ownership
- Governance
- Rule lifecycle
- Threat modeling alignment
- Data normalization
- Integration with incident response

Detection engineering should align with organizational risk priorities.

---

# Tradeoffs

## Aggressive Detection Strategy

Benefits

- Greater visibility
- Earlier threat identification

Tradeoffs

- More false positives
- Greater analyst workload

---

## Conservative Detection Strategy

Benefits

- Reduced operational noise
- Higher confidence alerts

Tradeoffs

- Increased detection gaps
- Slower identification of threats

---

# Best Practices

- Build detections around known attack behaviors.
- Validate detections using test data.
- Tune regularly.
- Document assumptions.
- Align detections with MITRE ATT&CK.
- Review effectiveness after incidents.

---

# Interview Questions

- What is Detection Engineering?
- Why do false positives occur?
- How do you balance false positives and false negatives?
- Why is telemetry quality important?
- How does MITRE ATT&CK improve detections?
- What metrics would you use to evaluate detection quality?

---

# Lessons Learned

To be completed throughout the project.

---

# Lab Implementation

Planned implementation:

- Failed login detection
- PowerShell detection
- Sysmon process execution detection
- Privileged account monitoring
- Authentication anomaly dashboard
- MITRE ATT&CK mapping

---

# Architect's Perspective

Detection Engineering is a business capability, not simply a technical feature. A Security Architect determines which risks require detection, what telemetry is necessary, how detections integrate with incident response, and how detection coverage aligns with organizational objectives. Effective detections reduce organizational risk while minimizing operational burden.
