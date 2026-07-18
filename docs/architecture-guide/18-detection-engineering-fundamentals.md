# 18. Detection Engineering Fundamentals

## Purpose

This document introduces the principles of detection engineering and explains how security events are transformed into actionable security detections. Detection engineering extends beyond writing search queries by combining business context, threat intelligence, security architecture, operational processes, and continuous improvement to identify malicious behavior while minimizing false positives.

This document builds upon the authentication investigation performed within this Splunk SIEM Detection Lab and establishes the foundation for creating production-quality detections that support Security Operations Centers (SOC), Incident Response teams, and enterprise security programs.

## Business Perspective

Organizations invest heavily in security controls that generate enormous volumes of telemetry every day. Firewalls, operating systems, cloud services, endpoint protection platforms, identity providers, and applications continuously produce logs describing normal and abnormal activity.

Raw telemetry alone provides little business value.

Without effective detections, security teams must manually review millions of events, increasing operational costs while allowing attacks to remain undetected.

Detection engineering transforms security telemetry into actionable intelligence by identifying suspicious behaviors that warrant investigation. Well-designed detections improve visibility, reduce Mean Time to Detect (MTTD), accelerate incident response, improve compliance reporting, and strengthen organizational resilience against cyber threats.

## What Is Detection Engineering?

Detection engineering is the discipline of designing, implementing, validating, tuning, and maintaining security detections that identify malicious or suspicious activity.

Unlike simple log searches, detection engineering combines technical knowledge, threat intelligence, operational experience, and business risk to determine which behaviors should generate alerts.

Effective detection engineering balances visibility with operational efficiency by maximizing true positive detections while minimizing false positives.

## Why Detection Engineering Matters

Modern organizations generate millions of security events each day.

No security analyst can manually inspect every event.

Detection engineering enables security teams to automatically identify activity requiring investigation while filtering routine operational noise.

Effective detections reduce analyst fatigue, improve operational consistency, increase investigation speed, and improve the overall maturity of a security program.

## Detection Lifecycle

Every production detection should follow a structured lifecycle.

Identify a threat scenario.

Determine the business risk.

Identify available telemetry.

Develop an investigative search.

Validate against known events.

Tune thresholds.

Reduce false positives.

Deploy operationally.

Continuously monitor effectiveness.

Retire or improve detections as threats evolve.

Detection engineering is a continuous improvement process rather than a one-time implementation.

## Components of a Detection

A mature detection typically contains:

- Detection name
- Business objective
- Threat description
- Data sources
- SPL query
- Thresholds
- Severity
- MITRE ATT&CK mapping
- False positive guidance
- Tuning recommendations
- Response workflow
- Detection owner
- Review schedule

These elements ensure detections remain understandable, maintainable, and operationally effective.

## Building Our First Detection

During the laboratory investigation, an intentional SSH authentication failure was generated against an invalid user.

Ubuntu recorded the following sequence of events:

- Invalid user
- Failed password
- Failed password
- Maximum authentication attempts exceeded
- Session disconnected

Splunk successfully ingested these events into the security_lab index.

This investigation demonstrated the complete SIEM lifecycle:

Security Event

↓

Operating System Log

↓

Splunk Ingestion

↓

Search

↓

Investigation

↓

Detection

The first laboratory detection searches for failed SSH authentication attempts.

```spl
index=security_lab sourcetype=linux_secure "Failed password"
```

Although intentionally simple, this query validates the detection workflow from event generation through investigation.

## Business Value

Detecting repeated authentication failures provides early visibility into credential-based attacks including:

- Brute force attacks
- Password spraying
- Credential stuffing
- Unauthorized access attempts
- User enumeration

Early detection allows organizations to respond before attackers successfully compromise accounts.

## Detection Metadata

Detection Name:

Multiple Failed SSH Authentication Attempts

Business Objective:

Identify repeated authentication failures that may indicate malicious attempts to obtain unauthorized access.

Data Source:

Ubuntu Authentication Logs

Source:

/var/log/auth.log

Splunk Index:

security_lab

Sourcetype:

linux_secure

## MITRE ATT&CK Mapping

Primary Technique:

T1110 – Brute Force

Related Techniques include:

- Password Guessing
- Password Spraying
- Credential Access
- Valid Accounts

MITRE mapping enables organizations to understand detection coverage and identify gaps within their defensive capabilities.

## Threshold Design

Threshold selection significantly influences detection quality.

An overly sensitive detection generates excessive false positives.

An overly restrictive detection allows attacks to remain undetected.

Current laboratory threshold:

Any failed password event.

Future production threshold:

Five or more failed authentication attempts from the same source within five minutes.

Thresholds should always be validated against organizational behavior rather than arbitrary values.

## Severity Classification

Current laboratory severity:

Informational

Typical production severity:

Medium

Escalation factors include:

- Privileged accounts
- Multiple hosts
- Multiple usernames
- External source addresses
- High-value assets
- Repeated activity over time

Severity should reflect business risk rather than technical complexity.

## False Positives

Expected false positives include:

- Users entering incorrect passwords
- Password changes
- Administrative testing
- Vulnerability assessments
- Automation failures
- Newly deployed systems

Understanding expected false positives allows analysts to quickly distinguish routine activity from malicious behavior.

## Detection Tuning

Detection tuning improves operational effectiveness.

Examples include:

- Excluding approved management hosts
- Excluding vulnerability scanners
- Adjusting thresholds
- Suppressing duplicate alerts
- Incorporating business hours
- Prioritizing privileged accounts
- Incorporating threat intelligence
- Applying asset criticality

Detection tuning is an ongoing operational responsibility.

## Response Workflow

Analysts responding to this detection should:

Identify the source IP.

Identify the targeted account.

Determine affected systems.

Review authentication history.

Determine whether successful logins followed failed attempts.

Assess organizational risk.

Escalate according to incident response procedures when necessary.

## Operational Considerations

Detection engineering requires:

- Reliable telemetry
- Accurate timestamps
- Consistent field extraction
- Search performance
- Version control
- Documentation
- Regular validation
- Scheduled reviews

Operational ownership is as important as technical implementation.

## Security Considerations

Detection logic should be protected because it represents organizational defensive capability.

Considerations include:

- Least privilege
- Change management
- Version control
- Detection validation
- Audit logging
- Secure administrative access

Compromise of detection logic may reduce an organization's ability to identify attacks.

## Architecture Considerations

Security architects should evaluate:

- Telemetry quality
- Data normalization
- Search efficiency
- Detection scalability
- Index strategy
- Field extraction
- Retention policies
- Correlation capabilities
- Operational ownership
- Integration with incident response

Detection quality depends upon architectural decisions made long before alerts are generated.

## Tradeoffs

Highly sensitive detections increase visibility but generate additional false positives.

Highly restrictive detections reduce analyst workload but may miss legitimate attacks.

Architects must balance detection fidelity, operational cost, analyst workload, infrastructure performance, and organizational risk.

## Best Practices

- Design detections around attacker behavior rather than individual log messages.
- Validate detections using known events.
- Continuously tune thresholds.
- Document detection intent.
- Map detections to MITRE ATT&CK.
- Review detections regularly.
- Measure detection effectiveness.
- Version control detection logic.
- Treat detections as production software.
- Continuously improve based on operational experience.

## Interview Questions

### What is detection engineering?

Detection engineering is the process of designing, implementing, validating, tuning, and maintaining security detections that identify malicious activity while minimizing false positives.

### Why is a single failed login usually not sufficient to trigger an alert?

Individual authentication failures occur during normal operations. Effective detections focus on suspicious patterns rather than isolated events.

### Why is tuning important?

Without tuning, detections generate excessive false positives that reduce analyst confidence and increase operational workload.

### Why map detections to MITRE ATT&CK?

MITRE mapping provides a standardized method for measuring detection coverage, identifying defensive gaps, and communicating detection capabilities.

### What makes a detection production ready?

A production-quality detection includes validated logic, documented purpose, operational ownership, severity, tuning guidance, false positive analysis, response procedures, and continuous review.

## Lessons Learned

The authentication investigation demonstrated that detection engineering begins with understanding attacker behavior rather than memorizing search syntax.

Successful detections require high-quality telemetry, reliable ingestion, validated searches, and operational context.

Detection engineering transforms collected events into actionable security intelligence capable of supporting incident response and organizational risk reduction.

## Architect's Perspective

Security architects should view detections as strategic security capabilities rather than simple search queries.

An effective detection combines business objectives, operational processes, threat intelligence, telemetry quality, architecture, governance, and continuous improvement into a repeatable security capability.

Well-designed detections reduce organizational risk by identifying malicious behavior early while enabling analysts to focus their attention on activity that genuinely threatens the enterprise.

## Key Takeaways

- Detection engineering transforms telemetry into actionable security intelligence.
- Effective detections focus on attacker behavior rather than individual events.
- Business context is as important as technical implementation.
- Detection quality depends upon reliable telemetry and sound architecture.
- False positive reduction is a continuous process.
- MITRE ATT&CK improves detection maturity and coverage analysis.
- Detection engineering is an operational discipline requiring continuous improvement.
- Production detections should be treated as managed security assets.
