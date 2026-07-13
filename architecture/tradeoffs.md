# Architecture Tradeoffs

## Purpose

Architecture is the process of making informed decisions under constraints. Every technology choice introduces advantages and disadvantages. This document captures the reasoning behind key architectural decisions made throughout this project.

---

# Decision Evaluation Criteria

Each decision is evaluated using the project's Architecture Lens:

- Business Value
- Security
- Cost
- Operational Complexity
- Performance
- Scalability
- Maintainability
- Reliability & Resilience
- Vendor Lock-In
- Risk

---

# SIEM Platform

## Selected

Splunk Enterprise

## Alternatives Considered

- Wazuh
- Elastic Security
- Microsoft Sentinel
- Security Onion

### Benefits

- Industry-leading market recognition
- Extensive documentation
- Powerful SPL search language
- Strong dashboard capabilities
- Commonly encountered in enterprise environments

### Tradeoffs

- Commercial licensing
- Daily ingestion limits under the free license
- Higher resource requirements
- Vendor-specific search language

---

# Deployment Model

## Selected

Local Deployment

### Benefits

- No ongoing cloud costs
- Repeatable lab environment
- Safe experimentation
- Full administrative control

### Tradeoffs

- Limited scalability
- Does not fully represent distributed enterprise deployments

---

# Endpoint Coverage

## Selected

Windows + Ubuntu Linux

### Benefits

- Represents common enterprise operating systems
- Allows comparison of different log sources
- Demonstrates heterogeneous environment monitoring

### Tradeoffs

- Additional configuration effort
- Different logging models between platforms

---

# Documentation

## Selected

Architecture-first documentation

### Benefits

- Demonstrates architectural thinking
- Captures design rationale
- Supports interview discussions
- Improves maintainability

### Tradeoffs

- Additional upfront effort
- More documentation to maintain as the project evolves

---

Additional tradeoffs will be documented as the project progresses.
