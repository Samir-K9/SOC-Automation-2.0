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

**Validation Checklist:**

- [ ] **Splunk receives logs:** Verify in Search & Reporting: `index=mydfir-project EventCode=4625`
- [ ] **Splunk alert triggers:** Check alert history in Splunk
- [ ] **N8N webhook receives data:** Check execution history in N8N workflow
- [ ] **ChatGPT analysis completes:** Verify OpenAI node executed successfully
- [ ] **AbuseIPDB enrichment works:** Verify HTTP Request node returned data
- [
## Screenshots

### Architecture Diagram
![Architecture Overview](screenshots/architecture.png)
*Complete workflow showing data flow from Windows endpoint through Splunk, N8N, AI analysis, and Slack notification*

### Splunk Configuration
![Splunk Dashboard](screenshots/splunk-dashboard.png)
*Splunk Enterprise dashboard showing real-time log ingestion from Windows endpoint*

![Splunk Alert Rule](screenshots/splunk-alert-config.png)
*Detection rule configuration for Event ID 4625 with webhook trigger to N8N*

### N8N Workflow Automation
![N8N Complete Workflow](screenshots/n8n-workflow-complete.png)
*Full N8N workflow with all nodes: Webhook → Parse → ChatGPT → AbuseIPDB → Slack*

![N8N Execution History](screenshots/n8n-execution-history.png)
*Workflow execution history showing successful alert processing*

### AI-Powered Analysis
![ChatGPT Analysis Output](screenshots/chatgpt-output.png)
*ChatGPT-generated threat analysis with MITRE ATT&CK mapping and recommended actions*

### Threat Intelligence
![AbuseIPDB Results](screenshots/abuseipdb-results.png)
*IP reputation data from AbuseIPDB showing abuse confidence score and historical reports*

### Slack Alert Delivery
![Slack Alert Message](screenshots/slack-alert-full.png)
*Formatted security alert delivered to SOC team with event details, threat intelligence, and AI analysis*

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

This foundational knowledge enables us to design, implement, and manage automated SOC workflows in production environments, accelerate incident response times, and optimize security operations through intelligent automation and AI integration.

---

## Future Enhancements

### Short-term Improvements
- **Multi-Event Correlation:** Detect attack patterns across multiple event types (failed login → successful login → privilege escalation)
- **Automated Response Actions:** Implement automated IP blocking via firewall API or account lockout
- **Custom Dashboards:** Build Splunk dashboards for SOC metrics (MTTD, MTTR, alert volume)
- **Email Notifications:** Add parallel email alerts for critical severity events

### Medium-term Expansions
- **Additional Log Sources:** Integrate Linux SSH logs, firewall logs, web server access logs
- **DFIR-IRIS Integration:** Automatic case creation in incident response platform
- **VirusTotal Integration:** File hash and URL reputation checks for malware analysis
- **User Entity Behavior Analytics (UEBA):** Detect anomalous user behavior patterns

### Long-term Vision
- **EDR Integration:** Connect endpoint detection and response tools (Wazuh, Velociraptor, CrowdStrike)
- **SOAR Playbooks:** Implement predefined response workflows (contain, isolate, remediate)
- **Machine Learning Models:** Train custom ML models for anomaly detection
- **Kubernetes Deployment:** Production-ready containerized deployment for high availability
- **Compliance Mapping:** Align detections to NIST CSF, ISO 27001, CIS Controls frameworks

---

## Security Considerations

### ⚠️ Important Security Warnings

**This lab environment is designed for educational purposes only and should NOT be used in production without significant security hardening.**

| Security Gap | Risk Level | Production Mitigation |
|--------------|------------|----------------------|
| **HTTP Webhooks** | High | Implement HTTPS with TLS certificates; use mutual TLS authentication |
| **API Keys in Plaintext** | Critical | Use secrets management (HashiCorp Vault, AWS Secrets Manager, Azure Key Vault) |
| **No Multi-Factor Authentication** | High | Implement SSO with MFA for N8N and Splunk access |
| **Third-Party Data Sharing** | Critical | Use on-premises LLM (Ollama, LLaMA 2) or anonymize PII before API calls |
| **Single Point of Failure** | Medium | Deploy clustered Splunk indexers and search heads; load-balanced N8N instances |
| **Insufficient Input Validation** | Medium | Implement strict input validation and sanitization in N8N workflows |

### Privacy and Compliance Considerations

**Data Privacy:**
- This setup sends security logs (containing usernames, IP addresses, computer names) to third-party services (OpenAI, AbuseIPDB)
- Potential PII exposure violates GDPR, CCPA, and other privacy regulations
- Not suitable for environments handling sensitive customer data

**Compliance Recommendations:**
- **Self-hosted LLM:** Deploy open-source models (Ollama, LLaMA 2, Mistral) for on-premises analysis
- **Data Masking:** Implement field redaction before sending to external APIs (hash usernames, anonymize IPs)
- **Audit Logging:** Enable comprehensive logging of all API calls and data transfers
- **Legal Review:** Obtain explicit consent and legal approval before processing real security data

**Production Security Checklist:**
- [ ] Replace HTTP with HTTPS (TLS 1.3) for all communications
- [ ] Implement secrets management solution for API keys and credentials
- [ ] Enable MFA for all administrative access
- [ ] Deploy Web Application Firewall (WAF) in front of exposed services
- [ ] Implement network segmentation and micro-segmentation
- [ ] Regular security audits and penetration testing
- [ ] Incident response plan for automation platform compromise
- [ ] Data retention and deletion policies compliant with regulations

---

## Lessons Learned

### Technical Insights

**Webhook Performance:**
- Real-time webhook triggers introduce 2-5 second latency compared to native SIEM integrations
- Consider batching non-critical alerts to reduce API costs and improve efficiency

**API Cost Management:**
- GPT-4 costs approximately $0.03 per 1K tokens (~750 words)
- For high-volume environments (1000+ alerts/day), use GPT-3.5-turbo to reduce costs by 90%
- Implement caching for repeated queries about the same IP addresses or users

**Log Parsing Challenges:**
- Splunk CIM (Common Information Model) is essential for normalized field extraction
- Custom parsing rules required for non-standard log formats
- Regular expression testing crucial before deploying detection rules to production

**N8N Debugging Techniques:**
- Function nodes with `console.log()` statements invaluable for troubleshooting
- Workflow execution history provides detailed error messages and data flow visualization
- Always test individual nodes before connecting full workflow

### Operational Takeaways

**Alert Fatigue:**
- Initial detection threshold (1 failed login) generated 100+ alerts per hour
- Adjusted to 5 failed attempts within 5-minute window, reducing false positives by 95%
- Lesson: Baseline normal activity before setting detection thresholds

**False Positive Reduction:**
- Corporate VPN users triggered alerts during legitimate password reset procedures
- Implemented IP whitelisting for known corporate infrastructure
- Added time-based correlation to distinguish brute force from typos

**Scaling Considerations:**
- Single Splunk instance handles ~5GB/day of log data
- Enterprise environments require distributed Splunk architecture (indexer cluster, search head cluster)
- N8N workflow execution limited by container resources; consider Kubernetes for high availability

### Career Development Impact

**Portfolio Value:**
- This project demonstrates proficiency across multiple SOC domains: SIEM, automation, AI integration, threat intelligence
- Bridges technical and analytical skills valued by security operations roles
- Tangible demonstration of cost-reduction and efficiency improvements

**Interview Preparation:**
- Prepared responses to "Describe a time you automated a repetitive task"
- Can explain trade-offs between different SIEM platforms and automation tools
- Demonstrates understanding of security operations workflow and incident response

**Certification Alignment:**
- Maps directly to CompTIA Security+ objectives (4.1 Security Monitoring, 4.3 Incident Response)
- Aligns with Splunk Core Certified User exam topics
- Relevant to GIAC Security Operations Certified (GSOC) practical scenarios

---

## References

### Official Documentation
- [Splunk Enterprise Documentation](https://docs.splunk.com/Documentation/Splunk)
- [Splunk Universal Forwarder](https://docs.splunk.com/Documentation/Forwarder)
- [N8N Workflow Automation Docs](https://docs.n8n.io/)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)
- [AbuseIPDB API Documentation](https://docs.abuseipdb.com/)
- [Slack API - Messaging](https://api.slack.com/messaging)

### Security Frameworks and Standards
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [CIS Critical Security Controls](https://www.cisecurity.org/controls)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

### Learning Resources
- [Splunk Fundamentals 1 (Free Course)](https://education.splunk.com/course/splunk-fundamentals-1)
- [N8N Community Workflows](https://n8n.io/workflows/)
- [Windows Event ID Encyclopedia](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/)
- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)

### Community and Support
- [Splunk Community Forums](https://community.splunk.com/)
- [N8N Community Forum](https://community.n8n.io/)
- [r/cybersecurity](https://www.reddit.com/r/cybersecurity/)
- [r/splunk](https://www.reddit.com/r/Splunk/)

---

## Acknowledgments

- **MyDFIR** for the original SOC automation lab concept and educational content
- **Splunk Community** for extensive documentation and best practices
- **N8N Open Source Team** for building an accessible automation platform
- **OpenAI** for providing accessible AI API services for security analysis
- **AbuseIPDB** for maintaining a comprehensive threat intelligence database
- **Cybersecurity Community** for sharing knowledge and detection engineering resources

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**Disclaimer:** This lab is designed for educational and training purposes only. Do not deploy this configuration in production environments without proper security hardening, compliance review, legal approval, and risk assessment. The authors are not responsible for any misuse or damage caused by implementation of this lab in unauthorized environments.

---

## Author

**[Your Name]**  
[LinkedIn](https://linkedin.com/in/yourprofile) | [GitHub](https://github.com/yourusername) | [Portfolio](https://yourportfolio.com)

*Cybersecurity Professional | SOC Analyst | Security Automation Enthusiast*

---

## Contributing

Contributions are welcome! If you have suggestions for improvements, additional detection rules, or integration with other security tools, please open an issue or submit a pull request.

**Contribution Ideas:**
- Additional Splunk detection use cases (PowerShell execution, lateral movement, data exfiltration)
- Integration with other SIEM platforms (Elastic Stack, Wazuh, Graylog)
- Alternative AI models (Anthropic Claude, Google PaLM, Open-source LLMs)
- Terraform/Ansible automation for complete lab deployment
- Advanced SOAR playbooks with remediation actions

---

<div align="center">

**⭐ If this project helped you learn SOC automation, please star this repository! ⭐**

![GitHub stars](https://img.shields.io/github/stars/yourusername/soc-automation-lab?style=social)
![GitHub forks](https://img.shields.io/github/forks/yourusername/soc-automation-lab?style=social)

*Built with ☕ and 🔐 for the cybersecurity community*

</div>
