# SOC Automation Lab with AI Integration

## Objective

The SOC Automation Lab project demonstrates the integration of AI-powered threat analysis into traditional SIEM workflows with advanced malware detection, incident case management, and conversational AI capabilities. This project showcases how modern Security Operations Centers can leverage artificial intelligence, multi-source threat intelligence, and automated case management to enhance threat detection, automate incident response, and reduce analyst workload through intelligent automation. By combining Splunk's powerful log analysis capabilities with N8N workflow automation, ChatGPT's contextual analysis, VirusTotal's malware detection, DFIR-IRIS case management, and a custom Splunk MCP server for conversational SIEM querying, this lab simulates enterprise-grade SOC operations with cutting-edge efficiency.

### Skills Learned

- Developed advanced SIEM configuration skills using Splunk Enterprise for centralized log management and correlation.
- Implemented automated threat detection workflows using N8N, reducing manual investigation time by automating tier-1 analyst tasks.
- Integrated AI-powered threat analysis using OpenAI's ChatGPT API to provide context-aware security insights and MITRE ATT&CK framework mapping.
- Enhanced threat intelligence capabilities by incorporating multiple external feeds (AbuseIPDB for IP reputation, VirusTotal for file hash analysis) for comprehensive IOC enrichment.
- Configured automated incident case management using DFIR-IRIS platform for structured investigation workflows and evidence tracking.
- Utilized Atomic Red Team to simulate realistic attack scenarios and validate detection rule effectiveness.
-  Implemented MCP (Model Context Protocol) server (livehybrid/splunk-mcp) to enable conversational AI querying of SIEM data through Claude Desktop, eliminating the need for complex SPL syntax.
- Configured collaborative incident response workflows using Slack API for real-time security team notifications.
- Gained hands-on experience in orchestrating multi-platform security automation across Windows endpoints, Linux servers, cloud-based AI services, and case management platforms.
- Improved proficiency in containerization technologies (Docker) for deploying scalable automation platforms.
- Developed custom integration solutions combining multiple security APIs into unified automation workflows.

---

## Prerequisites

### Hardware Requirements

- A host machine with minimum 16GB RAM (32GB recommended) to support multiple VMs and their anticipated workloads.
- 4+ CPU cores with virtualization enabled.
- 200GB free disk space for VM storage.

### Software Requirements

| Software | Description |
|----------|-------------|
| **VMware Workstation Pro / VirtualBox** | Hypervisor platform for creating and managing virtual machines. |
| **Windows 10** | Client endpoint used to generate security event logs and simulate real-world threat scenarios. |
| **Ubuntu Server 22.04** | Linux distribution for hosting Splunk SIEM, N8N automation server and DFIR-IRIS for case management. |
| **Splunk Universal Forwarder** | Agent that collects and forwards Windows logs to the Splunk indexer. |
| **Claude Desktop** | AI assistant application for conversational SIEM querying via custom MCP server. |

### Tools and Platforms

| Tool | Description |
|------|-------------|
| **Splunk Enterprise** | Security Information and Event Management (SIEM) platform for log aggregation, correlation, and alerting. |
| **N8N** | Open-source workflow automation platform (SOAR-like capabilities) for orchestrating security response workflows. |
| **OpenAI ChatGPT API** | AI-powered analysis engine providing context-aware threat summaries and MITRE ATT&CK technique mapping. |
| **AbuseIPDB** | Threat intelligence platform providing IP reputation data and abuse confidence scoring. |
| **VirusTotal** | Malware detection and file reputation platform analyzing files across 70+ antivirus engines. |
| **DFIR-IRIS** | Digital Forensics and Incident Response platform for case management and investigation tracking. |
| **Splunk MCP Server** | Model Context Protocol server (livehybrid/splunk-mcp) enabling conversational AI access to Splunk SIEM data through Claude Desktop. |
| **Atomic Red Team** | Open-source library of tests mapped to MITRE ATT&CK framework used to generate realistic attack telemetry for testing detection rules. |
| **Slack** | Collaborative messaging platform for delivering formatted security alerts to SOC teams. |
| **Docker & Docker Compose** | Container runtime for deploying and managing the N8N automation server. |

---

## Workflow Overview

- **Log Generation:** Windows 10 endpoint generates security event logs (Event ID 4625 - Failed Logon Attempts) captured by Windows Event Logging.
- **Log Forwarding:** Splunk Universal Forwarder collects Security, System, and Application logs and forwards them to Splunk indexer over port 9997.
- **Alert Triggering:** Splunk SIEM correlates events based on custom detection rules and triggers webhook alerts to N8N when suspicious activity is detected.
- **Workflow Orchestration:** N8N receives alert via webhook, parses relevant data (IP addresses, usernames, file hashes), and initiates automated response workflow.
- **AI Analysis:** ChatGPT API analyzes the security event, provides threat context, severity assessment, and maps to MITRE ATT&CK techniques.
- **IP Threat Intelligence Enrichment:** AbuseIPDB API enriches source IP addresses with reputation scores, abuse history, and geolocation data.
- **File Hash Analysis:** VirusTotal API analyzes file hashes (SHA256) for malware detection across multiple antivirus engines and provides community reputation scores.
- **Case Management:** DFIR-IRIS automatically creates incident response cases with all enriched data, IOCs, and investigation context for centralized tracking.
- **Incident Notification:** Formatted alert with AI analysis, threat intelligence, malware analysis results, and DFIR-IRIS case reference is delivered to Slack channel for SOC analyst review and action.
- **Conversational SIEM Querying:** Custom Splunk MCP server enables security analysts to query SIEM data using natural language through Claude Desktop, eliminating the need for complex SPL syntax and accelerating investigation workflows.

---

## Screenshots

### Architecture Diagram
![Architecture Overview](screenshots/architecture.png)
*Complete workflow showing data flow from Windows endpoint through Splunk, N8N, AI analysis, threat intelligence, malware detection, case management, and Slack notification*

### Splunk Configuration

*Splunk Enterprise dashboard showing real-time log ingestion from Windows endpoint*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/beb5b0fb5692b142a67c8775f88c7a77790b1bd8/screenshots/Screenshot%202026-04-27%20111225.png)

*Detection rule configuration for Event ID 4625 with webhook trigger to N8N*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/cd5d95a99869c0ab77c8518c5e47c05b2220ba31/screenshots/Screenshot%202026-04-27%20111527.png)


### N8N Workflow Automation

*Full N8N workflow with all nodes: Webhook → Parse → ChatGPT → AbuseIPDB → VirusTotal → DFIR-IRIS → Format → Slack*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/d3eaa66fb64c3295308b07f58bfef966dc74bb44/screenshots/Screenshot%202026-05-02%20194738.png)


### AI-Powered Analysis
![ChatGPT Analysis Output](screenshots/chatgpt-output.png)
*ChatGPT-generated threat analysis with MITRE ATT&CK mapping and recommended actions*

### Threat Intelligence

*IP reputation data from AbuseIPDB showing abuse confidence score and historical reports*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/cd4e5584f6547304175f2eea20b443b36d31644c/screenshots/Screenshot%202026-05-02%20195358.png)


*File hash analysis via VirusTotal showing malware detection across multiple antivirus engines*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/7a523633536720a3ebabafea87a91f2a4d212cae/screenshots/Screenshot%202026-05-02%20195801.png)

### DFIR-IRIS Case Management

*Enriched security alert forwarded to DFIR-IRIS for centralized case management with full event context and investigation timeline*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/c9e52bca6501307345d44267c0cc399617f9660a/screenshots/Screenshot%202026-05-02%20182824.png)

### Slack Alert Delivery

*Formatted security alert delivered to SOC team with event details, MITRE ATT&CK mapping, IP reputation, malware analysis, DFIR-IRIS case reference, and AI recommendations*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/7289d0089ff91f99538097adeecbe3a7334a9894/screenshots/Screenshot%202026-04-27%20125337.png)

### Conversational SIEM (Splunk MCP Server)

*Natural language query to Splunk via Claude Desktop using custom MCP server integration*
![Splunk MCP Query](screenshots/splunk-mcp-query.png)

*Structured SIEM results returned through conversational AI interface without requiring SPL syntax*
![Splunk MCP Results](screenshots/splunk-mcp-results.png)


### Testing and Validation
![Test Events Generated](screenshots/test-events.png)
*Windows Event Viewer showing generated Event ID 4625 failed logon attempts*

![End-to-End Test Success](screenshots/end-to-end-test.png)
*Complete workflow execution from event generation to Slack notification with all enrichments*

---

## Conclusion

This advanced SOC Automation Lab successfully demonstrates the integration of AI-powered analysis, multi-source threat intelligence, malware detection, automated case management, and conversational SIEM querying into traditional security workflows. By combining Splunk's robust log analysis capabilities with N8N's flexible workflow automation, ChatGPT's contextual threat analysis, AbuseIPDB's IP reputation data, VirusTotal's malware detection, DFIR-IRIS case management, and an MCP server integration (livehybrid/splunk-mcp) for natural language querying, we've built an enterprise-grade system that significantly reduces manual investigation time while enhancing the quality and depth of security insights.

The workflow automatically detects suspicious authentication attempts, enriches them with comprehensive threat intelligence from multiple sources, performs malware analysis on associated file hashes, creates structured incident response cases, applies AI-driven analysis including MITRE ATT&CK framework mapping, and delivers actionable alerts to security teams via Slack. Additionally, the custom Splunk MCP server enables security analysts to query SIEM data using natural language, eliminating the learning curve of SPL syntax and accelerating investigation workflows.

Through this project, we've gained practical hands-on experience in:
- Configuring enterprise SIEM platforms (Splunk) for centralized log management
- Implementing detection rules and correlation logic for threat identification
- Building complex automated security workflows using orchestration platforms (N8N)
- Integrating AI services to enhance threat analysis and reduce false positives
- Enriching security events with multiple external threat intelligence feeds (IP and file-based)
- Implementing automated malware analysis workflows
- Deploying incident response case management platforms for investigation tracking
- Implementing MCP servers for AI-powered conversational access to security data
- Delivering contextualized alerts to security teams through collaborative platforms

This foundational knowledge enables us to design, implement, and manage automated SOC workflows in production environments, accelerate incident response times, optimize security operations through intelligent automation and AI integration, and build custom solutions that bridge the gap between security tools and AI-powered analysis platforms.

---

<div align="center">
**Made with:** Splunk 🔍 | N8N ⚡ | ChatGPT 🤖 | AbuseIPDB 🛡️ | VirusTotal 🦠 | DFIR-IRIS 📋 | Claude MCP 💬

</div>
