## Understanding Risk Management

**Risk** is defined as the **likelihood** that a **threat** will exploit a **vulnerability**, resulting in a negative impact on an organization. Risk evaluation uses two main criteria: **Impact** (magnitude of harm) and **Likelihood/Probability** (how often the risk is expected to occur). You cannot eliminate risk, only **manage** it. 

### 1. Threats and Vulnerabilities

A **threat** is a potential danger or circumstance that could compromise the Confidentiality, Integrity, or Availability (CIA) of data or systems. A **vulnerability** is a weakness that a threat can exploit.

| Threat Category | Examples |
| :--- | :--- |
| **Malicious Human** | Unskilled attackers, organized crime, state-sponsored **Advanced Persistent Threats (APTs)**. |
| **Accidental Human** | Users accidentally deleting/corrupting data, administrators causing outages via configuration errors. |
| **Environmental/Natural** | Hurricanes, floods, earthquakes, long-term power failure. |

A **Threat Assessment** identifies, categorizes, and predicts the likelihood and potential impact of threats against an organization's assets.

| Vulnerability Example | Description |
| :--- | :--- |
| **Default Configurations** | Failure to **harden a system** by changing default settings (e.g., default passwords). |
| **Lack of Malware Protection** | Missing or outdated antivirus/anti-malware definitions. |
| **Improper Patch Management** | Failure to update systems with patches, hotfixes, or service packs, leaving known flaws exploitable. |
| **Lack of Firewalls** | Host-based or network firewalls are disabled or improperly configured. |
| **Lack of Organizational Policies** | Missing policies like job rotation, mandatory vacations, or least privilege, increasing the risk of fraud or collusion. |

### 2. Risk Types and Management Terms

| Risk Type/Category | Description |
| :--- | :--- |
| **Internal vs. External** | **Internal** risks are from within (employees, hardware, software); generally predictable. **External** risks are from outside (attackers, natural disasters); many are unpredictable. |
| **Intellectual Property (IP) Theft** | Risk associated with the unauthorized use or theft of copyrights, patents, trademarks, or trade secrets. |
| **Software Compliance/Licensing** | Risk of losing money due to unauthorized use of software licenses (lost sales) or improper protection/management of purchased licenses. |
| **Legacy Systems/Platforms** | Primary risk is that the vendor no longer supports them, meaning no patches are released for discovered vulnerabilities. |

| Risk Term | Definition |
| :--- | :--- |
| **Risk Awareness** | Acknowledgment that risks exist and must be managed. |
| **Inherent Risk** | The risk level that exists **before** any controls are put in place. |
| **Residual Risk** | The risk level that **remains** after controls have been implemented. This risk is formally **accepted** by senior management. |
| **Control Risk** | The risk that the controls currently in place are **inadequate** to manage the identified risks. |
| **Risk Appetite** | The **amount of risk** an organization is **willing to accept** in pursuit of its goals (e.g., expansionary, conservative, neutral). |
| **Risk Tolerance** | The organization’s **ability to withstand risk** (often related to financial capacity). |

### 3. Risk Management Strategies

Risk management focuses on limiting or mitigating risks.

| Strategy | Action | Example |
| :--- | :--- | :--- |
| **Avoidance** | Not participating in or discontinuing a risky activity or service. | Deciding not to use an application that requires too many open firewall ports. |
| **Mitigation** | Implementing **controls** to reduce the vulnerability or the impact of the threat. | Installing up-to-date antivirus software to reduce the risk of malware. |
| **Acceptance** | Choosing to tolerate the risk, usually because the **cost of the control outweighs the potential loss**. Residual risk is always accepted. | Accepting the risk of a low-cost mouse being stolen instead of spending heavily on specialized locks for it. |
| **Transference** | Sharing the risk with another entity. | Purchasing **insurance** (including **cybersecurity insurance**) to cover financial losses related to a breach or incident. |

### 4. Risk Assessment Methodologies

A **risk assessment** (or analysis) quantifies or qualifies risks to help management prioritize resources. It starts by identifying **assets** and their **Asset Value (AV)**.

#### A. Quantitative Risk Assessment

Uses **specific monetary amounts** to measure and prioritize risks.

| Term | Definition & Formula | Example Calculation |
| :--- | :--- | :--- |
| **Asset Value (AV)** | The monetary value (often replacement cost) of an asset. | \$1,000,000 |
| **Exposure Factor (EF)** | The percentage of the asset expected to be damaged by the risk. | 50\% (or 0.5) |
| **Single Loss Expectancy (SLE)** | The cost of a single loss event. | $$SLE = AV \times EF$$ \$1,000,000 x 0.5 = **\$500,000** |
| **Annualized Rate of Occurrence (ARO)** | The expected frequency of the event in one year. | Once every 10 years = 0.1 |
| **Annualized Loss Expectancy (ALE)** | The expected annual loss from the risk. | $$ALE = SLE \times ARO$$ \$500,000 x 0.1 = **\$50,000** |

**Control Decision:** A control is a fiscally sound decision if its cost is **less than the savings** it provides (the reduction in ALE).

#### B. Qualitative Risk Assessment

Uses **judgment** to categorize risks based on **likelihood** and **impact** (e.g., Low, Medium, High).

* Experts assign probability and impact ratings (often converted to a simple numerical scale like 1, 5, 10).
* **Risk Score** is often calculated as: $$Risk\ Score = Likelihood \times Impact$$
* Results are often visualized using a **Risk Matrix**. 

### 5. Risk Documentation and Analysis

* **Risk Register:** A comprehensive document or tool listing all identified risks, their likelihood, impact, current status, and assigning **Risk Owners** responsible for managing them.
* **Key Risk Indicators (KRIs):** Metrics used to proactively monitor the level of risk (e.g., percentage of overdue security patches, average time to respond to an incident).
* **Risk Reporting:** The final phase of assessment, identifying risks and recommended controls. This report must be highly protected.

### 6. Supply Chain Risks

A **supply chain** includes all elements (suppliers, processes, services) required to produce and sell a product.

* **Attack Vector:** An attacker can compromise the supply chain by attacking a **third-party supplier** (a **supply chain attack**) rather than directly attacking the organization.
* **Mitigation:** Ensuring the organization has **multiple sources** for essential components, hardware, software, and services.

## Comparing Scanning and Testing Tools

Security administrators use **vulnerability scanners** (passive weakness checks) and **penetration tests** (active exploitation attempts) as part of a **vulnerability assessment** to determine the security posture of systems and networks.

A typical vulnerability assessment process:
1. Identify and prioritize **assets** based on value.
2. Identify and prioritize **vulnerabilities** or weaknesses.
3. Recommend **controls** to mitigate serious vulnerabilities.

### 1. Network Scanners

**Network scanners** gather information about hosts on a network and are used for reconnaissance during penetration tests. 

| Scanning Method | Description |
| :--- | :--- |
| **ARP Ping Scan** | Sends an ARP packet to an IP address; a response indicates a host is operational with that IP. |
| **SYN Stealth Scan** | Sends a SYN packet; a SYN/ACK response indicates an operational host. The scanner sends an RST (reset) instead of ACK to close the connection without completing the handshake. |
| **Port Scan** | Checks for **open ports** on a system, indicating an underlying service (e.g., open port 443 suggests HTTPS). |
| **Service Scan** | Verifies the protocol or service running on an identified open port (e.g., sends an HTTPS command to port 443). |
| **OS Detection (TCP/IP Fingerprinting)** | Analyzes packet details (like TCP window size) in system responses to identify the target's **Operating System**. |

### 2. Vulnerability Scanning

A **vulnerability scanner** is a tool that passively identifies weaknesses, known security issues, and misconfigurations by checking systems against a database of known vulnerabilities.

| Vulnerability Classification Standards | Description |
| :--- | :--- |
| **Common Vulnerabilities and Exposures (CVE)** | A dictionary of publicly known security vulnerabilities and exposures. Used by scanners like an antivirus signature file. |
| **Common Vulnerability Scoring System (CVSS)** | An industry-standard system that assigns severity scores (0 to 10) to vulnerabilities to help security professionals **prioritize** mitigation work. |
| **Security Content Automation Protocol (SCAP)** | A protocol designed to facilitate communication between vulnerability scanners and other security tools. |

#### Scan Confirmation (Accuracy)

When analyzing scan output, administrators must confirm results to eliminate errors: 

| Type | Condition | Outcome |
| :--- | :--- | :--- |
| **True Positive** | Vulnerability exists, and the scanner reports it. | **Correct** (Vulnerability is identified). |
| **True Negative** | Vulnerability does not exist, and the scanner does not report it. | **Correct** (No vulnerability is identified). |
| **False Positive** | Vulnerability **does not exist**, but the scanner **incorrectly reports** that it does. | **Error** (Increases administrative overhead to investigate). |
| **False Negative** | Vulnerability **exists**, but the scanner **fails to detect** or report it. | **Error** (Dangerous, as a real risk is missed). |

#### Credentialed vs. Non-Credentialed Scans

| Scan Type | Execution Context | Impact/Accuracy | Use Case |
| :--- | :--- | :--- | :--- |
| **Non-Credentialed** | Run **without** any user credentials (like an external attacker). | Lower accuracy, more false positives. | See what an external attacker would see. |
| **Credentialed** | Run with the privileges of a valid account (e.g., administrator). | Checks at a much **deeper level** (e.g., software versions), resulting in **higher accuracy** and fewer false positives. | Auditing internal security and configurations (e.g., **Configuration Review**). |

### 3. Penetration Testing (Pen Testing)

A **penetration test** is an **active** assessment that simulates or performs an attack to exploit vulnerabilities and determine the effectiveness of security controls. It must always be conducted with written **Rules of Engagement (ROE)**.

| Pen Test Category | Focus | Goal |
| :--- | :--- | :--- |
| **Physical** | Physical security measures (buildings, data centers). | Gaining unauthorized access to physical spaces (social engineering, lock picking). |
| **Offensive** | Simulating a real-world attack (network, systems, applications). | Exploiting vulnerabilities to gain unauthorized access or cause damage. |
| **Defensive** | Evaluating deployed security controls (firewall rules, configurations). | Identifying weaknesses in security controls *before* they can be exploited. |
| **Integrated** | Combines elements of physical, offensive, and defensive testing. | Comprehensive evaluation of the organization's entire security posture. |

#### Pen Test Phases and Tactics

| Phase/Tactic | Description |
| :--- | :--- |
| **Reconnaissance** (Footprinting) | Learning as much as possible about the network/target. |
| **Passive Reconnaissance** | Uses **Open-Source Intelligence (OSINT)** (social media, public records) without engaging the target. Tools: **theHarvester**, Whois lookups. |
| **Active Reconnaissance** | Sends data to targets and analyzes responses (network scanners, port scans). **Requires explicit authorization.** Tools: **Nmap**, **Netcat (nc)**, **hping**, **Dnsenum**. |
| **Initial Exploitation** | Actively exploiting a discovered vulnerability (e.g., missing patch) to gain initial access to a system. |
| **Persistence** | Techniques used to maintain a presence in the network undetected (e.g., creating backdoors or alternate accounts). |
| **Lateral Movement** | Maneuvering throughout the network *after* initial access (e.g., using WMI or PowerShell to scan and exploit other systems). |
| **Privilege Escalation** | Gaining higher levels of access/privileges on the exploited system or network (e.g., moving from a standard user to an administrator). |
| **Pivoting** | Using an exploited system as a launch point to attack or gather information on **other** systems and segments of the network. |
| **Cleanup** | Removing all traces of the tester's activities (accounts, scripts, logs, modified settings) as defined by the ROE. |

#### Knowledge of Environment

Pen tests are classified by the level of knowledge the tester has prior to the test: 

| Testing Type | Knowledge Level | Alias | Attacker Similarity |
| :--- | :--- | :--- | :--- |
| **Unknown Environment** | **Zero** knowledge of the environment. | **Black Box** | Approaches the test with the same knowledge as an external attacker. |
| **Partially Known** | **Some** knowledge (e.g., network documentation but not full layout). | **Gray Box** | Simulates an internal user or partner with limited access. |
| **Known Environment** | **Full** knowledge (source code, documentation, logon details). | **White Box** | Focuses on deep code review and configuration flaws from an insider perspective. |

## Responsible Disclosure, Audits, and Remediation

This section covers the final aspects of vulnerability management, from external reporting programs to internal audits and the final steps of fixing and verifying security issues.

### 1. External Reporting and Audits

| Program/Process | Description | Security Benefit |
| :--- | :--- | :--- |
| **Responsible Disclosure (RD)** | A coordinated process enabling individuals to report discovered security vulnerabilities to vendors/developers before they are exploited. | Allows security issues to be **addressed promptly** and prevents widespread attacks. |
| **Bug Bounty Programs** | A type of RD program that **incentivizes** external security researchers by offering monetary or other rewards for valid vulnerability submissions. | Creates a crowdsourced model of experts looking for flaws that internal teams may miss. |
| **System and Process Audits** | A review of an organization’s systems, processes, and procedures to assess **compliance** with standards and internal policies. | Identifies areas of non-compliance, inefficiencies, and serves as a valuable source for discovering existing vulnerabilities. |

### 2. Intrusive vs. Non-Intrusive Testing

Testing tools are categorized based on their potential to affect system operations.

| Testing Type | Intrusion Level | Impact on System | Example |
| :--- | :--- | :--- | :--- |
| **Intrusive** (Invasive) | **High** | Tools may **disrupt operations**, cause system instability, or take a system down by attempting to exploit vulnerabilities. | **Penetration Testing** |
| **Non-Intrusive** (Non-Invasive) | **Low** | Tools will **not compromise** a system and are much safer to run on live networks because they do not attempt to exploit vulnerabilities. | **Vulnerability Scanning** |

### 3. Responding to and Remediating Vulnerabilities

Once a serious vulnerability is identified, an organization must take steps to mitigate the risk.

#### Remediation and Mitigation

| Action | Description | When Used |
| :--- | :--- | :--- |
| **Patching** | Applying software updates to correct vulnerabilities and other flaws. | The most common and direct method for correcting a known vulnerability. |
| **Compensating Control** | Deploying a **secondary security control** to prevent a known vulnerability from being exploited. | When a patch is unavailable or when continuous operation of a vulnerable system is required. **Example:** Using a **Web Application Firewall (WAF)** to block SQL injection attacks against a vulnerable application. |
| **Segmentation** | Placing the vulnerable system on an **isolated network** to reduce its accessibility to outsiders and minimize the risk of a compromise. | To limit the attack surface when a vulnerability cannot be immediately patched. |
| **Exception/Exemption** | Granting formal permission for a system to continue operating despite violating security policies. | Used in conjunction with compensating controls or segmentation when business needs demand a system remain online. (Must be accompanied by risk acceptance.) |

#### Validation of Remediation

After fixing a vulnerability, it is crucial to confirm the fix was successful:

1.  **Rescan** the affected system to verify that the vulnerability no longer exists.
2.  Update vulnerability reporting to communicate to stakeholders that the issue was addressed.
3.  **Maintain records** of the remediation work for audit purposes.

## Capturing Network Traffic

Security professionals and attackers use specialized tools to capture, analyze, and manipulate network packets, providing deep insight into network activity and security.

### 1. Packet Capture and Analysis

**Packet Capture** involves using a **protocol analyzer** (or **sniffer**) to capture network packets in transit. **Packet Replay** involves editing captured packets and sending them back out over the network.

| Tool | Type / Use | Description & Key Feature |
| :--- | :--- | :--- |
| **Protocol Analyzer** (Sniffer) | Analysis / Troubleshooting | Captures packets to **analyze and modify** packet headers and payloads. Used by administrators to troubleshoot and by attackers to capture cleartext data like unencrypted credentials. |
| **Wireshark** | Protocol Analyzer (GUI) | A free, popular **Windows-based** graphical tool used to capture, display, and analyze packets. Can display the entire contents of a packet, including unencrypted data in ASCII and hexadecimal format.  |
| **tcpdump** | Protocol Analyzer (CLI) | A command-line tool, typically used on **Linux systems** (like Kali Linux), to capture packets. Often used to capture data, which is later analyzed in Wireshark. |
| **Tcpreplay** | Replay Utility Suite | A suite of utilities used to edit and **send edited packets** back over the network. Used by administrators to test the effectiveness of network devices like an **Intrusion Detection System (IDS)** against known attacks. |

### 2. NetFlow

**NetFlow** is a feature available on many routers and switches (originally developed by Cisco) used to collect **IP traffic statistics** and send them to a **NetFlow collector** for analysis.

| Feature | Protocol Analyzer (Wireshark) | NetFlow Collector |
| :--- | :--- | :--- |
| **Data Captured** | **All data** (Packet headers and payload contents). | **Statistics only** (Counts, timestamps, and connection details). |
| **Packet Detail** | Views **individual packets** in full detail. | Records **flows** (conversations) between systems. |
| **Information Included** | Source/Destination MAC/IP, Protocol, Full Data. | Timestamps (start/finish), Input/Output interface ID, Source/Destination IP/Port, **Packet count and byte count**. |

## Understanding Frameworks and Standards

A **framework** is a structured guide providing a foundation of basic concepts and best practices for implementing security. Frameworks help professionals secure various systems and manage risks.

### 1. ISO Standards

The **International Organization for Standardization (ISO)** develops globally recognized standards (which must be purchased):

| ISO Standard | Focus | Description |
| :--- | :--- | :--- |
| **ISO 27001** | Information Security Management System (ISMS) | Defines requirements for establishing, implementing, maintaining, and continually improving an ISMS. Organizations can achieve certification. |
| **ISO 27002** | Information Security Controls | Provides **best practices guidance** and detailed controls, complementing the requirements outlined in ISO 27001. |
| **ISO 27701** | Privacy Information Management System (PIMS) | An extension of 27001/27002, outlining a framework for managing and protecting **Personally Identifiable Information (PII)** to comply with global privacy regulations (e.g., EU GDPR). |
| **ISO 31000** | Risk Management | Provides **guidelines** and principles that organizations can adopt for effective risk management. |

### 2. Industry-Specific Frameworks

These frameworks apply to specific sectors or security goals:

* **Payment Card Industry Data Security Standard (PCI DSS):** Applies to organizations that **handle credit card data**. It mandates 12 principal requirements to protect cardholder information and reduce fraud risk.
* **Center for Internet Security (CIS):** Develops, validates, and promotes free **best practice solutions** (benchmarks and controls) to help organizations defend against pervasive cyber threats.

### 3. NIST Frameworks

The **National Institute of Standards and Technology (NIST)** publishes highly respected, **free-to-download** frameworks.

#### A. NIST Risk Management Framework (RMF)

(NIST SP 800-37) is mandatory for U.S. federal agencies and widely adopted in the private sector. It provides a seven-step process to manage security and privacy risks: 

1.  **Prepare:** Identify key roles, risk tolerance, and establish continuous monitoring strategy.
2.  **Categorize:** Determine the adverse impact (loss of Confidentiality, Integrity, Availability) of systems to prioritize them.
3.  **Select:** Choose and tailor necessary security controls (often starting with baselines).
4.  **Implement:** Put the selected controls into operation and document any changes.
5.  **Assess:** Verify that the implemented controls are working correctly and producing the desired outcome.
6.  **Authorize:** A senior official grants authorization to operate based on the risk assessment (emphasized by government).
7.  **Monitor:** Continuously assess system/environment changes and analyze risk responses.

#### B. NIST Cybersecurity Framework (CSF)

Aligns with the RMF and helps organizations improve their ability to prevent, detect, and respond to cyberattacks. It has three core components: 

| CSF Component | Description |
| :--- | :--- |
| **Core** | Five key functions representing the lifecycle of security activities: **Identify**, **Protect**, **Detect**, **Respond**, and **Recover**. |
| **Tiers** | Helps organizations gauge their view and maturity of risk management, ranging from **Partial (Tier 1)** to **Adaptive (Tier 4)** (most mature). |
| **Profile** | Lists specific desired outcomes. **Current Profiles** describe the existing state, while **Target Profiles** describe the desired state. Comparing them helps identify security **gaps**. |

### 4. Reference Architecture and Guides

* **Reference Architecture:** A document or set of documents providing a set of **standards** for high-level design decisions on complex projects (e.g., standardizing interfaces, reusable modules).
* **Benchmarks/Configuration Guides:** Vendor- or platform-specific guides that outline secure settings and best practices for configuring different systems (e.g., Windows, Linux, web servers, database servers). Following these ensures system hardening.

## Audits and Assessments

**Audits** and **Assessments** are tools used to provide business leaders and stakeholders with **assurance** that an organization complies with regulatory requirements and industry best practices.

### 1. Audits vs. Assessments

| Feature | Audit | Assessment |
| :--- | :--- | :--- |
| **Formality** | **Formal** evaluation and structured process. | **Less formal** review. |
| **Purpose** | To **confirm** that security controls are adequate and effectively protecting critical assets (compliance). | To review cybersecurity defenses, often including vulnerability scans, penetration tests, and control reviews. |
| **Performer** | Independent team (external firm or internal audit group). | Internal cybersecurity team or an external firm. |
| **Outcome** | **Attestation** (a formal statement on the effectiveness of controls). | Identification of vulnerabilities, risks, and areas for improvement. |

### 2. Categories of Audits

Audits are performed by a team **independent** from those who implement the security controls to ensure objectivity.

| Audit Type | Performer | Audience/Purpose |
| :--- | :--- | :--- |
| **External Audits** | An **independent auditing firm**. | Board of Directors, regulators, and external stakeholders. Often required for annual financial audits and includes cybersecurity controls. |
| **Internal Audits** | An auditing team **within the organization** (reporting to the Board's audit committee). | Management, to ensure compliance with internal policies and regulations, and to perform self-assessments. |

### 3. Gap Analysis and Attestation

* **Gap Analysis:** A common task for internal audit groups. It involves comparing an organization’s current operations to the **requirements of a specific standard** (e.g., ISO 27001). The goal is to note any "gaps" or areas where the organization is not fully meeting the standard, which are then identified as opportunities for improvement.
* **Attestation:** The formal statement made by the auditor at the conclusion of an audit. It certifies that specific **security controls and processes are in place and operating effectively**, putting the auditor's reputation behind the findings.