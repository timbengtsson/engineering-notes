# Security Operations

This section focuses on the operational side of IT security. That is protecting, monitoring, and responding to threats in *running systems*.<br>

While design and architecture aim to prevent issues, operational security assumes that failures, misconfigurations, and attacks will happen. <br>
The goal is to detect them early, limit impact, and respond effectively.

---

## Purpose

Security operations is where the rubber meets the road and theory meets reality.<br>

This area covers:
- Visibility into system behavior
- Early detection of suspicious activity
- Reducing attack surface through hardening
- Responding to incidents in a structured and calm way
- Learning from incidents to improve future defenses

The focus is primarily defensive (blue team–oriented), but with an understanding of attacker techniques.

---

## Areas Covered

### Log Monitoring & Analysis
Understanding what to log, where logs live, and how to read them:
- Authentication and authorization events
- System and service logs
- Application logs
- Identifying anomalies and indicators of compromise

### System Hardening
Reducing attack surface through:
- File permissions and ownership
- Service configuration
- Secure defaults
- Auditing and monitoring critical system changes

### Monitoring & Alerting
Detecting issues before they become incidents:
- Centralized logging
- Host-based intrusion detection
- Rate-limiting and brute-force protection
- Alert fatigue and signal-to-noise considerations

### Incident Response
Handling security incidents in a controlled way:
- Triage and initial assessment
- Log-based investigation
- Containment and recovery
- Post-incident review and improvement

---

## Contents
- [Log Monitoring](./log-monitoring.md)
- System Hardening *(planned)*
- Monitoring & Alerting *(planned)*
- Incident Response *(planned)*

---

## Mindset
Operational security is not about reacting emotionally to alerts.<br>
It is about preparation, visibility, and making informed decisions under pressure.

---

## Questions to Ponder
- Do we have a documented incident response plan?
- Do we know who is responsible during a security incident?
- Do we have a backup strategy, and has recovery been tested?
- How quickly can we detect abnormal or malicious behavior?
- Do we know [which logs are critical and where they are stored](./log-monitoring.md#logs-of-interest)?
- What systems or data would cause the most damage if compromised? 
- Are access rights reviewed and adjusted over time?
- How would we notice if credentials were leaked or abused?
- Are alerts actionable, or are we generating noise?