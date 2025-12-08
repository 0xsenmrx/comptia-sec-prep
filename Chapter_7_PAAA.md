## Identifying Network Attacks

This section covers common network-based attacks, emphasizing the concept of **resource exhaustion** and how attackers use **forgery** and **interception** to disrupt services or steal data.

### Denial of Service (DoS) Attacks

| Attack Type | Description | Goal & Indicator |
| :--- | :--- | :--- |
| **DoS** | Attack launched by **one attacker** against **one target**. | **Resource Exhaustion:** Overload system resources (CPU, memory, bandwidth) to prevent legitimate users from accessing services. |
| **DDoS** | **D**istributed **D**enial-**o**f-**S**ervice. Attack launched by **two or more computers** (often a **botnet**) against a single target. | **Indicator:** Sustained, abnormally **high network traffic** and system resource usage (processor/memory). |
| **Reflected DDoS** | Attacker sends requests to a third-party server with a **spoofed source IP address** (the target's IP). The third party sends the response to the victim. | Uses a legitimate third party to redirect traffic, hiding the attacker's true source. |
| **Amplified DDoS** | Combines reflection with amplification, where a **small request** from the attacker generates a **significantly larger response** from the third-party server directed at the target. | Increases the volume of traffic directed at the target, making the attack more effective. |
| **SYN Flood Attack** | A DoS/DDoS attack specifically targeting the **TCP three-way handshake**. The attacker sends a barrage of **SYN** packets but never sends the final **ACK** packet, leaving the server with many **half-open connections**.  | **Goal:** Consumes server resources (limited half-open connections) until the server can no longer accept legitimate connections. |

### Forgery and Spoofing Attacks

**Forgery** attacks involve creating a fake identity, certificate, or file to trick a user or system. **Spoofing** is a form of forgery where an entity impersonates another.

| Spoofing Method | Description |
| :--- | :--- |
| **Email Spoofing** | Changing the sender address in an email header so it appears the email is coming from someone else (common in spam/phishing). |
| **IP Spoofing** | Changing the source IP address in a packet so it appears the packet originated from a different system. |
| **MAC Spoofing** | Using software methods to change the hard-coded **MAC address** associated with a Network Interface Card (NIC). |

### Interception and Manipulation Attacks

| Attack Type | Description | Indicators |
| :--- | :--- | :--- |
| **On-Path Attack** (Man-in-the-Middle) | Active interception and modification where a third computer sits between two communicating parties, intercepts all traffic, and can modify, insert, or eavesdrop on data. | **Delay in traffic**, and in secure sessions, users will see **certificate warnings** (certificates not issued by a trusted CA) or **SSH key change warnings**.  |
| **SSL Stripping** | An on-path attack that changes an encrypted **HTTPS** connection to an unencrypted **HTTP** connection by intercepting the TLS negotiation phase. | The web browser shows the connection as **"Not secure"** or the URL includes **HTTP** instead of HTTPS. |
| **Replay Attack** | An attacker **captures data** (including credentials) from a previous communication session and **replays** the modified or original data to impersonate one of the parties (called **credential replay**). | Thwarted by using **timestamps** (e.g., Kerberos tickets), **sequence numbers**, and multi-factor authentication. |

### DNS Manipulation Attacks

DNS (Domain Name System) resolves hostnames (e.g., google.com) to IP addresses.

| Attack Type | Location of Attack | Description | Indicator |
| :--- | :--- | :--- | :--- |
| **DNS Poisoning** | **DNS Server** (or its cache). | Modifies or corrupts the DNS data (records) stored on a DNS server, causing all users relying on that server to be redirected to a malicious IP address. | User enters one URL but is taken to a different website. |
| **Pharming** | **User's Local System** (e.g., corrupting the local **hosts file**). | Manipulates the DNS name resolution process on the user's local machine, redirecting specific hostnames to malicious IPs. | User enters one URL but is taken to a different website. |
| **URL Redirection** | **Website's Files** (exploiting a vulnerability). | Attacker gains access to a website's underlying files and implements a redirect script to send all visitors to an alternate malicious website. | You are redirected to a different website after trying to access the intended one. |
| **Domain Hijacking** | **Domain Registrar** (usually via social engineering). | An attacker gains unauthorized control over the domain registration (often by changing the owner's email password first) and changes the ownership or DNS settings. | The legitimate owner loses control of their domain, and the website content is often completely changed. |

**DNS Filtering** and **DNS Sinkholes** are defensive measures. A **DNS sinkhole** is a DNS server that provides an **incorrect result** for a malicious domain name, preventing infected systems (like botnets) from contacting their command-and-control servers.

## Secure Coding Concepts

Secure application development requires developers to use **secure coding concepts** to prevent applications from becoming an attack vector.

### 1. Input Validation and Sanitization

**Input validation** is the most crucial security practice, involving checking data for validity *before* the application uses it.

| Validation Type | Description |
| :--- | :--- |
| **Server-Side** (Secure) | Code runs on the server. **Most secure** because it cannot be bypassed by the user. Always serves as the final check. |
| **Client-Side** (Faster) | Code runs on the user's system (e.g., JavaScript in a web browser). **Faster**, as it prevents unnecessary server roundtrips, but can be easily **bypassed** (e.g., by disabling JavaScript or using a web proxy). |

**Improper input handling** (lack of validation) allows many attacks, including **buffer overflow**, **SQL injection**, **DLL injection**, and **cross-site scripting (XSS)**.

| Common Input Checks | Purpose |
| :--- | :--- |
| **Proper Characters** | Verifying data types (e.g., only numbers for a zip code). |
| **Boundary/Range Checking** | Ensuring values fall within expected minimum/maximum limits (e.g., quantity of three or less). |
| **Blocking HTML/Special Characters** | Prevents attacks by detecting and removing characters like `<`, `>`, `'`, `=`, or `;`. |

**Sanitization (HTML Escaping):** Techniques like HTML encoding (e.g., replacing `>` with `&gt;`) are used to render potentially malicious code harmless, preventing attacks like XSS and directory traversal.

### 2. Handling Race Conditions and Errors

| Concept | Description | Security Concern |
| :--- | :--- | :--- |
| **Race Condition** | A conflict where two or more applications/modules try to access or modify a resource at the **exact same time**. | Can lead to data corruption or, if exploited, allow attackers to leverage a **TOCTOU** (Time of Check to Time of Use) attack. |
| **TOCTOU Attack** | **T**ime **o**f **C**heck **t**o **T**ime **o**f **U**se (a state attack). An attacker races the system, modifying a resource **after** the operating system validates access (**check**) but **before** the application performs the action (**use**). | Exploitable if symbolic links are used instead of direct file paths. |
| **Error Handling** | Routines that catch errors (**exception handling**) to prevent the application or operating system from crashing, maintaining system **integrity**. | **Errors to users should be generic** (to prevent reconnaissance). **Detailed information should be logged** for developers to troubleshoot. |
| **Code Obfuscation** | Attempts to make code unreadable by renaming variables, replacing numbers with expressions, and removing whitespace. | **Not a reliable security method** (security through obscurity) but can slow down casual reverse engineering. |
| **Software Diversity** | Using a compiler that mimics multiple languages and adds randomness to the executable code. | An attack that succeeds on one system might fail on another system running the same program compiled with diversity. |

### 3. Application Life Cycle Security

| Area | Secure Practice |
| :--- | :--- |
| **Outsourced Code** | Must ensure contracts specify: **thorough testing** before acceptance, adherence to **secure coding practices**, defense against **malicious code** (backdoors/logic bombs), and a clear process for **updates and vulnerability patching**. |
| **Data Exposure** | Protect data in all states (**at rest, in transit, and in processing**). Use **encryption** for data at rest and in transit. After processing encrypted data in memory, the application should **flush the memory buffers** to ensure no unencrypted remnants remain. |
| **HTTP Headers** | Configuring server response headers (based on recommendations like **OWASP Secure Headers Project**) to enhance security. | **`HTTP Strict-Transport-Security`:** Forces browsers to use HTTPS only. **`Content-Security-Policy`:** Defines acceptable content sources (scripts, styles, etc.). **`X-Frame-Options`:** Prevents the page from being rendered in an X-Frame, mitigating clickjacking attacks. |
| **Secure Cookie** | A cookie with the **secure attribute set** which ensures it is only transmitted over **secure, encrypted channels (HTTPS)**, protecting its confidentiality. |
| **Code Signing** | Digitally signing software with a certificate. **Benefits:** **Identifies the author** and provides a **hash** to verify the code **has not been modified** by malware. |

### 4. Code Analysis and Testing

| Analysis Type | Execution State | Method | Purpose |
| :--- | :--- | :--- | :--- |
| **Static Code Analysis** | **Without running** the code (Examining the source code). | **Manual Code Review:** A developer (other than the author) goes line-by-line to find vulnerabilities. **Automated Tools:** Scan code for defects. | Discover vulnerabilities before deployment. |
| **Dynamic Code Analysis** | **While running** the code. | **Fuzzing:** Sending large amounts of **random, malformed data** to the application to try and cause a crash or unexpected result, indicating a vulnerability. | Discover vulnerabilities during execution. |
| **Sandboxing** | Running the application in an **isolated environment** (e.g., a **Virtual Machine**) during testing. | Restricts the application's actions to the isolated area, preventing damage to the live system. |
| **Package Monitoring** | Tracking the use of shared code libraries and packages written by others. | Ensures that when vulnerabilities arise in a shared package, the organization can quickly identify all affected applications and patch them. |
| **Software Version Control** | Tracking changes to code over time (who made the update and when). | Allows developers to revert to a stable version and helps track down the source of issues. |

## Database Attacks (SQL Injection)

### SQL Injection Attacks

A **SQL injection (SQLi)** attack occurs when an attacker enters additional, malicious data into an application's input form (which uses **SQL queries** to interact with a back-end **database**) to execute unintended SQL commands.

| Element | Description |
| :--- | :--- |
| **SQLi Indicator** | Attackers often use SQL separators (`;`) to execute multiple commands and the comment syntax (`--`) to ignore closing quotes. |
| **Common Exploit Phrase** | Attackers frequently use the phrase **`' or 1=1;--`**. Since `1=1` is always **True**, the database's `WHERE` clause evaluates to true, often causing the query to return all records (e.g., the entire Customer table). |

**Example of Malicious Query:**
If the input is `' or 1=1;--`, the resulting executed query is:
$$\text{SELECT * FROM Customers WHERE name = '' or 1=1;--'}$$

### Protection Against SQL Injection

1.  **Input Validation:** Block or sanitize malicious characters like `'`, `;`, and `-`.
2.  **Stored Procedures:** Use **parameterized stored procedures** instead of directly copying user input into a SQL statement. The database interprets the user's input as literal **data** (a parameter) instead of executable **SQL code**, rendering the attack string harmless.

### Monitoring

**Web Server Logs** record activity and can be searched for indicators of SQLi attacks (e.g., the phrase `' or 1=1`). **SIEM systems** centralize logs and can be configured to alert administrators when suspicious patterns are detected.

## Automation and Orchestration for Secure Operations

**Automation** uses scripting to handle tasks, while **Security Orchestration, Automation, and Response (SOAR)** tools coordinate automated responses to security events (often low-level events) without human intervention.

### 1. Automation and Scripting Use Cases

Automation helps IT and security teams streamline processes, minimize human error, and ensure consistent security.

| Use Case | Description | Security Benefit |
| :--- | :--- | :--- |
| **User Provisioning** | Automating the creation, update, and removal of user accounts and permissions. | Enforces **least privilege** and prevents unauthorized access. |
| **Resource Provisioning** | Automating the creation and configuration of virtual machines, storage, and networks. | Ensures a **standardized, secure environment** and reduces configuration drift/errors. |
| **Guardrails** | Implementing automated rules that enforce security policies across the infrastructure. | Ensures security best practices are **consistently followed**. |
| **Security Groups** | Automating the management of access controls applied to network resources. | Ensures security controls are **consistently applied** and easily updated. |
| **Ticket Creation & Escalation** | Automatically generating and assigning incident tickets and escalating high-priority issues. | Streamlines incident response, leading to **improved response times** and reduced impact. |
| **Enabling/Disabling Services/Access** | Automating access changes based on user roles, policies, or risk assessments. | Maintains a secure environment by **limiting unnecessary attack surfaces**. |
| **Continuous Integration (CI) & Testing** | Automating code review, testing, and deployment. | Prevents the introduction of **security vulnerabilities** into production. |
| **Integrations & APIs** | Using **APIs** to connect and enable security tools and platforms to share information in real-time. | Allows tools to work together more effectively and streamlines operations. |

### 2. Benefits of Automation and Scripting

Automation significantly improves an organization's security posture and efficiency.

* **Efficiency/Time Saving:** Reduces the time required for repetitive tasks, allowing teams to focus on strategic work.
* **Enforcing Baselines:** Enables the consistent enforcement of security policies and configurations across all systems.
* **Standard Infrastructure Configurations:** Reduces the risk of misconfigurations caused by manual processes.
* **Secure Scaling:** Allows organizations to grow (scale operations) while ensuring security measures are consistently applied.
* **Reaction Time:** Improves an organization’s response time to security incidents and vulnerabilities.
* **Workforce Multiplier:** Allows security teams to manage more systems and processes without needing to hire additional personnel, resulting in cost savings.
* **Employee Retention:** Increases job satisfaction by automating repetitive work.

### 3. Considerations and Challenges

When implementing automation, organizations must address potential drawbacks:

| Consideration | Challenge | Mitigation |
| :--- | :--- | :--- |
| **Complexity** | Automation and scripting add complexity to infrastructure and processes. | Ensure the added complexity is manageable and well-documented. |
| **Cost** | Initial investment in tools, infrastructure, and training can be significant. | Carefully weigh long-term benefits against initial costs. |
| **Single Point of Failure** | Over-reliance on a single automated process can introduce a critical failure point. | Establish redundancies and fallback mechanisms. |
| **Technical Debt** | Scripts and integrations can become outdated, poorly maintained, or introduce vulnerabilities over time. | Plan for regular maintenance and updates for all scripts and tools. |
| **Ongoing Supportability** | Requires resources for training, documentation, monitoring, and updating the automation infrastructure. | Allocate resources specifically for the long-term maintenance and support of automation solutions. |
