# SOC Automation Lab with AI Integration

## Objective

This project builds an automated SOC workflow that connects Splunk with AI analysis, threat intelligence feeds, malware scanning, and case management.

It focuses on taking a basic SIEM pipeline and extending it with automation and AI so security alerts can be enriched, analyzed, and routed with minimal manual effort. The goal is to show how modern SOCs can reduce repetitive work while improving investigation quality.

The stack combines Splunk for log analysis, N8N for automation, ChatGPT for contextual threat analysis, VirusTotal for malware detection, DFIR-IRIS for case management, and a Splunk MCP server for natural language SIEM queries.

---

## Skills Learned

- Configured Splunk Enterprise for centralized log collection and correlation  
- Built automated detection workflows in N8N to reduce manual Tier 1 alert triage  
- Used ChatGPT API for threat summaries and MITRE ATT&CK mapping  
- Enriched alerts using AbuseIPDB and VirusTotal for IP and file reputation data  
- Set up DFIR-IRIS for structured incident tracking and investigation workflows  
- Used Atomic Red Team to generate attack simulations and validate detections  
- Implemented a Splunk MCP server (livehybrid/splunk-mcp) for natural language querying in Claude Desktop  
- Built Slack integrations for real-time alerting to a SOC channel  
- Connected Windows, Linux, and cloud services into one automated workflow  
- Deployed N8N using Docker and managed the automation stack  
- Integrated multiple security APIs into a single workflow pipeline  

---

## Prerequisites

### Hardware Requirements

- A system with at least 16GB RAM (32GB preferred if running multiple VMs)  
- 4+ CPU cores with virtualization enabled  
- Around 200GB of free storage for virtual machines  

### Software Requirements

| Software | Description |
|----------|-------------|
| VMware Workstation Pro / VirtualBox | Used to run virtual machines |
| Windows 10 | Endpoint to generate security logs and simulate activity |
| Ubuntu Server 22.04 | Hosts Splunk, N8N, and DFIR-IRIS |
| Splunk Universal Forwarder | For forwarding logs from endpoints |
| Claude Desktop | Used for natural language SIEM queries through MCP |

### Tools and Platforms

| Tool | Description |
|------|-------------|
| Splunk Enterprise | SIEM used for log ingestion and correlation |
| N8N | Workflow automation tool used for SOC automation |
| OpenAI ChatGPT API | Provides AI-based threat analysis |
| AbuseIPDB | IP reputation and abuse scoring |
| VirusTotal | File and hash malware analysis |
| DFIR-IRIS | Incident response and case management platform |
| Splunk MCP Server | Enables natural language querying of Splunk |
| Atomic Red Team | Attack simulation framework |
| Slack | Used for SOC alert notifications |
| Docker & Docker Compose | Used to deploy N8N and supporting services |

---

## Workflow Overview

- Windows 10 generates authentication logs, including failed login attempts  
- Splunk Universal Forwarder sends logs to the Splunk indexer over port 9997  
- Splunk detects suspicious activity using correlation rules and triggers a webhook  
- N8N receives the alert and starts an automated workflow  
- ChatGPT analyzes the event and provides context, severity, and MITRE mapping  
- AbuseIPDB checks the source IP reputation and historical abuse data  
- VirusTotal scans any related file hashes for malware detection  
- DFIR-IRIS creates a structured incident case with all enriched data  
- Slack receives a formatted alert with analysis and investigation context  
- Analysts can query Splunk using natural language through the MCP server instead of SPL  

---

## Screenshots

### Architecture Diagram
![Architecture Overview](screenshots/architecture.png)
*End-to-end workflow from endpoint logs to Splunk, N8N automation, AI analysis, threat intelligence, case management, and Slack notifications*

### Splunk Configuration

*Splunk showing real-time log ingestion from Windows endpoints*
![Image Alt](link)

*Detection rule for failed logins with webhook trigger to N8N*
![Image Alt](link)

---

### N8N Workflow

*Full automation workflow handling parsing, enrichment, AI analysis, and alerting*
![Image Alt](link)

---

### AI Analysis

*ChatGPT output showing threat context and MITRE ATT&CK mapping*
![Image Alt](screenshots/chatgpt-output.png)

---

### Threat Intelligence

*AbuseIPDB IP reputation results showing abuse score and history*
![Image Alt](link)

*VirusTotal analysis showing malware detection across engines*
![Image Alt](link)

---

### DFIR-IRIS Case Management

*Incident automatically created in DFIR-IRIS with enriched context and timeline*
![Image Alt](link)

---

### Slack Alert

*SOC alert delivered with full enrichment and AI analysis*
![Image Alt](link)

---

### Conversational SIEM (MCP Server)

*Natural language query returning Splunk results without SPL*
![Image Alt](link)

---

## Conclusion

This project shows how a traditional SIEM setup can be extended into a more automated SOC workflow using AI and orchestration tools.

The system detects suspicious activity, enriches it with threat intelligence, runs malware analysis, and builds a structured incident case automatically. On top of that, it allows natural language querying of Splunk data, which makes investigation faster and more accessible.

Building this gave me hands-on experience with SIEM configuration, automation workflows, threat intelligence integration, and AI-assisted security analysis.

It also helped connect how different security tools can work together instead of operating in isolation, which is closer to how real SOC environments are structured.

---

<div align="center">
**Made with:** Splunk 🔍 | N8N ⚡ | ChatGPT 🤖 | AbuseIPDB 🛡️ | VirusTotal 🦠 | DFIR-IRIS 📋 | Claude MCP 💬
</div>
