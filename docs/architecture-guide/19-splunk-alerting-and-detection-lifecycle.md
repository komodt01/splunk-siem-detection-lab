# 19. Splunk Alerting and Detection Lifecycle

## Purpose

This document explains how Splunk transforms a search into an operational security detection through scheduled alerts. It describes the alert lifecycle, architectural decisions, production considerations, and the business value of implementing reliable, repeatable detections within a Security Operations Center (SOC).

## What Is a Splunk Alert?

A Splunk alert is a scheduled or real-time search that continuously evaluates incoming data and performs one or more actions when defined conditions are met. Alerts extend the value of Search Processing Language (SPL) by moving beyond manual investigations to automated detection of security events.

In this lab, the first alert detects failed SSH authentication attempts from Linux authentication logs ingested into the `security_lab` index.

## Why It Is Important

Searching data manually is effective for investigations but does not scale for continuous monitoring. Security teams require automated detections that identify suspicious behavior as it occurs. Alerts reduce the time required to discover security events, improve consistency, and allow analysts to focus on validating and responding to meaningful activity.

A mature SIEM depends on reliable alerts that balance detection coverage with manageable operational workload.

## Alert Lifecycle

The detection lifecycle implemented during this project follows a structured progression.

1. Generate security-relevant activity.
2. Verify successful log ingestion.
3. Validate field extraction.
4. Develop an SPL query.
5. Test the query against known events.
6. Save the query as a reusable report.
7. Promote the report to a scheduled alert.
8. Configure trigger conditions.
9. Configure trigger actions.
10. Validate alert execution.
11. Tune the detection to reduce false positives.
12. Deploy into production monitoring.

Each stage builds confidence before operationalizing a detection.

## Scheduled vs. Real-Time Alerts

Splunk supports both scheduled and real-time alerts.

Scheduled alerts execute at defined intervals and evaluate events occurring within a specified search window. This approach provides predictable resource utilization and is appropriate for most production security monitoring.

Real-time alerts continuously evaluate incoming events and provide the lowest detection latency. However, they consume more system resources and require careful tuning to avoid excessive alert volume.

This project intentionally uses scheduled alerts because they represent the most common enterprise deployment model.

## Alert Configuration

The first detection was configured using the following design decisions.

Alert Type:
Scheduled

Search Interval:
Every five minutes

Search Window:
Previous five minutes

Trigger Condition:
Number of results greater than zero

Trigger Frequency:
Once

Trigger Action:
Add to Triggered Alerts

These settings provide continuous monitoring while avoiding overlapping execution windows.

## Why This Configuration Was Selected

The objective of this configuration is to create a repeatable operational detection while minimizing unnecessary processing overhead.

Running the search every five minutes provides near-real-time visibility without the cost of continuous execution. Searching the previous five minutes ensures that newly ingested authentication failures are evaluated during each execution cycle.

Triggering only once prevents repeated notifications for identical search results.

## Detection Engineering Considerations

A useful detection must be accurate, understandable, maintainable, and operationally practical.

Detection engineering involves more than writing SPL. Analysts must understand attacker behavior, logging characteristics, field availability, search performance, and alert fatigue.

Each detection should have a clearly defined purpose, expected behavior, documented assumptions, and validation procedures.

## Security Considerations

Authentication failures often represent one of the earliest indicators of malicious activity.

Potential scenarios include:

- Password guessing
- Credential stuffing
- Automated brute-force attacks
- Unauthorized administrative access
- Reconnaissance activity
- Misconfigured automation

Alerts should be correlated with additional telemetry before declaring an incident.

## Operational Considerations

Production alerting requires continuous maintenance.

Security teams should periodically review:

- False positive rates
- Search execution time
- Alert frequency
- Detection coverage
- Logging completeness
- Data quality
- Infrastructure performance

Alerts that generate excessive noise reduce analyst effectiveness and increase the likelihood of important events being ignored.

## Architecture Considerations

Detection architecture should separate data ingestion, search logic, alerting, dashboards, and incident response workflows.

Alerts should be modular, reusable, and independent of individual dashboards whenever possible.

Searches should also leverage normalized data models and consistent field naming to simplify future expansion into enterprise-scale environments.

## Tradeoffs

Scheduled alerts reduce infrastructure utilization but introduce small detection delays.

Real-time alerts improve responsiveness but consume additional processing resources.

Highly sensitive detections may justify real-time monitoring, whereas lower-risk detections typically benefit from scheduled execution.

The appropriate balance depends on organizational risk tolerance, available infrastructure, and operational staffing.

## Best Practices

- Validate searches before enabling alerts.
- Use meaningful alert names and descriptions.
- Keep trigger logic simple and understandable.
- Tune detections using real operational data.
- Reduce false positives before production deployment.
- Document assumptions and expected behavior.
- Review alerts regularly for continued effectiveness.
- Build detections incrementally rather than attempting to monitor every possible event immediately.

## Interview Questions

Why would you choose a scheduled alert instead of a real-time alert?

How would you reduce false positives in an authentication detection?

How would you prioritize authentication alerts in a SOC?

How would you validate that a new detection is functioning correctly?

How would you scale hundreds of alerts across an enterprise SIEM?

## Lessons Learned

Building an effective alert requires considerably more than writing an SPL query.

Successful detections depend on reliable data ingestion, accurate field extraction, thoughtful search design, appropriate scheduling, operational validation, and continuous tuning.

The complete lifecycle demonstrates how SIEM platforms transform raw log data into actionable security intelligence.

## Architect's Perspective

From an architectural perspective, alerting represents the transition from passive visibility to active security operations.

A well-designed detection should be reliable, explainable, maintainable, and aligned with business risk rather than simply generating notifications.

The objective is not to create the largest number of alerts but to build a small set of high-confidence detections that consistently identify meaningful security events while minimizing operational overhead. This philosophy improves analyst productivity, reduces alert fatigue, and creates a scalable foundation for enterprise detection engineering.
