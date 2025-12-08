## Understanding Threat Actors and Attack Vectors

**Threat actors** (attackers) are individuals or groups that launch cyberattacks against organizations. Understanding their attributes and motivations is crucial for designing effective defenses.

### Types of Threat Actors

| Threat Actor Type | Description | Primary Motivation | Attributes |
| :--- | :--- | :--- | :--- |
| **Nation-State / APT** | Employed or sponsored by a government to advance national interests. They are an **Advanced Persistent Threat (APT)**—highly organized, funded, and capable of long-term, sophisticated attacks. | Espionage, War, Strategic Advantage. | High **resources/funding**, High **sophistication**, External. |
| **Organized Crime** | Groups structured in a hierarchy, focused on coordinated criminal activity (e.g., operating ransomware). | **Financial Gain** (Greed). | High to Moderate resources, Moderate sophistication, External. |
| **Hacktivist** | Launches attacks to further an **activist movement** or cause (e.g., using disinformation campaigns). | **Philosophical/Political Beliefs**, Disruption/Chaos. | Varying resources, External. |
| **Unskilled Attacker** | Uses existing computer scripts or code to launch attacks (**Script Kiddie**). | Boredom, Curiosity, Ego. | Low resources, Low sophistication, External. |
| **Insider Threat** | Any individual with **legitimate access** to the organization's internal resources (employees, contractors). | **Revenge**, **Financial Gain**, or **Unwittingly** (due to being uneducated/negligent). | High **privileged access**, Internal. |
| **Competitor** | An organization seeking to gain proprietary information about a rival. | Espionage, Financial Gain (e.g., stealing trade secrets). | Varying resources, External. |
| **Ethical Hacker** | (White-Hat Hacker) Engages in hacking to **identify and report vulnerabilities** to improve security. | Ethical, Improvement. | Varies, usually contracted or authorized, External. |

### Threat Actor Motivations

Key reasons threat actors launch attacks:
* **Financial Gain:** Stealing credit card data, committing fraud, demanding ransom payments.
* **Data Exfiltration:** Stealing sensitive information (moving data outside the allowed area).
* **Service Disruption/Chaos:** Taking down websites or infrastructure (often used by hacktivists).
* **Blackmail:** Acquiring sensitive or embarrassing information to extort money.
* **Revenge:** Personal grudges against an individual or organization.
* **Espionage:** Stealing intellectual property or trade secrets (common for nation-states and competitors).
* **War:** Using cyberattacks to disrupt, damage, or destroy critical infrastructure.

### Threat Vectors and Attack Surface

A **threat vector** is the path an attacker uses to gain access and exploit a vulnerability. The **attack surface** is the sum of all exposed threat vectors an organization must defend.

| Threat Vector Category | Description and Examples |
| :--- | :--- |
| **Message-Based** | Attacks starting via email (**spam**) with malicious links/attachments (Phishing, Spear Phishing, Whaling). |
| **File-Based** | Malicious code hidden within seemingly harmless files (documents, spreadsheets). |
| **Image-Based** | Embedding malicious code within image files or using **steganography** (hiding data in an image). |
| **Voice Call** | Phone-based social engineering, impersonating trusted individuals (Vishing). |
| **Removable Device** | Devices (USB drives) loaded with malware that executes when plugged into a computer. |
| **Software/System-Based** | Targeting vulnerabilities in **unsupported OS/applications**, using default credentials, or exploiting **open service ports**. |
| **Network-Based** | Exploiting weaknesses in wired/wireless networks, unsecured Bluetooth, or eavesdropping on traffic. |
| **Supply-Chain** | Compromising a trusted third party (MSPs, vendors) to gain access to the target organization. |

### Shadow IT

**Shadow IT** refers to any **unauthorized systems or applications** (including cloud services) used within an organization without IT approval.

* **Risk:** Shadow IT increases risk because these systems are not properly managed (e.g., they may lack patches or backups) and are susceptible to emerging vulnerabilities.

## Determining Malware Types

**Malware (Malicious Software)** is a broad category of software installed without the user's consent, causing symptoms like slow system performance, random reboots, and unauthorized processes.

### Major Malware Categories

| Malware Type | Key Characteristics | Delivery Method / Mechanism |
| :--- | :--- | :--- |
| **Virus** | Malicious code that **attaches to a host application**. Requires the host application to be executed (often unknowingly by the user) to run and replicate. | Infected files, infected USB drives, or automatic OS execution. |
| **Worm** | **Self-replicating** malware that **travels autonomously** across a network without a host application or user interaction. | Exploits network vulnerabilities to spread quickly; consumes massive network bandwidth. |
| **Logic Bomb** | A string of code embedded in an application that executes only when a **specific logical event** occurs (e.g., a specific date/time, or a name is missing from a payroll list). | Usually planted by insiders; dormant until triggered. |
| **Trojan (Trojan Horse)** | Appears to be beneficial or harmless (e.g., pirated software, a game, or a browser extension) but contains a **hidden malicious payload**. | **Drive-by downloads**, malicious email attachments, or **scareware** (fake antivirus demanding payment). |
| **RAT (Remote Access Trojan)** | A type of Trojan that grants attackers **remote, sustained control** over an infected system, often with the ability to install additional malware. | Drive-by downloads, malicious email attachments. |
| **Keylogger** | Captures a user's **keystrokes**. Can be software-based (part of spyware/RAT) or **hardware-based** (a physical device plugged into the keyboard port). | Malware installation, physical access to the device. |
| **Spyware** | Software installed secretly to **monitor the user's computer and activity**, often collecting private data (data-harvesting). | Often bundled with other software (**Bloatware**) or via drive-by downloads. |
| **Rootkit** | A program that gains **administrative (kernel-level or root-level) access** to a system and **hides its running processes** and files from the operating system and antivirus scans. | Exploits OS vulnerabilities; uses **hooking techniques** to intercept system function calls. |
| **Ransomware** | Malware that **encrypts a user's data** or locks their system, preventing access, and demands a **ransom** payment for the decryption key. | Drive-by downloads, embedded in other software via email. |
| **Bloatware** | Unwanted programs bundled with legitimate software. Can be legitimate or malicious (often containing spyware or adware). | User consenting to obscured **Terms of Use** during installation. |

### Indicators of a Malware Attack

Generic signs that a system or network may be infected:

* **System Performance:** Computer runs significantly slower, random reboots.
* **Extra Network Traffic:** Abnormal network traffic levels compared to a known baseline.
* **Data Exfiltration:** Unauthorized transfer of data (e.g., credentials, files) out of the network.
* **Encrypted Traffic:** A large volume of encrypted traffic leaving the network can indicate data exfiltration, bypassing DLP, even if the content cannot be read.
* **Traffic to Specific IPs:** Attempts by an infected system ("bot zombie") to connect to known **command and control (C2)** servers (monitor firewall logs for blacklisted IPs).
* **Outgoing Spam:** Desktop computers sending large amounts of unsolicited email, indicating they are part of a botnet.

## Social Engineering and Human Vectors

**Social engineering** is the practice of using social tactics and psychological manipulation to trick individuals into revealing sensitive information (like credentials) or performing actions they wouldn't normally take. Social engineering attacks can occur in person, over the phone, via email, or on websites.

### Social Engineering Techniques

| Technique | Description | Security Implication |
| :--- | :--- | :--- |
| **Impersonation** | Posing as a trusted individual (e.g., IT technician, executive) to gain information or physical access (e.g., to a server room). | Leads to unauthorized access or disclosure of sensitive data. |
| **Tailgating / Piggybacking** | Following closely behind an authorized person through a secured entry point (Homer badges in, Francesca walks in behind him without badging). | Bypasses physical access controls. Prevented by **Access Control Vestibules (Mantraps)** or turnstiles.  |
| **Shoulder Surfing** | Gaining unauthorized information by observing someone's screen or looking over their shoulder as they enter credentials (PINs, passwords). | Loss of confidentiality. Mitigated by screen filters and proper monitor positioning. |
| **Pretexting** | Creating a detailed, believable **fictitious story (pretext)** to manipulate a target into providing information or access (e.g., calling as an IT technician needing login credentials to "fix" an urgent problem). | Exploits the target's trust and willingness to help. |
| **Elicitation** | Gathering information **without asking for it directly** through casual conversation. Techniques include flattery, **active listening**, **reflective questioning**, giving **false statements** to prompt correction, and **bracketing** (using a number range to get a specific value). | Allows attackers to gather personal details (for password resets) or proprietary information. |
| **Disinformation (Hoaxes)** | Providing **false information** to influence a target's action (e.g., an email hoax warning of a non-existent virus and encouraging users to delete system files). | Can waste help-desk time or cause users to damage their own systems. |
| **Dumpster Diving** | Searching through trash or recycling for discarded documents, printouts, or notes containing PII, PHI, proprietary data, or old company directories. | Mitigated by **shredding or burning** sensitive documents. |

### Attack Vectors Related to Social Engineering

| Attack Type | Description | Mitigation Strategy |
| :--- | :--- | :--- |
| **Watering Hole Attack** | Identifying websites that a specific group of targets (e.g., employees of a nuclear plant) are likely to visit, then **infecting those trusted sites with malware** to compromise the visitors. | Security updates, blocking malicious IPs, employee training. |
| **Business Email Compromise (BEC)** | A targeted attack where the attacker **impersonates a high-level executive** (CEO, CFO) to request an urgent fraudulent wire transfer or confidential data (like employee tax records) from an unsuspecting employee. | Strong email security, multi-factor authentication, and clear verification procedures for sensitive requests. |
| **Typosquatting** | Registering a domain name that is a **slight misspelling** of a legitimate domain (e.g., `comptai.org` instead of `comptia.org`). | Used to host malware, earn ad revenue (pay-per-click), or resell the domain. |
| **Brand Impersonation** | Posing as a **well-known, trusted company or brand** (using logos/designs) in emails or fake websites to steal login credentials or credit card information. | Employee training, verifying links/senders, using strong authentication. |

## Message-Based Attacks

Attackers frequently use messaging channels (email, IM, phone) because they are highly successful at tricking users.

### General Phishing Attacks

| Attack Type | Description | Key Characteristic |
| :--- | :--- | :--- |
| **Spam** | Unwanted or unsolicited email, ranging from harmless advertisements to malicious content (links, code, attachments). | Criminals confirm a victim's email address is valid if the victim attempts to "opt-out" from a malicious sender. |
| **Phishing** | Sending email impersonating a well-known company (e.g., bank, PayPal) to trick users into **revealing personal information** or clicking a malicious link that leads to malware installation. | Creates a false sense of urgency (e.g., "account will be suspended") to make the user click. **Legitimate companies never ask you to validate credentials via email.** |
| **SPIM** | **S**pam over **I**nstant **M**essaging (IM) channels (WhatsApp, Facebook Messenger, SMS). | Bypasses traditional email spam/antivirus filters; often uses malicious links related to current events (e.g., COVID-19, stimulus payments). |
| **Beacons** | A tracking link (often linked to an image) embedded in a malicious email. When the email client loads the image, the server registers the request, validating that the user's email address is active. | Most email programs block images by default to thwart this validation method. |

### Targeted Phishing (Spear Phishing and Whaling)

| Attack Type | Description | Target and Risk |
| :--- | :--- | :--- |
| **Spear Phishing** | A **targeted** form of phishing sent to specific groups of users (e.g., all employees of a company, or customers of a service). | High success rate because the email is customized. **Digital signatures** can help verify the sender's identity to reduce success. |
| **Whaling** | A form of spear phishing that **targets high-level executives** ("whales") or impersonates them to attack high-level employees (e.g., HR or Payroll). | The payoff is large (confidential company information, large financial transactions, W-2 forms). |
| **Business Email Compromise (BEC)** | *(See previous section)* Highly targeted and often involves impersonating an executive to request **urgent fraudulent wire transfers**. | Major financial loss and data theft. |

### Phone-Based Attacks

| Attack Type | Description | Mechanism |
| :--- | :--- | :--- |
| **Vishing** | **V**oice phishing that uses the **phone system (VoIP)** to trick users into giving up personal and financial information. | Attackers can **spoof caller ID** to make the call appear local or from a trusted company. Often uses automated recordings to collect sensitive data (credit card, SSN, etc.). |
| **Smishing** | **S**MS phishing that uses **text messages** to trick users (e.g., claiming suspicious account activity). | Often tries to exploit **Two-Factor Authentication (2FA)** by tricking the user into sending a legitimate verification code (sent by the real company) back to the attacker via text. |

## The Anatomy of a Cyber Attack (APTs)

A successful cyberattack often starts with a **single click** by an uneducated user and gives the attacker access for **lateral movement** throughout the network. This process, often utilized by sophisticated groups like APTs, involves several steps: 

| Step | Action by Attacker / System | Goal |
| :--- | :--- | :--- |
| **1. Reconnaissance** | The attacker uses publicly available information (social media, news) and social engineering to **identify a specific target** within the organization. | Gather intelligence to craft a believable attack. |
| **2. Initial Access & Phishing** | The attacker crafts a **spear phishing email** with a malicious link or attachment. The link may lead to a **drive-by download** or a fake site for **credential harvesting**. | Trick the user into clicking the link or entering credentials to gain an initial foothold. |
| **3. Execution** | The user clicks the link. The malicious website attempts to install malware (e.g., a **RAT** or **ransomware**) or captures the entered credentials. | Compromise the user's system or steal their login information. |
| **4. Command and Control (C2)** | If malware is installed, it collects the user's information and sends it back to the attacker's server (C2). If credentials are stolen, the attacker uses them directly. | Establish a connection and gain user credentials. |
| **5. Lateral Movement** | The attacker uses the compromised system and the target's credentials to scan and access other systems within the network. Tools like **WMI** and **PowerShell** are frequently used. | Expand access from the initial infected host to other high-value assets. |
| **6. Privilege Escalation** | The attacker uses specialized techniques to gain higher permissions (administrator privileges) than the original user. | Gain control of sensitive systems and servers. |
| **7. Data Gathering & Preparation** | Malware searches computers and servers for data of interest (emails, files, etc.). The gathered data is typically **encrypted and divided into chunks**. | Locate and prepare sensitive data for theft. |
| **8. Exfiltration** | The encrypted data chunks are **exfiltrated** (transferred unauthorized) from the internal network back to the attacker's external resources. | Steal the data. |
| **Ransomware Action** | *(Alternative Path)* Instead of exfiltrating data, ransomware begins encrypting files as soon as it locates them, sometimes focusing on deleting or encrypting backups first. | Demand a ransom payment to return access to the data. |

### Attack Timeline

The time it takes for an attacker to begin **lateral movement** after the initial infection is often **less than two hours**. This rapid response highlights the need for immediate detection and incident response.

## Blocking Malware and Other Attacks

Organizations use a **defense-in-depth (layered security)** approach to protect against malware and other attacks, combining multiple security controls.

### Malware Defense Mechanisms

| Security Control | Location | Function | Mechanism |
| :--- | :--- | :--- | :--- |
| **Spam Filters** | Mail Gateways, Email Servers, User Systems. | Detect and block **unsolicited/malicious email (spam/phishing)** before it reaches the user. | Uses blocklists/safelists; often errs on the side of caution (allowing spam) rather than blocking legitimate email. |
| **Anti-Malware Software** | Mail Gateways, Workstations, Servers (All Systems). | **Detects, blocks, and removes** various forms of malware (viruses, Trojans, worms, rootkits, spyware). | Provides **real-time protection** (continuous monitoring) and performs scheduled/manual scans. |
| **Network Boundaries** | Firewalls, **Unified Threat Management (UTM)** systems. | Monitors network traffic for signs of malware or malicious activity attempting to enter the network. | Inspection and filtering of traffic at the perimeter. |

### Anti-Malware Detection Methods

Anti-malware software relies on two main methods:

1.  **Signature-Based Detection:**
    * Detects **known malware** by comparing files against a database of **signature files (data definition files)** which contain known patterns of malicious code.
    * Requires regular, frequent **updates** to the signature files to stay effective against new threats.
2.  **Heuristic-Based Detection:**
    * Detects **previously unknown malware** (including zero-day exploits) based on suspicious **behavior** or characteristics.
    * Often involves running questionable code in a **sandbox (virtualized environment)** to observe if it engages in malicious activity (like modifying system files or adding variations, as seen in polymorphic malware).

**File Integrity Monitors** are often used by anti-malware scanners to detect modifications to critical system files. They calculate and store a baseline hash of the file; if a later hash check doesn't match the baseline, it signals unauthorized modification, which can indicate a rootkit infection.

## Why Social Engineering Works (Psychological Principles)

Social engineers exploit psychological principles to increase the effectiveness of their attacks:

| Principle | Description | Effective In Attacks Like... |
| :--- | :--- | :--- |
| **Authority** | People are more likely to comply when told to do something by someone they perceive as an authority figure (e.g., executive, technician, government agent). | Impersonation, Whaling, Vishing. |
| **Intimidation** | Using bullying or threatening tactics to force a victim to act immediately. | Impersonation, Vishing (e.g., threatening financial loss or job consequences). |
| **Urgency** | Creating a sense of limited time to encourage quick decisions without critical thinking. | Ransomware (countdown timer), Phishing (immediate account suspension), Vishing, Whaling. |
| **Scarcity** | Encouraging action by implying a limited quantity or exclusive access to an item. | Phishing, Trojan attacks (e.g., "limited access" to a new product). |
| **Consensus / Social Proof** | Victims are more likely to believe and act if they think many other people are doing it (e.g., fake testimonials promoting malicious software). | Trojans, Hoaxes. |
| **Familiarity & Trust** | Building rapport or leveraging an existing relationship (or faking one) makes a victim more likely to comply with requests or overlook suspicious behavior. | Shoulder Surfing, Tailgating, Vishing. |

## Threat Intelligence Sources

**Threat Intelligence** provides data and analysis about existing and emerging threats to help organizations improve their defenses.

### Open-Source Intelligence (OSINT) Resources

| Source | Description | Standard/Example |
| :--- | :--- | :--- |
| **Vulnerability Databases** | Publicly accessible databases that document known software vulnerabilities. | **National Vulnerability Database (NVD)**, **Common Vulnerabilities and Exposures (CVE)**. |
| **STIX / TAXII** | **STIX (Structured Threat Information eXpression)** defines **what** cyber threat information should be shared. **TAXII (Trusted Automated eXchange of Intelligence Information)** defines the services and messages for **how** that information is exchanged. | Used by **Automated Indicator Sharing (AIS)** from CISA. |
| **Dark Web** | Hidden area of the Internet where criminals store and sell hacking tools, pirated materials, and often post zero-day vulnerabilities before they hit public databases. | Access requires specific software/authentication. |
| **Indicators of Compromise (IoC)** | Pieces of evidence that a cyberattack is happening or has happened (e.g., specific malicious URLs, file names, or unique hashes). | Used by security professionals to search logs and systems for signs of infection. |
| **Other Sources** | Vendor websites, Academic Journals, Conferences, local industry groups (e.g., InfraGard), and specific file/code repositories (e.g., GitHub). | |

### Predictive Analysis

Predictive analysis attempts to forecast what attackers will do next and how to thwart future attacks.

### Threat Maps

Provide a visual, anonymized representation of **active and recent cyber threats** globally.
