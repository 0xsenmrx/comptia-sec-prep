## Change Management

**Change Management** provides a formal process for approving and carrying out technology changes in a coordinated manner to minimize risk and disruption.

### 1. Business Processes in Change Management

A robust change management program incorporates several key business processes:

| Process Element | Description | Purpose |
| :--- | :--- | :--- |
| **Formal Approval Process** | Management review and clearance required before a change can occur. | Ensures proper authorization and accountability. |
| **Ownership Statements** | Clearly defines the **primary owner** (key decision-maker/sponsor) for accountability. | Assigns responsibility for the change and its outcome. |
| **Stakeholder Analysis** | Identifies all internal and external individuals/groups potentially affected by the change. | Ensures coordination and prevents surprises. |
| **Impact Analysis** | Reviews all potential effects and unintended side effects of the change. | Critical part of **risk management**; forces comprehensive planning. |
| **Testing** | Carries out the change in a **test environment** prior to production deployment. | Confirms the change functions as expected; results support final approval. |
| **Backout Plan** | Detailed sequence of steps to **restore the system** to a previously operational state if the change fails. | Minimizes downtime and ensures a rapid recovery. |
| **Maintenance Windows** | Well-defined, coordinated times (usually off-hours) where systems may be down. | Allows change managers to consolidate changes and align stakeholder expectations. |

### 2. Technical Implications

Technical activities must be coordinated to ensure changes occur smoothly:

* **Security Control Updates:** Adjusting firewall rules, allow/deny lists, **Access Control Lists (ACLs)**, and other policies to accommodate the change.
* **Restricted Activities:** Identifying and implementing freezes (e.g., 48-hour new entry freeze) surrounding major system changes.
* **Downtime Communication:** Informing key stakeholders of outage expectations so they can plan business activities.
* **Disruption Avoidance:** Implementing controls around risky activities like application restarts or modifications to legacy applications.
* **Dependency Tracking:** Identifying upstream and downstream effects between interconnected systems and services.

### 3. Documentation and Version Control

* **Documentation:** A crucial repository of information about system design and configuration.
    * Change processes must ensure that **all documentation and diagrams are updated** before a change is formally closed out.
* **Version Control:** A formal process used to track the current and historic versions of software code and system configurations.
    * Developers check modified code into a version control system.
    * The system deconflicts changes made by multiple developers and tracks production vs. testing versions.
    * Version control is often integrated directly into the software development lifecycle.

## Protecting Data

Data policies and procedures are essential to protect secrets, prevent data leakage, and ensure compliance.

### 1. Understanding and Classifying Data Types

Organizations classify data based on its sensitivity, criticality, and regulatory requirements.

| Data Type | Description | Example / Regulation | Private Classification Example |
| :--- | :--- | :--- | :--- |
| **Regulated Data** | Governed by external laws, standards, and regulations. | PCI DSS (Credit Card Data), HIPAA (PHI), GDPR (PII). | **Restricted** |
| **Financial Information** | Data about monetary transactions or financial health. | GLBA (US financial institutions), salary data. | **Confidential** |
| **Intellectual Property (IP)** | Information crucial to the business, protected by copyright, trademark, or patent law. | Proprietary product designs, algorithms. | **Confidential** / **Restricted** |
| **Trade Secrets** | A type of IP that derives value specifically from being kept secret. | Coca-Cola formula, unpatented proprietary processes. | **Restricted** |
| **Legal Information** | Highly sensitive data related to lawsuits or legal strategy, often protected by attorney-client privilege. | Data concerning current or future litigation. | **Restricted** |
| **Personally Identifiable Information (PII)** | Information about an individual that should remain private. | Social Security numbers, full names, addresses, date of birth. | **Private** / **Confidential** |
| **Protected Health Information (PHI)** | Health and medical information tied to an individual. | Medical records, treatment history. | **Private** / **Restricted** |
| **Public Data** | Information available to anyone (e.g., press releases). | Company website content, brochures. | **Public** |

> A **Data Classification System** provides formal categories (e.g., Top Secret, Secret, Confidential, Unclassified, Public, Private) to identify data sensitivity and criticality, guiding the implementation of appropriate security controls.

### 2. Securing Data

The data classification level dictates the required security controls.

* **Permission Restrictions:** Limiting access to data only to authorized users (based on the principle of least privilege).
* **Geographic Restrictions:** Using controls (e.g., firewall rules, policies) to prevent users outside a defined geographic area (e.g., the European Union) from accessing certain data to ensure regulatory compliance.

### 3. Data Retention and Sanitization

#### Data Retention

A **Data Retention Policy** defines:
1.  How long specific data types must be retained.
2.  Where the data should be stored.

* **Benefits:** Reduces storage resources and legal liability by limiting the amount of old data that must be produced in response to a court order.
* **Compliance:** Must align with laws that mandate retention for specific time frames (e.g., 3+ years).

#### Data Sanitization

**Data Sanitization** ensures that all usable data is removed or destroyed from devices before disposal, preventing unauthorized access (**loss of confidentiality**). 

| Sanitization Method | Media Type | Description | Note |
| :--- | :--- | :--- | :--- |
| **File Shredding** | Disk Drives | Overwrites a file's location repeatedly with 1s and 0s to remove remnants. | Targets specific files, not the whole disk. |
| **Wiping / Overwriting** | Magnetic Drives | Bit-level overwrite process that writes patterns of 1s and 0s across the entire disk surface multiple times. | Makes data unreadable; simple deletion/formatting is not sufficient. |
| **Degaussing** | Magnetic Media (Tapes, HDDs) | Uses a powerful electronic magnet to randomize the magnetic patterns of the media. | **Only effective against magnetic media; destroys HDDs for reuse; ineffective against SSDs.** |
| **Physical Destruction (SSDs)** | SSDs, Disk Platters | Physically destroying the media by grinding or pulverizing. | Often the only acceptable method for SSDs (due to flash memory nature). |
| **Paper Shredding** | Paper Documents | Physically cuts paper; **cross-cut shredders** are best as they cut into fine particles. | Prevents dumpster diving. |
| **Pulping** | Shredded Paper | An additional step after shredding that reduces paper to a mash/puree. | Ensures complete destruction of paper. |
| **Pulverizing** | Optical Media, Hard Drives | Grinding media (e.g., CDs, hard drive platters) into fine particles. | Effective for media immune to degaussing. |
| **Certificate of Destruction (COD)** | All Media | A written certification provided (often by a third-party contractor) confirming that data destruction was properly carried out. | Provides an audit trail and legal proof of destruction. |

## Incident Response and Forensics

### 1. The Incident Response Plan

An **Incident Response Plan** provides a formal, coordinated, detailed set of procedures for personnel to follow when a security incident occurs, building upon the high-level **Incident Response Policy**.

| Component | Description | Example |
| :--- | :--- | :--- |
| **Definitions of Incident Types** | Clarifies the difference between an event and an actual security incident. Categorizes incidents for consistent handling. | Malware infection, DDoS attack, data breach, ransomware demand. |
| **Incident Response Team (CIRT/SIRT)** | A multidisciplinary team of employees with expertise in technical, security, management, and communications fields. | Includes senior management (authority), network admin (technical), security expert (forensics), and communications expert (media). |
| **Roles and Responsibilities** | Defines specific duties for each member of the incident response team. | Who authorizes containment, who handles evidence, who talks to law enforcement. |

### 2. Communication Plan

A sub-plan of the Incident Response Plan, outlining how and to whom information related to an incident is communicated.

| Communication Element | Target Audience | Key Requirement |
| :--- | :--- | :--- |
| **First Responders** | Incident Response Team/Entities | Must know when and who to contact to ensure early detection and containment. |
| **Internal Communication** | Senior Personnel/Management | Must inform management of serious incidents (e.g., data breaches, critical operations impact) but not routine, blocked attacks. |
| **Reporting Requirements** | External Entities | Notification of law enforcement or customers, often dictated by laws and regulations. |
| **External Communication** | Media/Public | Must be strictly controlled; only designated personnel can speak externally. |
| **Law Enforcement** | Law Enforcement Personnel | Must designate who can authorize involving law enforcement (to balance investigative help against public scrutiny). |
| **Customer Communication** | Customers | Must be approved by senior executives due to reputational and legal risks. |

### 3. Incident Response Process Phases

Incident response follows a structured, multi-phase lifecycle to ensure effective handling and continuous improvement. 

1.  **Preparation:** Occurs **before** an incident. Establishes the plan, procedures, training, and implements security controls to prevent incidents (e.g., anti-malware).
2.  **Detection & Analysis:** Monitoring systems (via **SIEM, SOAR, XDR, UEBA**) watch for unusual activity. Potential incidents are verified to distinguish true incidents from false positives (e.g., checking an IDS alert).
3.  **Containment:** Isolating the verified incident to protect critical systems and maintain business operations.
    * *Example:* Quarantining an infected device or blocking a network segment using an **Access Control List (ACL)**.
4.  **Eradication:** Removing the cause of the attack.
    * *Example:* Removing all remnants of malware, disabling compromised accounts, patching the exploited vulnerability.
5.  **Recovery:** Restoring all affected systems to normal operation.
    * *Actions:* Rebuilding systems from clean images, restoring data from backups, and verifying normal operation.
6.  **Lessons Learned:** A post-incident review to analyze the incident and the response. Includes a **Root Cause Analysis** to identify the initial failure point.
    * *Goal:* Modify procedures, plans, or controls to prevent recurrence.

### 4. Training and Testing

| Method | Description | Primary Goal |
| :--- | :--- | :--- |
| **Tabletop Exercises** | Scenario-based, non-threatening discussion of a hypothetical incident (e.g., simulated data breach). | Identify gaps and refine the existing Incident Response Plan. |
| **Simulations** | Hands-on, practical recreation of real-world incidents in a controlled environment. | Provide practical experience applying the plan and procedures. |
| **Threat Hunting** | **Proactively** searching for sneaky, hidden cyber threats that bypassed automated security systems. | Reduce the dwell time (time an attacker remains unnoticed) and limit damage. |

### 5. Digital Forensics: Acquisition and Preservation

**Digital Forensics** is the collection and analysis of digital data as evidence for legal proceedings, ensuring the data is controlled and unmodified.

#### Order of Volatility (OOV)

Evidence must be collected starting with the most volatile (easiest to lose) and moving to the least volatile. 

1.  **Cache** (Processor/HDD cache)
2.  **RAM** (Volatile memory, lost on power-down)
3.  **Swap File/Pagefile** (Extension of RAM, rebuilt on reboot)
4.  **Disk** (Local hard drives/attached devices)
5.  **Network** (Remote log servers, shared folders - least volatile due to robust backups)

#### Data Acquisition

* **Snapshots:** Capturing the current state of memory or disk contents for forensic analysis.
* **Forensic Artifacts:** Hidden or non-obvious pieces of data forensic experts extract (e.g., Web history, Recycle Bin contents, RDP cache, Windows Registry keys).
* **Firmware Forensics:** Extracting and reverse-engineering firmware code to check for embedded malware or backdoors.

#### Forensic Tools

* **Write-Blocker:** A hardware device used during acquisition to prevent any modification of the original evidence disk.
* **Imaging Tools:** Capture a **forensic image** (a bit-by-bit copy) of the disk or memory without modifying the original.
    * *Examples:* `dd` (Linux), `memdump`, **FTK Imager**, WinHex, Autopsy.
* **Verification:** Using **hashes** and **checksums** (e.g., SHA-256) to prove that the forensic image retains **integrity** and was not modified during collection or analysis.

## Legal Holds, eDiscovery, and Automated Response

### 1. Legal Holds and Electronic Discovery (eDiscovery)

* **Legal Hold:** A legal obligation imposed on an organization to **preserve** all forms of relevant data (digital and paper) once litigation or an investigation is reasonably anticipated.
    * **Goal:** Prevents the destruction of evidence (spoliation).
    * **Data Custodians:** Management directs personnel (custodians) to preserve data on all corporate systems (servers, emails, logs, mobile devices).

* **Electronic Discovery (eDiscovery):** The identification and collection of **Electronically Stored Information (ESI)** for use as evidence in legal cases. 
    * **Scope:** Files, emails, voicemail, social media entries, and website data.
    * **Metadata:** Data about data, which is vital and must be preserved during collection.
        * *Examples:* File creation/modification dates, email headers (sender/recipient/time), web page meta tags, and mobile device location/communication history.

### 2. Admissibility of Documentation and Evidence

To ensure evidence is **admissible** in a court of law and supports **non-repudiation**, specific forensic procedures must be followed to prove the evidence was not modified.

* **Chain of Custody:** A rigorous, documented process that provides assurances that evidence has been controlled and properly handled from the moment of collection.
    * **Form:** A physical or digital record documenting **every person** who had custody of the evidence, where it was stored, and the time of transfer.
    * **Purpose:** Proves the evidence presented in court is the unaltered original. Lack of adequate control or documentation makes evidence inadmissible. 

### 3. Reporting

Digital forensic experts document their findings in a report, which must be technically accurate.

* **Contents:**
    * Executive Summary (findings and recommendations).
    * List of forensic tools used.
    * List of evidence collected and analyzed.
    * Findings justifying the recommendations.
    * Documentation of the **Tactics, Techniques, and Procedures (TTPs)** used in the attack.

### 4. Security Orchestration, Automation, and Response (SOAR)

**SOAR** platforms automate the detection and response to low-level security events, freeing administrators to focus on complex incidents.

* **Orchestration:** Connecting various security tools (firewalls, DLP, SIEM) so they work together.
* **Automation:** Automatic execution of defined tasks.
* **Response:** Implementing defensive actions.

| SOAR Component | Description | Function |
| :--- | :--- | :--- |
| **Playbook** | Provides **general guidelines** and a checklist of steps for responding to a well-known incident (e.g., Phishing Playbook). | Documents the formal procedure that humans *or* automation should follow. |
| **Runbook** | Implements the Playbook guidelines using the organization's available security **tools**. | Executes the automated response (e.g., quarantining an email, blocking a malicious URL). |

* **Automation Example:** A SOAR platform identifies a phishing email, automatically forwards the attachment to a sandbox for analysis, verifies the maliciousness, and then executes the runbook to quarantine the email and block the embedded URL across the enterprise.

## Security Governance and Documentation

**Security Governance** is the set of responsibilities and processes established by top-level management to direct, evaluate, and control an organization's security efforts, providing the framework for security decision-making.

### 1. Governance Structures

| Structure/Entity | Description | Role |
| :--- | :--- | :--- |
| **Boards** | Executives and high-ranking individuals. | Make critical decisions about security policy and strategy. |
| **Committees** | Specialized groups. | Focus on specific aspects like risk management, compliance, or incident review. |
| **Centralized Structure** | Decision-making authority concentrated at the top. | Ensures consistent security policies across the entire organization. |
| **Decentralized Structure** | Decision-making authority spread across different parts of the organization. | Allows quicker responses to local challenges but risks inconsistent practices. |

* **External Considerations:** Governance must account for **Regulatory Requirements** (e.g., specific government standards), **Legal Obligations** (e.g., data privacy laws), **Industry Standards** (e.g., best practice benchmarks), and the global **Security Environment** (prevailing cyber threats).

### 2. Security Documentation Hierarchy

Security documentation is categorized by level of detail and authority. 

| Document Type | Level of Detail | Authority | Example |
| :--- | :--- | :--- | :--- |
| **Policies** | High-Level, Brief Statements (What) | **Mandatory** | Acceptable Use Policy (AUP), Incident Response Policy. |
| **Standards** | Technical and Business Requirements (How, Specifics) | **Mandatory** | Password complexity rules (length, characters), Approved encryption algorithms. |
| **Procedures** | Specific Step-by-Step Instructions (Execution) | **Mandatory** | Onboarding/Offboarding checklist, Detailed change management steps. |
| **Guidelines** | Optional Best Practices/Advice (Wisdom) | **Optional** | Advice on the most effective way to implement the encryption standard. |

#### Common Security Policies:

* **Acceptable Use Policy (AUP):** Describes proper use of systems and networks and user responsibilities; requires user acknowledgement.
* **Information Security Policy:** Defines rules for managing, protecting, and distributing information (e.g., password complexity, sensitive data handling).
* **Business Continuity and Disaster Recovery (BCDR) Policy:** Outlines steps to continue operations during and after a disruption (backup, recovery, restoration).
* **Incident Response Policy:** Defines rules and structure for responding to security incidents (e.g., data breach).
* **Software Development Lifecycle (SDLC) Policy:** Provides structure and security requirements for software development at each phase.
* **Change Management Policy:** Specifies the process for requesting, approving, testing, and implementing changes to IT systems.

### 3. Data Governance and Data Roles

**Data Governance** refers to the processes an organization uses to manage, process, and protect data, ensuring its availability, usability, integrity, and security.

* **Critical Data:** Data essential to the success of an organization's mission; requires additional governance and controls.

| Data Role | Responsibility | Typical Position |
| :--- | :--- | :--- |
| **Data Owner** | **Primary, high-level responsibility** for specific data. Ensures correct classification, labeling, and adequate security controls. **Cannot delegate responsibility.** | Senior Executive/Manager (Business Side) |
| **Data Steward** | **Day-to-day implementation** of the Data Owner's requirements and policies. | Business Manager/Analyst (Business Side) |
| **Data Custodian** | **Routine daily tasks** related to data maintenance, storage, backup, and implementation of technical business rules. | IT Professional (e.g., Database Administrator, System Admin) |
| **Data Controller** | The entity that **collects** information and **determines the purpose** and means of processing personal data. | The Organization (e.g., for employee payroll data) |
| **Data Processor** | A **third-party organization** that uses and manipulates data **on behalf of** the Data Controller. | Payroll company, Cloud Service Provider (CSP) |

### 4. Monitoring and Revision

Security governance is an iterative process requiring continuous monitoring and adjustment:

* **Monitoring:** Continuous checking of security measure effectiveness (e.g., routine security audits, log reviews, vulnerability scanning, incident metrics analysis).
* **Revision:** Updating policies, standards, and procedures based on monitoring insights, evolving threats, changes in business strategy, or new regulatory requirements.

## Third-Party Risk Management

Organizations must manage the risks introduced by entities outside the organization (**third parties**) such as vendors and supply chain partners.

### 1. Supply Chain and Vendor Risk

* **Supply Chain:** Includes all elements required to produce and sell products/services. It can be an **attack vector** (e.g., the M. J. Brunner Inc. breach).
* **Supply Chain Analysis:** Regularly identifies all vendors and assesses the associated risks.
* **Vendor Management Systems:** Provide vendors with limited, necessary access (system integration) to internal networks or data.
* **Vendor Diversity:** Implementing policies to use more than one vendor for the same product/service to provide cybersecurity **resilience** and reduce risk if one vendor fails.
* **End of Life (EOL) / End of Service Life (EOSL):**
    * **EOL:** The date when a product is no longer offered for sale.
    * **EOSL:** The date when the vendor stops providing support, patches, or upgrades to resolve vulnerabilities.

### 2. Vendor Assessment and Due Diligence

**Due Diligence** is a critical step when selecting a new vendor, involving a thorough evaluation of their capabilities, credentials, reputation, and security posture.

| Assessment Component | Description | Purpose |
| :--- | :--- | :--- |
| **Right-to-Audit Clause** | Contractual clause permitting the customer to hire an auditor to review the vendor's records and systems. | Ensures the vendor executes sufficient security measures. |
| **Internal/Independent Assessments** | Requesting evidence of the vendor's own internal security reviews or evaluations by an unbiased third party. | Provides assurance of adherence to security standards. |
| **Security Questionnaires** | Comprehensive forms the vendor must complete, detailing their security practices and measures. | Provides a clear view of the vendor's security infrastructure. |
| **Penetration Testing** | Simulated cyberattack performed on the system (by the vendor or a hired third party). | Identifies and addresses potential security weaknesses before malicious actors exploit them. |
| **Ongoing Monitoring** | Continuous vigilance of the vendor’s services post-selection. | Ensures consistent security posture and timely threat response. |
| **Conflicts of Interest Check** | Assessing if the vendor has relationships (e.g., with a competitor) that could compromise their ability to prioritize your needs. | Addresses potential risks and requires contractual clauses for disclosure and exit strategies. |

### 3. Vendor Agreements

Organizations use various agreements to stipulate performance expectations, responsibilities, and legal obligations.

| Agreement Type | Description | Key Feature |
| :--- | :--- | :--- |
| **Service Level Agreement (SLA)** | Stipulates performance expectations (e.g., minimum uptime, maximum downtime). | Includes **monetary penalties** if the vendor fails to meet expectations. |
| **Memorandum of Understanding (MOU/MOA)** | Expresses a mutual intention to work together toward a common goal. | Less formal than an SLA; **does not include monetary penalties.** |
| **Business Partners Agreement (BPA)** | Details the relationship, obligations, and shares of profits/losses between business partners. | Helps settle conflicts when they arise. |
| **Non-Disclosure Agreement (NDA)** | Ensures proprietary data is not disclosed to unauthorized entities. | Legal document that holds the second party legally responsible for unauthorized sharing. |
| **Master Services Agreement (MSA)** | A single contract containing all general terms for a vendor you work with repeatedly. | Referenced by specific **Work Orders (WO)** or **Statements of Work (SOW)** for new projects. |
| **Rules of Engagement** | Specific rules defining what a vendor is, and is **not**, allowed to do when conducting security testing activities. | Essential for controlling the scope of penetration testing. |

## Security Compliance and Privacy

**Security Compliance** ensures an organization adheres to external laws, regulations, and private standards, often focusing on protecting individual privacy (**data subjects**).

### 1. Key Compliance Regulations

| Regulation / Standard | Scope (Focus) | Jurisdiction / Authority | Key Requirement |
| :--- | :--- | :--- | :--- |
| **HIPAA** | **Health Information** | U.S. Federal Law | Mandates protection of personal health information (PHI) held by healthcare providers and related organizations. |
| **GLBA** (Financial Services Modernization Act) | **Financial Information** | U.S. Federal Law | Requires financial institutions to provide consumers with a **Financial Privacy Rule** notice detailing data collection and usage. |
| **GDPR** (General Data Protection Regulation) | **Privacy Data** | European Union (EU) Directive | Mandates protection of privacy data for individuals in the EU; applies globally to any organization processing this data. |
| **PCI DSS** (Payment Card Industry Data Security Standard) | **Cardholder Data** | Private Contractual Standard | Strict security requirements for any merchant handling credit card information (not a government law). |

### 2. Compliance Monitoring and Reporting

Compliance is an ongoing process using internal and external reviews to maintain adherence.

* **Due Diligence:** Actions taken to ensure the organization is **aware** of all applicable legal requirements, risks, and regulations.
* **Due Care:** The **continuous effort** of ensuring the organization adheres to these requirements and addresses identified non-compliance promptly.
* **Attestation:** Verification (by internal personnel or third parties) that the organization is compliant with relevant rules and regulations.
* **Acknowledgement:** Recognition and acceptance of compliance standards by employees and stakeholders (fosters a culture of compliance).
* **Automation:** Tools used to streamline and standardize compliance, reduce errors, and facilitate real-time reporting.

### 3. Data Privacy

Privacy laws exist at local, regional, national, and global levels, presenting a complex compliance challenge.

* **Local/Regional Laws:** Reflect specific area concerns (e.g., **California Consumer Privacy Act (CCPA)**, **GDPR** in the EU).
* **Right to be Forgotten:** A key concept in regulations like **GDPR**, empowering individuals to request the erasure of their personal data under specific circumstances.

### 4. Data Inventory and Retention

* **Data Inventory:** A detailed list (or map) of where important data is kept, who has access, and why it is used.
    * **Purpose:** Essential starting point for security and privacy; required by laws like GDPR/CCPA to know what personal data is held and where.
* **Data Retention Policies:** Rules specifying how long data should be kept and detailing how to **safely dispose** of it when no longer needed.
    * **Benefit:** Limits the volume of data that could be exposed during a breach and helps ensure compliance with laws requiring data deletion when its purpose is fulfilled.

## Security Awareness

**Security Awareness** is essential for organizational security, involving training personnel on policies and current threats to reduce risky behaviors.

### 1. Training Methods

A diversity of techniques should be used to ensure all employees understand cybersecurity threats.

| Training Method | Description | Key Benefit |
| :--- | :--- | :--- |
| **Computer-Based Training (CBT)** | Interactive training using applications (installed or web-based). | Allows students to learn at their own pace, with options to pause, rewind, and review material. |
| **Phishing Simulations** | Sending out **fake phishing emails** to employees to see if they click a malicious link or respond inappropriately. | Provides management with metrics on training effectiveness and identifies users who need remediation training. |
| **User Guidance and Training** | Formal instruction on specific security issues to increase user **situational awareness** regarding digital activities. | Reinforces security policies and reduces the risk of **insider threats**. |

### 2. Key Training Topics

Users are generally not security experts and need guidance on specific threats and best practices:

* **Insider Threat:** Training on recognizing signs of potential harm caused by someone *within* the organization (disgruntled, careless, or uninformed employee).
* **Password Management:** Importance of strong, unique passwords and the secure use of **password managers**.
* **Removable Media and Cables:** Training on the risks of introducing malware or exfiltrating data via devices like USB drives and the procedure for reporting lost/found devices.
* **Social Engineering:** Explaining common attacks (phishing, impersonation) and how to recognize and respond to them.
* **Operational Security (OpSec):** Limiting information shared publicly (e.g., on social media) and properly disposing of sensitive information.
* **Hybrid/Remote Work Environments:** Securing home networks, proper use of VPNs, and physically securing devices when working remotely.
* **Recognizing Anomalous Behavior:** Training personnel to understand **normal behavior** so they can spot and report unusual or risky actions (intentional or unintentional) that may indicate a security problem.

### 3. Program Development and Execution

* **Management:** Requires regular monitoring and reporting activities to check the program's effectiveness and identify areas for improvement or new initiatives.
* **Execution:** Ensuring training sessions are delivered on schedule, tracking attendance, and verifying that personnel are learning the necessary skills.
* **Automation:** Can be used to manage the program by tracking progress, delivering training, and flagging areas that need administrative attention.
