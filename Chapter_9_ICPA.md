## Comparing Physical Security Controls

**Physical Security Controls** are tangible items used to deter, detect, and respond to physical threats (e.g., fences, locks, badges). **Physical Access Controls** specifically regulate entry and exit.

### 1. Layers of Physical Protection (Defense in Depth)

Organizations implement physical controls at multiple boundaries:

| Boundary Layer | Example Controls | Purpose |
| :--- | :--- | :--- |
| **Perimeter** | Fences, security guards at gates, zigzag barricades, lighting. | Deters entry onto the property and controls vehicular access. |
| **Buildings** | Locked doors, lighting, video cameras, security guards, reception desks. | Restricts entry to authorized personnel and monitors entrances/exits. |
| **Secure Work Areas** | Restricted access doors, escort requirements for visitors. | Limits access to spaces where classified or highly sensitive tasks occur. |
| **Server Rooms / Wiring Closets** | Electronic locks, video surveillance (CCTV). | Protects servers, routers, and switches from unauthorized access or installation of monitoring hardware. |
| **Hardware** | Locking cabinets, safes, cable locks (e.g., for laptops). | Protects individual physical devices from theft or tampering. |

> **Note:** **Industrial Camouflage** (like landscaping) can be used to hide security elements (e.g., fences) for aesthetic benefits while maintaining protection.

### 2. Access Badges and Entry Controls

| Control Type | Description | Security Feature |
| :--- | :--- | :--- |
| **Proximity Cards / Smart Cards** | Small cards or tokens that activate when near a reader, unlocking electronic doors. | Can be combined with a **PIN** to achieve **multifactor authentication** (something you have + something you know). |
| **Turnstiles** | Physical gates used with access badges to ensure only **one person** enters a secure area at a time (deters **tailgating**). |
| **Access Control Vestibules** (Mantraps) | A secure entry compartment with **two sets of interlocking doors**. | Traps individuals attempting to enter unauthorized, effectively preventing tailgating and forced entry.  |
| **Bollards** | Short, reinforced concrete/steel posts placed in front of entrances. | Prevents **brute force attacks** like vehicles driving through the front of a building. |

### 3. Personnel, Surveillance, and Sensors

* **Security Guards / Receptionists:** Actively check IDs/badges against access control lists, record visitor logs, and deter incidents like **tailgating**.
* **Video Surveillance (CCTV):** Transmits signals from cameras to monitors. Provides **reliable proof** of a person's location and activity (harder to refute than digital logs).
    * Features: Often includes **motion detection** and **object detection**.
    * Compensating Control: A CCTV system can serve as a temporary **compensating control** while waiting for a more permanent system (like smart card access) to be implemented. 
* **Sensors:** Used to detect changes in the environment and trigger alarms or lighting. Common types include:
    * **Motion Detection:** Detects movement to trigger full lighting or alarms (when areas are empty).
    * **Noise Detection:** Detects sounds (e.g., glass breaking, exceeding a noise level).
    * **Infrared:** Detects heat signatures (infrared radiation) from people or animals, even in darkness.
    * **Pressure:** Detects changes in pressure on a surface (e.g., floor mats, doors).
    * **Microwave/Ultrasonic:** Detects movement or presence using reflected waves/sound.

### 4. Asset Management

**Asset management** is the process of tracking valuable assets (hardware, software, data) throughout their life cycles to ensure the organization knows what it owns, its location, and how it is secured.

| Asset Management Type | Focus | Security Benefit |
| :--- | :--- | :--- |
| **Hardware Asset Management** | Tracking physical devices (servers, laptops, network devices). | Reduces **system sprawl** (excess, underutilized systems) and **undocumented assets**. Methods often include **RFID tags** for automated inventory control. |
| **Software Asset Management** | Tracking software licenses, installations, and usage. | Ensures **compliance** with licensing agreements and minimizes security risks from unpatched or unauthorized software. |
| **Data Asset Management** | Tracking databases, files, and information repositories. | Defines data ownership, classification, and access controls, ensuring the **Confidentiality, Integrity, and Availability (CIA)** of data. |

### 5. Layered Security and Attack Types

* **Defense in Depth (Layered Security):** Implementing several layers of protection using **platform diversity** (different vendors, technologies, and controls). If one layer fails, others remain to protect the assets.
* **Vendor Diversity:** Using security controls from different vendors (e.g., two different firewalls) so a vulnerability in one doesn't compromise the entire defense.
* **Physical Attack Types:**
    * **Card Skimming/Cloning:** Capturing magnetic stripe data (skimming) and copying it onto a new card (cloning).
    * **Brute Force Attacks:** Attempts to simply crash through physical controls (e.g., driving a vehicle through a door, trying every possible PIN).
    * **Environmental Attacks:** Attacks that disrupt power or environmental conditions (e.g., cutting power, raising temperature, flooding) required by data centers.

## Adding Redundancy and Fault Tolerance

Redundancy adds duplication to critical system components and networks to provide **fault tolerance**. A system with fault tolerance can suffer a component failure but still continue to operate, thereby increasing reliability and availability (resiliency).

### 1. Single Point of Failure (SPOF)

A **single point of failure** is any component whose failure causes the entire system or service to fail. Organizations remove SPOFs to increase reliability and availability.

| Component | SPOF Risk | Redundancy/Mitigation |
| :--- | :--- | :--- |
| **Disk** | A single drive failure crashes the system. | **RAID** (Redundant Array of Inexpensive Disks). |
| **Server** | Failure of a single critical server halts the service. | **Load balancing** (Active/Active or Active/Passive clustering). |
| **Power** | Failure of the single power source. | **UPSes**, dual power supplies, and **generators**. |
| **Personnel** | Only one person can perform a critical task (e.g., helicopter pilot, vulnerability scanner operator). | Cross-training, proper documentation, and well-defined business continuity plans. |

### 2. Disk Redundancies (RAID)

RAID provides fault tolerance for disks, increasing system availability. 

| RAID Level | Technique | Minimum Drives | Fault Tolerance | Usable Storage | Key Feature |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RAID-0** | Striping | 2 | None | Sum of all disks | **Highest performance** (speed), but no redundancy. |
| **RAID-1** | Mirroring | 2 | 1 disk failure | Half of total capacity | High read performance, high data protection. **Disk Duplexing** adds a second disk controller. |
| **RAID-5** | Striping with Parity | 3 | 1 disk failure | $N-1$ disks | Parity information is spread across all disks. |
| **RAID-6** | Striping with Dual Parity | 4 | **2 disk failures** | $N-2$ disks | Provides higher fault tolerance for critical data storage. |
| **RAID-10** | Mirroring and Striping (1+0) | 4 | Up to half the disks (in mirrored sets) | Half of total capacity | Provides the best combination of performance and redundancy. |

### 3. Server Redundancy and High Availability

**High Availability (HA)** aims for a service to remain operational with almost zero downtime (e.g., 99.999% or "five nines" uptime).

#### Load Balancers (Clustering)
Load balancers distribute data loads across multiple servers (in a cluster or web farm) to provide **scalability** (handling more clients) and **high availability** (if one server fails, others continue service).

| Configuration | Description | Function | SPOF Mitigation |
| :--- | :--- | :--- | :--- |
| **Active/Active** | All servers in the cluster are actively processing requests. | Distributes traffic equally among servers (e.g., round-robin or least utilized). | If one server fails, the load balancer stops sending requests to it, maintaining service. |
| **Active/Passive** | One server is active; the other(s) are inactive (standby). | The inactive server takes over (**failover**) if the active server fails (detected via **heartbeat** connection). Both nodes typically access shared external storage.  | Ensures service continuity with minimal interruption during failover. |

| Load Balancing Scheduling Methods | Description |
| :--- | :--- |
| **Round-Robin** | Sends requests to servers in a sequential, rotating fashion. |
| **Least Used** | Automatically detects the load and sends new clients to the server with the lowest utilization. |
| **Source Address Affinity** (Session Persistence) | Directs a user's requests to the same server for the entire session based on their source IP address. |

#### NIC Teaming
**NIC Teaming** groups two or more physical network adapters into a single virtual adapter.
* **Benefit 1 (Performance):** Increases bandwidth capacity and uses load-balancing algorithms for outgoing traffic.
* **Benefit 2 (Redundancy):** Eliminates the physical NIC as a SPOF; if one NIC fails, the team continues to operate.

### 4. Power Redundancies

Power redundancies ensure fault tolerance and high availability for mission-critical systems.

| Control | Function | Security Benefit |
| :--- | :--- | :--- |
| **Uninterruptible Power Supply (UPS)** | Provides **short-term power** during a power fluctuation or outage. | Allows for a graceful shutdown of systems or keeps them running until generators start. |
| **Dual/Redundant Power Supply** | A second power supply in a device that automatically takes over if the primary one fails. | Eliminates the single power supply as a SPOF. Most are **hot-swappable**. |
| **Generators** | Provides **long-term power** during extended outages (days or weeks). | Ensures business continuity during prolonged power loss (e.g., natural disasters). |
| **Managed PDUs** (Switched) | Distributes power to devices in a rack, while also **monitoring and reporting** power quality (voltage, current, consumption) to a central console. | Allows administrators to centrally monitor and manage power usage. |

## Protecting Data with Backups

**Backups** are copies of data used for restoration if the original data is lost (e.g., due to fire, disk failure, or **ransomware**). Redundancy (like RAID) and backups are **not** the same; redundancy protects against component failure, while backups protect against site destruction or data corruption.

### 1. Backup Media and Storage

| Media/Method | Description | Key Feature |
| :--- | :--- | :--- |
| **Tape** | Traditional, inexpensive, and high-capacity media. | Most common media for long-term or offsite storage. |
| **Disk** | Stored on local or USB hard drives. | Faster access than tape, but more expensive. |
| **Network-Attached Storage (NAS)** | A dedicated computer (often Linux-based) providing **file-level data storage** via a standard Ethernet connection. | Simple, centralized file storage accessible on the network. |
| **Storage Area Network (SAN)** | Provides **block-level data storage** via a full network (typically Fibre Channel or high-speed Ethernet). | Used for high-speed access to disk arrays and **real-time replication**. |
| **Cloud Storage** | Backups stored with major cloud providers (AWS, Google, Azure). | Provides geographic redundancy and automatic encryption. |

### 2. Online vs. Offline Backups

| Category | Typical Meaning (General) | Database Context |
| :--- | :--- | :--- |
| **Offline Backup** | Stored on traditional media *within* the network (tapes, local disks, NAS). | A **cold backup** performed while the database is **offline** (local backup). |
| **Online Backup** | Stored in the **cloud** (accessible via the Internet). | A **hot backup** performed while the database is **operational** (captures and applies changes). |

### 3. Backup Types and Strategies

Backup utilities use different types of backups to balance storage cost (money) and backup/restore time. 

| Backup Type | Description | Time to Backup | Recovery Time |
| :--- | :--- | :--- | :--- |
| **Full (Normal)** | Backs up **all** selected data. | Longest | **Quickest** (only one backup set to restore). |
| **Differential** | Backs up all data changed **since the last full backup**. | Grows steadily during the week. | Quick (only requires the full + the latest differential). **Restores with 2 tapes/sets.** |
| **Incremental** | Backs up all data changed **since the last full or incremental backup**. | Shortest (only 1 day's changes). | Longest (requires restoring the full + *every* incremental set in order). **Restores with N tapes/sets.** |
| **Snapshot/Image** | Captures data at a **point in time**. | Varies | Quick reversion (commonly used for Virtual Machines before risky changes). |

| Strategy Goal | Recommended Backup Strategy |
| :--- | :--- |
| **Minimize Backup Time** (e.g., limited maintenance window) | **Full / Incremental** (Incremental backups are small and fast). |
| **Minimize Restore Time** (e.g., quick recovery is critical) | **Full / Differential** (Only requires restoring two backup sets). |

#### Advanced Techniques
* **Replication:** Creating an exact copy of data or a system in real-time or near-real-time to maintain a secondary site or system.
* **Journaling:** Recording changes to data sequentially in a separate log (**journal**) to quickly recover data to its most recent state by applying the changes to a previous backup.

### 4. Backup Integrity and Geographic Considerations

* **Testing Backups:** The **test restore** is the only reliable way to validate a backup's integrity. It should be performed regularly to verify the process and ensure administrators are familiar with restoration procedures.
* **Encryption:** Crucial for protecting sensitive data in backups both in transit and at rest, mitigating the risk of data breaches even if the backup media is stolen.

| Geographic Consideration | Description | Security/Compliance Impact |
| :--- | :--- | :--- |
| **Offsite vs. Onsite** | At least one copy must be stored **offsite** to protect against a disaster destroying the primary site. Onsite copies offer faster recovery time. | Offsite storage provides protection against single site disasters (e.g., fire, flood). |
| **Distance** | The geographic dispersal (distance) between the main site and the offsite location. May be close (for quick retrieval) or far (to avoid regional disasters). | Ensures an event at the primary site doesn't affect the backup location (e.g., an earthquake). |
| **Legal Implications** | Backups containing sensitive data (e.g., PII, PHI) must be protected according to governing laws. | Ensures legal compliance and data confidentiality. |
| **Data Sovereignty** | Data stored in a different country (often via cloud providers) is subject to **that country's laws and regulations**. | Must be considered to avoid legal/regulatory non-compliance. |

## Comparing Business Continuity Elements

**Business Continuity Planning (BCP)** helps an organization prepare for and survive potential outages (Environmental, Human-made, Internal, or External) of critical services. It includes a **Disaster Recovery Plan (DRP)**, which details the steps to restore critical functions after an outage.

### 1. Business Impact Analysis (BIA) Concepts

A **Business Impact Analysis (BIA)** identifies an organization's most critical systems and functions. It helps management prioritize recovery efforts.

| Concept | Description |
| :--- | :--- |
| **Mission-Essential Functions** | Activities that **must** continue or be restored quickly after a disaster (e.g., online sales, customer fund access). |
| **Vulnerable Business Processes** | Processes that support mission-essential functions (e.g., a multi-step shopping cart path). |
| **Maximum Downtime Limit** | The maximum allowable outage time for critical systems; exceeding this limit results in unacceptable impact. |
| **Site Risk Assessment** | A focused assessment of risks unique to a specific geographic location or site (e.g., hurricanes in Florida, earthquakes in California). |

#### Recovery Objectives

The BIA output drives the calculation of two critical recovery metrics:

| Metric | Definition | Derived From | Goal |
| :--- | :--- | :--- | :--- |
| **Recovery Time Objective (RTO)** | The **maximum amount of time** it can take to restore a system after an outage. | Maximum allowable outage time identified in the BIA. | Minimize downtime (e.g., 5 minutes for a critical web server). |
| **Recovery Point Objective (RPO)** | The **maximum amount of data loss** (measured as a point in time) that is acceptable. | Business tolerance for data loss. | Minimize lost data (e.g., 1 week for archived data; up-to-the-minute for transactions). |

#### Reliability Metrics

| Metric | Definition | Purpose |
| :--- | :--- | :--- |
| **Mean Time Between Failures (MTBF)** | The average time between failures (usually in hours). | Measures a system's **reliability**; higher numbers indicate better performance. |
| **Mean Time to Repair (MTTR)** | The average time it takes to restore/recover a failed system. | Specifies service contract expectations for system restoration time. |

### 2. Continuity of Operations Planning (COOP)

**COOP** focuses on restoring mission-essential functions at an alternate processing site (**recovery site**) when the primary site is unavailable (**failover**). 

| Recovery Site Type | Readiness / Status | Cost | Recovery Time | Key Feature |
| :--- | :--- | :--- | :--- | :--- |
| **Hot Site** | Fully equipped with hardware, software, connectivity, and **up-to-date data** (24/7). | Most expensive | **Shortest** (minutes to an hour). | Best for high-availability requirements. |
| **Warm Site** | Includes necessary **hardware** and connectivity, but may require installation of software and restoration of recent data. | Moderate | Medium (hours to days). | A common compromise between cost and recovery time. |
| **Cold Site** | Basic facility with power, water, and connectivity, but **no equipment or data**. | Least expensive | Longest (days to weeks). | All hardware, software, and data must be brought in and configured upon activation. |

> **Geographic Dispersion:** Recovery sites must be located far enough from the primary site to ensure they are not affected by the same disaster.

### 3. Disaster Recovery Plan (DRP)

The DRP identifies the steps to recover critical systems. A DRP includes a **hierarchical list** that prioritizes what systems and services must be restored first (Critical Business Functions and Security Services come first).

| DRP Phase | Action |
| :--- | :--- |
| **Activation** | DRP is initiated (imminent or immediate). |
| **Implement Contingencies** | Moving critical functions to an alternate site (failover) or retrieving off-site backups. |
| **Recover Critical Systems** | Restoring systems according to the hierarchical priority list and reviewing change management. |
| **Test Recovered Systems** | Verifying system functionality and comparing with performance baselines before bringing them online. |
| **After-Action Report** | A formal review ("lessons learned") to identify successful/failed steps and update the DRP. |

### 4. Testing Plans with Exercises

Testing validates that the BCP and DRP are effective and ensures personnel are familiar with procedures.

| Exercise Type | Description | Effect on Systems |
| :--- | :--- | :--- |
| **Tabletop Exercise** | **Discussion-based** hypothetical scenario walk-through (e.g., in a conference room). | None (Theoretical only). |
| **Simulations** | **Hands-on** functional exercise using a **simulated/test environment**. | None (Does not affect production systems). |
| **Parallel Processing** | The recovery site is **activated and runs alongside** the primary site. | Runs in parallel with primary; no interruption. |
| **Failover Tests** (Full Interruption) | The **primary site is shut down** to force the recovery site to take over and handle the full load. | Highly disruptive to the organization; ultimate test of plan viability. |

## Capacity Planning

**Capacity planning** is the process of determining the resources required (People, Technology, and Infrastructure) to meet the current and future demands of an organization. This helps maintain **business continuity**, optimize performance, and prevent disruptions. 

| Area of Capacity Planning | Focus | Goal |
| :--- | :--- | :--- |
| **People (Human Resources)** | Analyzing current workforce skills, identifying gaps, and forecasting future staffing needs. | Ensures the organization has the necessary expertise and staffing levels (hiring, training, retaining) to meet objectives. |
| **Technology** | Determining the required hardware, software, and network resources. | Estimates computing power, storage, and bandwidth needed to handle current and future workloads, avoiding bottlenecks and ensuring high availability. |
| **Infrastructure** | Evaluating and managing physical facilities (data centers, office spaces, critical assets). | Ensures adequate space, power, cooling, and essential resources to support business continuity and projected growth. |


