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

*End-to-end workflow from endpoint logs to Splunk, N8N automation, AI analysis, threat intelligence, case management, and Slack notifications*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-Lab-AI-Integration/blob/b029d211d2848656aef13fae366d565816dd55f2/screenshots/Screenshot%202026-05-05%20113623.png)


---

### Splunk Configuration

*Splunk showing real-time log ingestion from Windows endpoints*  
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/beb5b0fb5692b142a67c8775f88c7a77790b1bd8/screenshots/Screenshot%202026-04-27%20111225.png)

*Detection rule for failed logins with webhook trigger to N8N*  
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/cd5d95a99869c0ab77c8518c5e47c05b2220ba31/screenshots/Screenshot%202026-04-27%20111527.png)

---

### N8N Workflow

*Full automation workflow handling parsing, enrichment, AI analysis, and alerting*  
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/d3eaa66fb64c3295308b07f58bfef966dc74bb44/screenshots/Screenshot%202026-05-02%20194738.png)

---

### AI Analysis

*ChatGPT output showing threat context*  
![ChatGPT Analysis Output](https://github.com/Samir-K9/SOC-Automation-2.0/blob/fed49dc12fc65091a28e993522a440acbc783344/screenshots/Screenshot%202026-05-03%20181034.png)

---

### Threat Intelligence

*AbuseIPDB IP reputation results showing abuse score and history*  
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/cd4e5584f6547304175f2eea20b443b36d31644c/screenshots/Screenshot%202026-05-02%20195358.png)

*VirusTotal analysis showing malware detection across engines*  
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/7a523633536720a3ebabafea87a91f2a4d212cae/screenshots/Screenshot%202026-05-02%20195801.png)

---

### DFIR-IRIS Case Management

*Incident automatically created in DFIR-IRIS with enriched context and timeline*  
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/c9e52bca6501307345d44267c0cc399617f9660a/screenshots/Screenshot%202026-05-02%20182824.png)

---

### Slack Alert

*SOC alert delivered with full enrichment and AI analysis*  
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/7289d0089ff91f99538097adeecbe3a7334a9894/screenshots/Screenshot%202026-04-27%20125337.png)

---

### Conversational SIEM (MCP Server)

*Natural language query returning Splunk results without SPL*  
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/446dd14d91d5455408aef9ee0b9df2b6301248df/screenshots/Windows%2010%20x64-2026-05-02-19-33-25.png)

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
