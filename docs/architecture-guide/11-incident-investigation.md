# Splunk Incident Investigation

## Purpose

Incident Investigation is the process of using security telemetry to determine what happened, how it happened, what systems were affected, and what actions should be taken to contain and remediate a security event. Splunk provides investigators with centralized visibility into security data that supports evidence-based decision making.

This document explains how Splunk supports the incident investigation lifecycle and the architectural considerations required to enable effective investigations.

---

# What Is Incident Investigation?

Incident investigation is the systematic analysis of security events to determine:

- What occurred
- When it occurred
- Who was involved
- Which systems were affected
- How the attack progressed
- What business impact exists
- What remediation actions are required

Effective investigations depend on reliable, complete, and timely security telemetry.

---

# Investigation Lifecycle

A typical investigation includes:

1. Alert received
2. Initial triage
3. Scope determination
4. Evidence collection
5. Timeline reconstruction
6. Root cause analysis
7. Containment
8. Eradication
9. Recovery
10. Lessons learned

Splunk primarily supports the evidence collection and analysis phases.

---

# Investigation Data Sources

Investigators commonly analyze:

- Windows Event Logs
- Sysmon
- Linux authentication logs
- Firewall logs
- VPN logs
- Cloud audit logs
- Identity providers
- Endpoint Detection and Response (EDR)
- Threat intelligence
- Application logs

The broader the visibility, the greater the investigative context.

---

# Investigation Activities

Typical activities include:

- User activity analysis
- Authentication review
- Process execution analysis
- Network connection review
- Timeline creation
- Event correlation
- Asset identification
- Privilege analysis

Splunk enables investigators to correlate events across multiple systems.

---

# Search Strategy

Investigations generally begin with broad searches before narrowing to specific indicators.

Common approaches include:

- Searching by user
- Searching by host
- Searching by IP address
- Searching by process
- Searching by timeframe
- Searching by event type

Efficient searches reduce investigation time.

---

# Evidence Integrity

Architects should ensure:

- Reliable timestamps
- Complete telemetry
- Secure storage
- Audit logging
- Controlled administrative access
- Appropriate retention

The integrity of security evidence is essential for investigations and regulatory compliance.

---

# Security Considerations

Architects should consider:

- Data confidentiality
- Least privilege
- Chain of custody
- Regulatory requirements
- Evidence preservation
- Investigation auditing

Security investigations often involve highly sensitive information.

---

# Operational Considerations

Organizations should establish:

- Investigation procedures
- Escalation processes
- Documentation standards
- Communication plans
- Evidence retention policies
- Incident review procedures

Consistent processes improve investigation quality.

---

# Architecture Considerations

Architectural decisions include:

- Required telemetry
- Log retention
- Search performance
- Data normalization
- Detection integration
- Asset context
- Identity integration
- Scalability

Well-designed architecture reduces investigation complexity.

---

# Tradeoffs

## Extensive Data Collection

Benefits

- Better investigative context
- Improved timeline reconstruction
- Greater detection opportunities

Tradeoffs

- Increased storage
- Higher licensing costs
- More operational complexity

---

## Selective Data Collection

Benefits

- Lower cost
- Easier management
- Faster searches

Tradeoffs

- Investigation blind spots
- Reduced evidence
- Potentially incomplete timelines

---

# Best Practices

- Collect security-relevant telemetry.
- Preserve evidence.
- Validate timestamps.
- Standardize investigation procedures.
- Document findings.
- Review incidents for continuous improvement.

---

# Interview Questions

- How does Splunk support incident investigations?
- Why is telemetry quality important?
- How would you investigate a compromised account?
- Why is timeline reconstruction valuable?
- What architectural decisions improve investigations?

---

# Lessons Learned

To be completed throughout the project.

---

# Lab Implementation

Planned implementation:

- Failed login investigation
- PowerShell investigation
- Sysmon process investigation
- Authentication timeline reconstruction
- Multi-source event correlation

---

# Architect's Perspective

A Security Architect enables effective investigations by ensuring the organization collects the right telemetry, protects the integrity of security evidence, and designs an architecture that allows investigators to reconstruct events quickly and accurately. The goal is not merely to collect logs, but to provide the visibility necessary to reduce business impact during security incidents.
