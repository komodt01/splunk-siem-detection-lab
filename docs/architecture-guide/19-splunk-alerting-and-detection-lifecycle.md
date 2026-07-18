# 19. Splunk Alerting and Detection Lifecycle

## Purpose

This document explains how Splunk transforms a validated security search into an operational alert. It describes the alert lifecycle, scheduling model, trigger conditions, alert actions, tuning considerations, and architectural decisions involved in implementing automated detections.

The document is based on the failed SSH authentication detection created in this lab and demonstrates the progression from raw security telemetry to continuous security monitoring.

## Business Perspective

Manual searches are useful during investigations, but they do not provide continuous monitoring. An analyst cannot repeatedly search every security data source to determine whether suspicious activity has occurred.

Alerts automate this monitoring process by periodically evaluating security telemetry and notifying analysts when defined conditions are met.

From a business perspective, effective alerting helps organizations:

- Reduce mean time to detect
- Improve incident response speed
- Apply monitoring consistently
- Reduce dependence on manual review
- Identify suspicious activity earlier
- Support audit and compliance requirements
- Protect critical systems and identities
- Improve security operations efficiency

The objective is not to generate the greatest number of alerts. The objective is to generate timely, actionable alerts that help reduce organizational risk.

## What Is a Splunk Alert?

A Splunk alert is a saved search that runs automatically according to a defined schedule or in real time.

When the search meets a specified trigger condition, Splunk performs one or more configured actions.

Examples of alert actions include:

- Adding the alert to the Triggered Alerts list
- Sending an email
- Calling a webhook
- Running a script
- Writing an event to another index
- Creating a ticket
- Initiating a SOAR workflow
- Creating a notable event in Splunk Enterprise Security

An alert therefore combines search logic, execution timing, trigger criteria, and response actions into a reusable operational security capability.

## Why Alerts Are Different from Searches

A manual search answers a question at a specific moment.

For example:

```spl
index=security_lab sourcetype=linux_secure "Failed password"
