# 🛡️ SOC Automation Project: AI-Powered Security Operations

An end-to-end Security Operations Center (SOC) automation workflow that demonstrates real-world SIEM integration, threat detection, and AI-enhanced incident response. This project showcases proficiency in security monitoring, automation engineering, and modern DevSecOps practices.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/Platform-VMware%20%7C%20VirtualBox-blue)]()
[![SIEM](https://img.shields.io/badge/SIEM-Splunk-green)]()

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Architecture](#-architecture)
- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [Prerequisites](#-prerequisites)
- [Installation & Setup](#-installation--setup)
  - [VM Configuration](#1-virtual-machine-setup)
  - [Splunk Installation](#2-splunk-installation--configuration)
  - [Log Forwarding](#3-windows-log-forwarding)
  - [Alert Configuration](#4-splunk-alert-creation)
  - [N8N Automation](#5-n8n-workflow-automation)
  - [AI Integration](#6-chatgpt-integration)
  - [Threat Intelligence](#7-threat-intelligence-enrichment)
  - [Slack Notifications](#8-slack-integration)
- [Testing & Validation](#-testing--validation)
- [Screenshots](#-screenshots)
- [Future Enhancements](#-future-enhancements)
- [Security Considerations](#-security-considerations)
- [Lessons Learned](#-lessons-learned)
- [References](#-references)
- [License](#-license)

---

## 🎯 Overview

This project demonstrates an automated SOC workflow that:

1. **Collects** Windows security logs from a monitored endpoint
2. **Detects** suspicious activities using Splunk SIEM
3. **Triggers** automated workflows via N8N
4. **Analyzes** threats using ChatGPT API with MITRE ATT&CK mapping
5. **Enriches** IOCs using threat intelligence feeds (AbuseIPDB)
6. **Notifies** security teams via Slack with actionable insights

**Real-World Application:** Reduces mean time to detect (MTTD) and mean time to respond (MTTR) by automating tier-1 analyst tasks, allowing SOC teams to focus on complex investigations.

---

## 🏗️ Architecture

```
┌─────────────────┐
│   Windows 10    │
│   (Endpoint)    │
│                 │
│  Event Logs:    │
│  - Security     │
│  - System       │
│  - Application  │
└────────┬────────┘
         │
         │ Splunk Universal Forwarder
         │ Port: 9997
         │
         ▼
┌─────────────────┐
│  Splunk SIEM    │
│  (Ubuntu VM)    │
│                 │
│  - Log ingestion│
│  - Correlation  │
│  - Alert Rules  │
└────────┬────────┘
         │
         │ Webhook Trigger
         │ (EventCode 4625 - Failed Login)
         │
         ▼
┌─────────────────┐
│   N8N Workflow  │
│   (Ubuntu VM)   │
│                 │
│  Orchestration: │
│  ┌──────────┐   │
│  │ Webhook  │   │
│  └────┬─────┘   │
│       │         │
│       ▼         │
│  ┌──────────┐   │
│  │ ChatGPT  │   │
│  │ Analysis │   │
│  └────┬─────┘   │
│       │         │
│       ▼         │
│  ┌──────────┐   │
│  │AbuseIPDB │   │
│  │   API    │   │
│  └────┬─────┘   │
│       │         │
│       ▼         │
│  ┌──────────┐   │
│  │  Slack   │   │
│  │  Alert   │   │
│  └──────────┘   │
└─────────────────┘
         │
         ▼
    📱 Slack Channel
    (Formatted Alert)
```

---

## ✨ Features

- ✅ **Real-Time Threat Detection**: Monitors Windows security events (Event ID 4625 - Failed Logon Attempts)
- ✅ **Automated Incident Response**: Zero-touch workflow from detection to notification
- ✅ **AI-Powered Analysis**: ChatGPT provides context-aware threat summaries and MITRE ATT&CK mapping
- ✅ **Threat Intelligence Enrichment**: Automated IP reputation checks via AbuseIPDB
- ✅ **Collaborative Alerts**: Formatted Slack notifications with severity scoring and recommended actions
- ✅ **Scalable Architecture**: Containerized N8N deployment for easy replication
- ✅ **Cost-Effective**: Uses open-source tools and minimal API costs (~$5)

---

## 🛠️ Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **SIEM** | Splunk Enterprise | Log aggregation, correlation, alerting |
| **Endpoint** | Windows 10 | Log source (Security, System, Application) |
| **Automation** | N8N (Docker) | Workflow orchestration |
| **AI Analysis** | OpenAI GPT-4 | Threat analysis and contextualization |
| **Threat Intel** | AbuseIPDB API | IP reputation and abuse history |
| **Notifications** | Slack API | Team collaboration and alerting |
| **Virtualization** | VMware Workstation Pro | Lab environment |
| **OS** | Ubuntu Server 22.04 | Hosting Splunk and N8N |

---

## 📦 Prerequisites

### Hardware Requirements
- **RAM**: 16 GB minimum (32 GB recommended)
- **CPU**: 4+ cores
- **Storage**: 200 GB free disk space
- **Hypervisor**: VMware Workstation Pro or VirtualBox

### Software & Accounts
- [ ] VMware Workstation Pro (or VirtualBox)
- [ ] Windows 10 ISO
- [ ] Ubuntu Server 22.04 ISO
- [ ] Splunk Enterprise (free trial/dev license)
- [ ] OpenAI API account with credits ($5 minimum)
- [ ] AbuseIPDB API key (free tier)
- [ ] Slack workspace (free)

### Knowledge Prerequisites
- Basic Linux command line
- Networking fundamentals (TCP/IP, ports)
- Windows Event Logs basics
- SIEM concepts (log parsing, correlation rules)

---

## 🚀 Installation & Setup

### 1. Virtual Machine Setup

#### Create VMs with the following specifications:

| VM Name | OS | vCPU | RAM | Disk | Network |
|---------|-----|------|-----|------|---------|
| **Windows-SOC-Lab** | Windows 10 | 2 | 4 GB | 50 GB | NAT |
| **Splunk-Server** | Ubuntu Server 22.04 | 2 | 8 GB | 100 GB | NAT |
| **N8N-Automation** | Ubuntu Server 22.04 | 2 | 4 GB | 50 GB | NAT |

#### Post-Installation:

**Windows VM:**
```powershell
# Enable Remote Desktop (optional)
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -Name "fDenyTSConnections" -Value 0

# Note the IP address
ipconfig
```

**Ubuntu VMs:**
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install SSH (if not already)
sudo apt install openssh-server -y

# Note the IP address
ip addr show
```

#### Verify Network Connectivity:
```bash
# From Windows VM, ping Splunk server
ping <SPLUNK_IP>

# From N8N VM, ping Splunk server
ping <SPLUNK_IP>
```

---

### 2. Splunk Installation & Configuration

#### Install Splunk Enterprise

```bash
# Download Splunk (replace URL with latest version)
wget -O splunk.deb "https://download.splunk.com/products/splunk/releases/9.1.2/linux/splunk-9.1.2-b6b9c8185839-linux-2.6-amd64.deb"

# Install
sudo dpkg -i splunk.deb

# Navigate to Splunk bin
cd /opt/splunk/bin

# Start Splunk and accept license
sudo ./splunk start --accept-license

# Enable boot-start
sudo ./splunk enable boot-start
```

#### Access Splunk Web Interface
- URL: `http://<SPLUNK_IP>:8000`
- Default credentials will be set during first login

#### Configure Data Receiving

1. **Settings** → **Forwarding and receiving**
2. **Configure receiving** → **New Receiving Port**
3. Port: `9997` → **Save**

#### Create Index

1. **Settings** → **Indexes**
2. **New Index**
   - Index name: `mydfir-project`
   - **Save**

#### Install Windows Add-on

1. **Apps** → **Find More Apps**
2. Search: "Splunk Add-on for Microsoft Windows"
3. **Install**
4. Restart Splunk

---

### 3. Windows Log Forwarding

#### Install Splunk Universal Forwarder on Windows VM

1. Download from: https://www.splunk.com/en_us/download/universal-forwarder.html
2. Run installer
3. Configuration:
   - Deployment server: `<SPLUNK_IP>:8089`
   - Receiving indexer: `<SPLUNK_IP>:9997`

#### Configure inputs.conf

Navigate to: `C:\Program Files\SplunkUniversalForwarder\etc\system\local\`

Create/edit `inputs.conf`:

```ini
[WinEventLog://Security]
disabled = 0
index = mydfir-project

[WinEventLog://System]
disabled = 0
index = mydfir-project

[WinEventLog://Application]
disabled = 0
index = mydfir-project

[WinEventLog://Microsoft-Windows-TerminalServices-RemoteConnectionManager/Operational]
disabled = 0
index = mydfir-project
renderXml = true
```

#### Restart Splunk Universal Forwarder

```powershell
# Via Services or PowerShell
Restart-Service SplunkForwarder
```

#### Verify Log Ingestion

In Splunk Web → **Search & Reporting**:

```spl
index=mydfir-project
| stats count by source
```

You should see events from Security, System, Application logs.

---

### 4. Splunk Alert Creation

#### Create Detection Rule for Failed Logins

**Search Query:**
```spl
index=mydfir-project EventCode=4625
| stats count by _time, ComputerName, user, src_ip
| where count > 3
```

**Explanation:**
- `EventCode=4625`: Windows failed logon attempts
- Groups by time, computer, user, and source IP
- Filters for more than 3 attempts (basic threshold)

#### Save as Alert

1. **Save As** → **Alert**
2. **Title**: `Failed Login Attempts Detected`
3. **Alert type**: **Real-time** or **Scheduled** (every 1 minute)
4. **Trigger conditions**: Per-Result (each result triggers alert)
5. **Trigger actions**:
   - Add action: **Webhook**
   - URL: `http://<N8N_IP>:5678/webhook/<YOUR_WEBHOOK_PATH>` (will create in next step)
6. **Save**

---

### 5. N8N Workflow Automation

#### Install Docker and Docker Compose

```bash
# Install Docker
sudo apt install docker.io -y

# Install Docker Compose
sudo apt install docker-compose -y

# Add user to docker group
sudo usermod -aG docker $USER

# Re-login for group changes
exit
```

#### Create Docker Compose File

```bash
mkdir -p ~/n8n
cd ~/n8n
nano docker-compose.yml
```

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  n8n:
    image: n8nio/n8n
    restart: always
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=changeme123
    volumes:
      - n8n_data:/home/node/.n8n

volumes:
  n8n_data:
```

#### Start N8N

```bash
sudo docker-compose up -d

# Check logs
sudo docker-compose logs -f
```

#### Access N8N

- URL: `http://<N8N_IP>:5678`
- Login with credentials from docker-compose.yml

#### Create Workflow

1. **New Workflow**
2. Add nodes in this order:

**Node 1: Webhook**
- Trigger node
- HTTP Method: `POST`
- Path: `splunk-alert`
- Copy the webhook URL (format: `http://<N8N_IP>:5678/webhook/splunk-alert`)

**Node 2: Function (Parse Splunk Data)**
```javascript
// Extract relevant fields from Splunk webhook
const splunkData = $input.item.json.result;

return {
  json: {
    timestamp: splunkData._time,
    computer: splunkData.ComputerName,
    username: splunkData.user,
    sourceIP: splunkData.src_ip,
    failureCount: splunkData.count,
    rawData: splunkData
  }
};
```

**Configure remaining nodes in next sections...**

---

### 6. ChatGPT Integration

#### Get OpenAI API Key

1. Visit: https://platform.openai.com/api-keys
2. Create new secret key
3. Add $5 credit to account

#### Add to N8N Workflow

**Node 3: OpenAI (ChatGPT)**

**Credentials:**
- Add new OpenAI credential
- Paste API key

**Settings:**
- Resource: `Chat`
- Operation: `Message a Model`
- Model: `gpt-4` (or `gpt-3.5-turbo` for lower cost)

**Prompt (System Message):**
```
You are a cybersecurity analyst specializing in threat detection and incident response. 

Analyze the following failed login event and provide:
1. A concise summary of the incident
2. Severity assessment (Critical/High/Medium/Low)
3. MITRE ATT&CK technique mapping
4. Recommended immediate actions
5. Indicators of Compromise (IOCs)

Format your response in clear sections with markdown.
```

**User Message:**
```
Failed Login Event Details:
- Timestamp: {{ $json.timestamp }}
- Computer: {{ $json.computer }}
- Username: {{ $json.username }}
- Source IP: {{ $json.sourceIP }}
- Failure Count: {{ $json.failureCount }}

Analyze this event and provide security recommendations.
```

---

### 7. Threat Intelligence Enrichment

#### Get AbuseIPDB API Key

1. Register at: https://www.abuseipdb.com/
2. Navigate to **API** section
3. Copy your API key

#### Add to N8N Workflow

**Node 4: HTTP Request (AbuseIPDB)**

**Settings:**
- Method: `GET`
- URL: `https://api.abuseipdb.com/api/v2/check`

**Query Parameters:**
```
ipAddress: {{ $('Function').item.json.sourceIP }}
maxAgeInDays: 90
verbose: true
```

**Headers:**
```
Key: Accept
Value: application/json

Key: Key
Value: YOUR_ABUSEIPDB_API_KEY
```

**Node 5: Function (Format Threat Intel)**
```javascript
const ipCheck = $input.item.json.data;
const chatGPTResponse = $('OpenAI').item.json.message.content;

return {
  json: {
    aiAnalysis: chatGPTResponse,
    threatIntel: {
      ip: ipCheck.ipAddress,
      abuseScore: ipCheck.abuseConfidenceScore,
      isWhitelisted: ipCheck.isWhitelisted,
      countryCode: ipCheck.countryCode,
      usageType: ipCheck.usageType,
      isp: ipCheck.isp,
      totalReports: ipCheck.totalReports
    }
  }
};
```

---

### 8. Slack Integration

#### Setup Slack App

1. Go to: https://api.slack.com/apps
2. **Create New App** → **From scratch**
3. App name: `SOC Alerts`
4. Pick your workspace

**OAuth & Permissions:**
- Add scopes:
  - `chat:write`
  - `channels:read`
- **Install to Workspace**
- Copy **Bot User OAuth Token**

#### Create Slack Channel

1. Create channel: `#soc-alerts`
2. Invite the bot: `/invite @SOC Alerts`

#### Add to N8N Workflow

**Node 6: Slack**

**Credentials:**
- Add Slack OAuth credential
- Paste Bot User OAuth Token

**Settings:**
- Resource: `Message`
- Operation: `Post`
- Channel: `#soc-alerts`

**Message Text:**
```
🚨 *SECURITY ALERT: Failed Login Attempts Detected*

*Event Details:*
• Timestamp: {{ $('Function').item.json.timestamp }}
• Computer: {{ $('Function').item.json.computer }}
• Username: {{ $('Function').item.json.username }}
• Source IP: {{ $('Function').item.json.sourceIP }}
• Failure Count: {{ $('Function').item.json.failureCount }}

*Threat Intelligence:*
• Abuse Confidence Score: {{ $('Function 1').item.json.threatIntel.abuseScore }}%
• Country: {{ $('Function 1').item.json.threatIntel.countryCode }}
• ISP: {{ $('Function 1').item.json.threatIntel.isp }}
• Total Reports: {{ $('Function 1').item.json.threatIntel.totalReports }}

*AI Analysis:*
{{ $('Function 1').item.json.aiAnalysis }}

---
_Alert generated at {{ $now.format('YYYY-MM-DD HH:mm:ss') }}_
```

#### Activate Workflow

1. Click **Active** toggle in top-right
2. Save workflow

#### Update Splunk Alert

Go back to Splunk alert configuration and update webhook URL to:
```
http://<N8N_IP>:5678/webhook/splunk-alert
```

---

## 🧪 Testing & Validation

### Generate Test Events

#### Method 1: Failed RDP Login (Recommended)

On a separate machine (or host):

```bash
# Linux/Mac
ssh user@<WINDOWS_IP>  # Use wrong password 5 times

# Windows (RDP)
mstsc /v:<WINDOWS_IP>  # Enter wrong credentials
```

#### Method 2: PowerShell Script (Windows VM)

```powershell
# Simulate failed login events
1..10 | ForEach-Object {
    $cred = New-Object System.Management.Automation.PSCredential("FakeUser", (ConvertTo-SecureString "WrongPassword" -AsPlainText -Force))
    Start-Process runas.exe -Credential $cred -ArgumentList "cmd.exe" -ErrorAction SilentlyContinue
    Start-Sleep -Seconds 2
}
```

### Validation Checklist

- [ ] Splunk receives logs from Windows VM (`index=mydfir-project`)
- [ ] Splunk alert triggers on EventCode 4625
- [ ] N8N webhook receives Splunk data
- [ ] ChatGPT analysis completes successfully
- [ ] AbuseIPDB enriches source IP
- [ ] Slack message appears in #soc-alerts channel
- [ ] Full workflow completes in <30 seconds

### Troubleshooting

**No logs in Splunk:**
```bash
# Check Splunk Forwarder status on Windows
Get-Service SplunkForwarder

# Check Splunk receiving port
sudo netstat -tuln | grep 9997
```

**Webhook not triggering:**
```bash
# Check N8N logs
sudo docker-compose logs -f

# Test webhook manually
curl -X POST http://<N8N_IP>:5678/webhook/splunk-alert \
  -H "Content-Type: application/json" \
  -d '{"test": "data"}'
```

**API failures:**
- Verify OpenAI credits ($5 minimum)
- Check AbuseIPDB rate limits (free tier: 1000/day)
- Confirm Slack bot has `chat:write` permissions

---

## 📸 Screenshots

> **Add your screenshots in this section with descriptions**

### 1. Architecture Overview
![Architecture Diagram](screenshots/architecture.png)
*End-to-end workflow from log generation to Slack notification*

### 2. Splunk Dashboard
![Splunk Dashboard](screenshots/splunk-dashboard.png)
*Real-time monitoring of failed login attempts*

### 3. Splunk Alert Configuration
![Alert Setup](screenshots/splunk-alert.png)
*EventCode 4625 detection rule with webhook trigger*

### 4. N8N Workflow
![N8N Workflow](screenshots/n8n-workflow.png)
*Complete automation workflow with all nodes connected*

### 5. ChatGPT Analysis Output
![AI Analysis](screenshots/chatgpt-analysis.png)
*AI-generated threat summary with MITRE ATT&CK mapping*

### 6. AbuseIPDB Enrichment
![Threat Intel](screenshots/abuseipdb-result.png)
*IP reputation and abuse history from threat intelligence feed*

### 7. Slack Alert
![Slack Notification](screenshots/slack-alert.png)
*Final formatted alert delivered to SOC team channel*

### 8. Test Event Generation
![Test Events](screenshots/test-events.png)
*Simulated failed login attempts in Windows Event Viewer*

---

## 🔮 Future Enhancements

### Short-term
- [ ] **DFIR-IRIS Integration**: Automatic ticket creation for high-severity alerts
- [ ] **VirusTotal API**: File hash and URL reputation checks
- [ ] **Email Notifications**: Parallel alerting via SMTP
- [ ] **Dashboard**: Custom Splunk dashboard for SOC metrics

### Medium-term
- [ ] **Multi-Source Logs**: Linux (SSH), firewall, web server logs
- [ ] **Advanced Correlation**: Detect brute-force → successful login chains
- [ ] **Automated Response**: Block IPs via firewall API
- [ ] **SOAR Playbooks**: Predefined response workflows (isolate, contain, remediate)

### Long-term
- [ ] **EDR Integration**: Wazuh or Velociraptor for endpoint telemetry
- [ ] **UEBA**: User and Entity Behavior Analytics with ML
- [ ] **Kubernetes Deployment**: Production-ready containerized stack
- [ ] **Compliance Mapping**: NIST, ISO 27001, CIS Controls alignment

---

## 🔒 Security Considerations

### ⚠️ **NOT for Production Use**

This lab environment has intentional security gaps for learning purposes:

| Issue | Risk | Mitigation (Production) |
|-------|------|-------------------------|
| **Unencrypted Webhooks** | HTTP traffic is plaintext | Use HTTPS with TLS certificates |
| **API Keys in Config** | Keys stored in plaintext | Use secrets management (Vault, AWS Secrets Manager) |
| **No Authentication** | N8N UI exposed without MFA | Implement OAuth/SSO with MFA |
| **Data Privacy** | Logs sent to third-party AI | Use on-prem LLM or anonymize data |
| **Single Point of Failure** | No redundancy | Clustered Splunk indexers, load-balanced N8N |

### Privacy & Compliance

- **PII Handling**: This setup sends logs (potentially containing usernames, IPs) to OpenAI
- **GDPR/CCPA**: Not compliant for production SOC
- **Recommendation**: 
  - Use **self-hosted LLM** (Ollama, LLaMA 2)
  - Implement **data masking** before API calls
  - Get **explicit consent** for any real data processing

---

## 📚 Lessons Learned

### Technical Insights
1. **Webhook Latency**: Real-time alerts via webhooks introduce ~2-5s delay vs. native integrations
2. **API Costs**: ChatGPT-4 costs ~$0.03/1K tokens; use GPT-3.5-turbo for high-volume scenarios
3. **Log Parsing**: Splunk CIM (Common Information Model) is critical for normalized field names
4. **N8N Debugging**: Function nodes with console.log() helped troubleshoot data transformations

### Operational Takeaways
- **Alert Fatigue**: Initial threshold (1 failed login) generated 100+ alerts/hour
  - Solution: Increased threshold to 5 attempts within 5 minutes
- **False Positives**: Corporate VPN users triggered alerts during password resets
  - Solution: Whitelisted known VPN IP ranges in Splunk
- **Scaling**: Single Splunk instance handles ~5 GB/day; needs clustering for enterprise volume

### Career Development
- **Portfolio Value**: This project bridges multiple disciplines (SIEM, automation, AI)
- **Interview Questions**: Prepared for "Describe a time you automated a process"
- **Certifications**: Mapped to:
  - CompTIA Security+ (Objective 4.1: Security Monitoring)
  - Splunk Core Certified User
  - GIAC Security Operations Certified (GSOC)

---

## 📖 References

### Documentation
- [Splunk Enterprise Documentation](https://docs.splunk.com/Documentation/Splunk)
- [N8N Workflow Automation](https://docs.n8n.io/)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)
- [AbuseIPDB API Docs](https://docs.abuseipdb.com/)
- [Slack API Guide](https://api.slack.com/messaging/webhooks)

### Standards & Frameworks
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [CIS Critical Security Controls](https://www.cisecurity.org/controls)

### Learning Resources
- [MyDFIR YouTube Channel](https://www.youtube.com/@MyDFIR) (Original tutorial credit)
- [Splunk Fundamentals (Free Course)](https://education.splunk.com/)
- [N8N Community Workflows](https://n8n.io/workflows/)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**Disclaimer**: This lab is for educational purposes only. Do not use in production environments without proper security hardening, compliance review, and legal approval.

---

## 🤝 Contributing

Found a bug or have a suggestion? Open an issue or submit a pull request!

**Contribution Ideas:**
- Additional detection rules (PowerShell execution, lateral movement)
- Integration with other SIEM platforms (ELK, Wazuh)
- Terraform/Ansible automation for lab deployment
- Custom Splunk dashboards

---

## 👤 Author

**Your Name**  
[LinkedIn](https://linkedin.com/in/yourprofile) | [GitHub](https://github.com/yourusername) | [Portfolio](https://yourportfolio.com)

*Building this project? Tag me and share your results!*

---

## 🙏 Acknowledgments

- **MyDFIR** for the original project concept and tutorial
- **Splunk Community** for comprehensive documentation
- **N8N Open Source Team** for the automation platform
- **OpenAI** for GPT API access
- **AbuseIPDB** for threat intelligence feeds

---

<div align="center">

**⭐ If this project helped you, please star this repository! ⭐**

Made with ☕ and 🔐 for the cybersecurity community

</div>
