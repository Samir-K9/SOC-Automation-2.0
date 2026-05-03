# SOC Automation Lab with AI Integration

## Objective

The SOC Automation Lab project demonstrates the integration of AI-powered threat analysis into traditional SIEM workflows. This project showcases how modern Security Operations Centers can leverage artificial intelligence to enhance threat detection, automate incident response, and reduce analyst workload through intelligent automation. By combining Splunk's powerful log analysis capabilities with N8N workflow automation and ChatGPT's contextual analysis, this lab simulates real-world SOC operations with enhanced efficiency.

### Skills Learned

- Developed advanced SIEM configuration skills using Splunk Enterprise for centralized log management and correlation.
- Implemented automated threat detection workflows using N8N, reducing manual investigation time by automating tier-1 analyst tasks.
- Integrated AI-powered threat analysis using OpenAI's ChatGPT API to provide context-aware security insights and MITRE ATT&CK framework mapping.
- Enhanced threat intelligence capabilities by incorporating external feeds (AbuseIPDB) for IOC enrichment and reputation scoring.
- Configured collaborative incident response workflows using Slack API for real-time security team notifications.
- Gained hands-on experience in orchestrating multi-platform security automation across Windows endpoints, Linux servers, and cloud-based AI services.
- Improved proficiency in containerization technologies (Docker) for deploying scalable automation platforms.

---

## Prerequisites

### Hardware Requirements

- A host machine with minimum 16GB RAM (32GB recommended) to support multiple VMs and their anticipated workloads.
- 4+ CPU cores with virtualization enabled (Intel VT-x/AMD-V).
- 200GB free disk space for VM storage and log retention.

### Software Requirements

| Software | Description |
|----------|-------------|
| **VMware Workstation Pro / VirtualBox** | Hypervisor platform for creating and managing virtual machines. |
| **Windows 10** | Client endpoint used to generate security event logs and simulate real-world threat scenarios. |
| **Ubuntu Server 22.04** | Linux distribution for hosting Splunk SIEM and N8N automation server. |
| **Splunk Universal Forwarder** | Agent that collects and forwards Windows logs to the Splunk indexer. |

### Tools and Platforms

| Tool | Description |
|------|-------------|
| **Splunk Enterprise** | Security Information and Event Management (SIEM) platform for log aggregation, correlation, and alerting. |
| **N8N** | Open-source workflow automation platform (SOAR-like capabilities) for orchestrating security response workflows. |
| **OpenAI ChatGPT API** | AI-powered analysis engine providing context-aware threat summaries and MITRE ATT&CK technique mapping. |
| **AbuseIPDB** | Threat intelligence platform providing IP reputation data and abuse confidence scoring. |
| **Slack** | Collaborative messaging platform for delivering formatted security alerts to SOC teams. |
| **Docker & Docker Compose** | Container runtime for deploying and managing the N8N automation server. |

---

## Workflow Overview
- **Log Generation:** Windows 10 endpoint generates security event logs (Event ID 4625 - Failed Logon Attempts) captured by Windows Event Logging.
- **Log Forwarding:** Splunk Universal Forwarder collects Security, System, and Application logs and forwards them to Splunk indexer over port 9997.
- **Alert Triggering:** Splunk SIEM correlates events based on custom detection rules and triggers webhook alerts to N8N when suspicious activity is detected.
- **Workflow Orchestration:** N8N receives alert via webhook, parses relevant data, and initiates automated response workflow.
- **AI Analysis:** ChatGPT API analyzes the security event, provides threat context, severity assessment, and maps to MITRE ATT&CK techniques.
- **Threat Intelligence Enrichment:** AbuseIPDB API enriches source IP addresses with reputation scores and abuse history.
- **Incident Notification:** Formatted alert with AI analysis and threat intelligence is delivered to Slack channel for SOC analyst review and action.

---

## Screenshots

### Architecture Diagram
![Architecture Overview](screenshots/architecture.png)
*Complete workflow showing data flow from Windows endpoint through Splunk, N8N, AI analysis, and Slack notification*

### Splunk Configuration

*Splunk Enterprise dashboard showing real-time log ingestion from Windows endpoint*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/beb5b0fb5692b142a67c8775f88c7a77790b1bd8/screenshots/Screenshot%202026-04-27%20111225.png)

*Detection rule configuration for Event ID 4625 with webhook trigger to N8N*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/cd5d95a99869c0ab77c8518c5e47c05b2220ba31/screenshots/Screenshot%202026-04-27%20111527.png)


### N8N Workflow Automation

*Full N8N workflow with all nodes with successful execution*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/d3eaa66fb64c3295308b07f58bfef966dc74bb44/screenshots/Screenshot%202026-05-02%20194738.png)


### AI-Powered Analysis
![ChatGPT Analysis Output](screenshots/chatgpt-output.png)
*ChatGPT-generated threat analysis with MITRE ATT&CK mapping and recommended actions*

### Threat Intelligence

*IP reputation data from AbuseIPDB*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/cd4e5584f6547304175f2eea20b443b36d31644c/screenshots/Screenshot%202026-05-02%20195358.png)


*File hash analysis via VirusTotal*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/7a523633536720a3ebabafea87a91f2a4d212cae/screenshots/Screenshot%202026-05-02%20195801.png)

### DFIR IRIS Alert Ingestion

*Enriched security alert forwarded to DFIR IRIS for centralized case management with event context*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/c9e52bca6501307345d44267c0cc399617f9660a/screenshots/Screenshot%202026-05-02%20182824.png)

### Slack Alert Delivery

*Formatted security alert delivered to SOC team with event details, MITRE ATT&CK mapping, threat intelligence and AI analysis*
![Image Alt](https://github.com/Samir-K9/SOC-Automation-2.0/blob/7289d0089ff91f99538097adeecbe3a7334a9894/screenshots/Screenshot%202026-04-27%20125337.png)


### Testing and Validation
![Test Events Generated](screenshots/test-events.png)
*Windows Event Viewer showing generated Event ID 4625 failed logon attempts*

![End-to-End Test Success](screenshots/end-to-end-test.png)
*Complete workflow execution from event generation to Slack notification*

---

## Conclusion

This SOC Automation Lab successfully demonstrates the integration of AI-powered analysis into traditional SIEM workflows, creating an intelligent, automated security operations pipeline. By combining Splunk's robust log analysis capabilities with N8N's flexible workflow automation and ChatGPT's contextual threat analysis, we've built a system that significantly reduces manual investigation time while enhancing the quality of security insights.

The workflow automatically detects suspicious authentication attempts, enriches them with threat intelligence, applies AI-driven analysis including MITRE ATT&CK framework mapping, and delivers actionable alerts to security teams via Slack. This approach simulates real-world SOC automation techniques used by modern security operations centers to handle high-volume security events efficiently.

Through this project, we've gained practical hands-on experience in:
- Configuring enterprise SIEM platforms (Splunk) for centralized log management
- Implementing detection rules and correlation logic for threat identification
- Building automated security workflows using orchestration platforms (N8N)
- Integrating AI services to enhance threat analysis and reduce false positives
- Enriching security events with external threat intelligence feeds
- Delivering contextualized alerts to security teams through collaborative platforms


![GitHub stars](https://img.shields.io/github/stars/yourusername/soc-automation-lab?style=social)
![GitHub forks](https://img.shields.io/github/forks/yourusername/soc-automation-lab?style=social)

*Built with ☕ and 🔐 for the cybersecurity community*

</div>
