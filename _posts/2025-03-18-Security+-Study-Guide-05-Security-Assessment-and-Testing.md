"Cybersecurity professionals are responsible for building, operating, and maintaining security controls that protect against these threats. An important component of this maintenance is performing regular security assessment and testing to ensure that controls are operating properly and that the environment contains no exploitable vulnerabilities."

## Vulnerability Management
*Vulnerability management* programs:
- identify 
- prioritize 
- remediate 
- Use *vulnerability scanning* to detect vulnerabilities

##### NOTE
examples based around **Nessus**

### Identifying Scan Targets
- *asset inventory* a database built via network scans
- *Asset inventory* and *asset criticality* determines:
	- type of scans
	- frequency
	- priority of remediation

### Determining Scan Frequency
"Vulnerability scanning tools allow the automated scheduling of scans to take the burden off administrators."
- "The organization's *risk appetite* is its willingness to tolerate risk within the environment."
- *Regulatory requirements*, *Payment Card Industry Data Security Standard* (**PCI DSS**), *Federal Information Security Modernization Act* (**FISMA**), dictate scan frequency.
- *Technical constraints* may limit scanning frequency.
- *Business constraints* may limit timeframes
	- Retail business during the holiday season
- *Licensing limitations* may limit the bandwidth and/or number of scans
- Best practice to start slow and expand scans overtime.

### Configuring Vulnerability Scans
"It is important to conduct regular configuration reviews of vulnerability scanners to ensure that scan settings match current requirements."

#### Scan Sensitivity Levels
- Start with a template and adjust according to needs and save as new template.
- Sensitivity control types of scans

##### Warning
"Some plug-ins perform tests that may actually disrupt activity on a production system or, in the worst case, damage content on those systems." 
- *intrusive plug-ins* can be turned off 
- *nonintrusive plug-ins* should be left on
- Test environments can be used to mimic the real environment, and can then have the *intrusive plug-ins* ran just in case.

#### Supplementing Network Scans
- "Basic vulnerability scans run over a network, probing a system from a distance."
- May also cause false positives
- **supplement with trusted server configurations**
	- Scanner can be provided credentials to scan a target server

##### EXAM NOTE
"understand the differences between credentialed and noncredentialed scanning!"
- enforce the principle of least privilege
- provide scanner with read-only access

- *agent-based scanning* providing an “inside-out” vulnerability scan and reports findings to the vulnerability management platform

##### TIP
- beginning with a small pilot deployment
- after review of performance, procced with widespread deployment

#### Scan Perspective
- Based on where the scan initiates determines what vulnerabilities it'll find.
- Affecting Controls:
	- Firewall Settings
	- Network Segmentation
	- *Intrusion Detection Systems* (**IDS**s)
	- *Intrusion prevention systems* (**IPS**s)

##### NOTE
- supplement with scan from a *Approved Scanning Vendor* (**ASV**)

### Scanner Maintenance
##### TIP
- Scanning system can automatically update
- However, it's still Admin responsibility to manually check on a regular basis.

#### Scanner Software
- even vulnerability scanners can have security issues
- *Are they rootkits the way anti-cheat software is?*

#### Vulnerability Plug-in Feeds
- "Administrators should configure their scanners to retrieve new plug-ins on a regular basis, preferably daily."

##### Security Content Automation Protocol (SCAP)
- standard lead by *National Institute of Standards and Technology* (**NIST**)
	- *Common Configuration Enumeration* (**CCE**) system configuration issues
	- *Common Platform Enumeration* (**CPE**) product names and versions
	- *Common Vulnerabilities and Exposures* (**CVE**) security-related software flaws
	- *Common Vulnerability Scoring System* (**CVSS**) severity ranking of security-related software flaws
	- *Extensible Configuration Checklist Description Format* (**XCCDF**) A language for specifying checklists and reporting checklist results
	- *Open Vulnerability and Assessment Language* (**OVAL**) A language for specifying low-level testing procedures used by checklists
	- see NIST SP 800-126: [csrc.nist.gov/projects/security-content-automation-protocol](http://csrc.nist.gov/projects/security-content-automation-protocol) 

##### EXAM NOTE
- CompTIA uses **CVE** as *Common Vulnerability Enumeration*
- Professionals use **CVE** as *Common Vulnerabilities and Exposures*
- Map **CVE** to the meaning "standard naming system for flaws"

### Vulnerability Scanning Tools
- Toolkit:
	- vulnerability scanner
	- application scanner
	- web application scanner

#### Infrastructure Vulnerability Scanning
- Probes a wide range of network-connected devices for known vulnerabilities
- network vulnerability scanners:
	- Nessus: longest established software 
	- Qualys: newer, and uses SaaS model to test local and in the cloud
	- Rapid7's Nexpose: similar to the above
	- OpenVAS: is **FOSS** under **GNU GPL**
		- [https://en.wikipedia.org/wiki/OpenVAS](https://en.wikipedia.org/wiki/OpenVAS)

#### Application Testing
- analyze custom-developed software
- Three techniques:
	1. *Static testing* analyzes code without executing it
	2. *Dynamic testing* executes code as part of the test
	3. *Interactive testing* combines static and dynamic testing
- Should be apart of any software development process.

#### Web Application Scanning
- test for web-specific vulnerabilities
	- **SQL** injection
	- cross-site scripting (**XSS**)
	- cross-site request forgery (**CSRF**)
		- *Why not XRF then?*
- Nikto is **FOSS** under **GNU GPL**
	- [https://en.wikipedia.org/wiki/Nikto_(vulnerability_scanner)](https://en.wikipedia.org/wiki/Nikto_(vulnerability_scanner))

### Reviewing and Interpreting Scan Reports
- These reports offer details that make it easier for admins to understand and repair vulnerabilities.
- Also provides references:
	- *Internet Engineering Task Force* (**IETF**) documentation
- *output* section provides "verbatim output returned by a command"
- *risk information* section uses the *Common Vulnerability Scoring System* (**CVSS**)

#### Understanding CVSS
##### EXAM NOTE
- recall that **CSSS** is part of **SCAP**
- rated on 0 - 10 scale
- recall *Common Vulnerabilities and Exposures* (**CVE**) which lists: 
	- known vulnerabilities
		- contain an ID number 
		- description
		- reference

##### 8 metrics of a vulnerability
###### 1. Attack Vector Metric
- *attack vector metric* (**AV**) how an attacker would exploit
###### 2. Attack Complexity Metric
- *attack complexity metric* (**AC**) difficulty of exploiting 
###### 3. Privileges Required Metric
- *privileges required metric* (**PR**) type of account access needed
###### 4. User Interaction Metric
- *user interaction metric* (**UI**) whether the attacker needs another human 
###### 5. Confidentiality Metric
- *confidentiality metric* (**C**) type of information disclosure 
###### 6. Integrity Metric
- *integrity metric* (**I**) type of information alteration 
###### 7. Availability Metric
- *availability metric* (**A**) type of disruption
###### 8. Scope Metric
*scope metric* (**S**) effected system components beyond the initial scope

###### NOTE
- current CVSS v3.1
- v2.0 used 6 metrics

##### Interpreting the CVSS Vector
- CVSS vector uses a single-line format:
	- `CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N`

##### Summarizing CVSS Scores
- analysts can calculate the *CVSS base score*
###### CALCULATING THE IMPACT SUB-SCORE (ISS)
`ISS = 1 - [(1-Confidentiality)*(1-Integrity)*(1-Availability)]`

###### NOTE
- Don't have to calculate CVSS score manually:
	- [www.first.org/cvss/calculator/3.1](http://www.first.org/cvss/calculator/3.1)

##### CATEGORIZING CVSS BASE SCORES
Scores converted to categories
| CVSS Score | Rating   |
|------------|----------|
| 0.0        | None     |
| 0.1-3.9    | Low      |
| 4.0-6.9    | Medium   |
| 7.0-8.9    | High     |
| 9.0-10.0   | Critical |

###### EXAM NOTE
- **Be familiar with CVSS severity rating scale** 

### Confirmation of Scan Results
#### False Positives
- *false positive error* nonexistent vulnerability
- *positive report* found vulnerability
	- *true positive* accurate
	- *false positive* inaccurate
- *negative report* no vulnerability found
	- *true negative* accurate
	- *false negative* inaccurate

##### EXAM NOTE
- focus on **false positives** and **false negatives**
	- Must be able to identify them in a scenario.

#### Reconciling Scan Results with Other Data Sources
- *Log Reviews* 
- *Security information and event management* (**SIEM**) systems
- *Configuration management systems* 


## Vulnerability Classification
### Patch Management
- Security patches are vital, but also the first thing to fall to waist side "due to a **lack of resources for preventive maintenance**".

### Legacy Platforms
- Software eventually reaches end-of-life and should be discontinued when the security updates end.
	- "2015 when Microsoft discontinued support for the more than two decades old Windows Server 2003"
	- Where it's not possible to upgrade, it's best practice to isolate the system from the rest of the network as much as possible.

##### EXAM NOTE
- vulnerability response and remediation practices:
	- patching
	- insurance
	- segmentation
	- compensating controls
	- exceptions
	- exemptions

### Weak Configurations
- Default settings
- Default credentials
	- *admin, admin anyone?*
- Open service ports that are not necessary
- Open permissions
	- violates **least privilege** principle

### Error Messages
- *debug modes* give developers crucial information.
	- However, debug mode can be used by attackers
- "software development should always take place in a dedicated development environment"
	- Private network
	- Only environment with debug option

### Insecure Protocols
- Telnet
	- replaced with SSH
- FTP
	- *Secure File Transfer Protocol* (**SFTP**)
	- *FTP-Secure* (**FTPS**)
	- *Why two?*

### Weak Encryption
- see Chapter 7 Cryptography and the PKI
- Two important choices:
	1. Algorithm to use
	2. Encryption key
-  *Advanced Encryption Standard* (**AES**)


## Penetration Testing
The process by which a "White Hat"/"Red Team" uses technical tools to test the organizations security policies. Often IT systems, but can also include it's people. see [Social Engineering And Password Attacks](https://pbrazeale.github.io/Security+-Study-Guide-04-Social-Engineering-and-Password-Attacks/)

### Adopting the Hacker Mindset
- Instead of focusing on the security design overview, find a weakness and exploit it.
	- Only needs 1 way to be right
	- Where "Blue Team" must also be right.

### Reasons for Penetration Testing
- *security operations centers* (**SOC**s)
- It's the only/best method for testing against an attack before it actually happens.
	- Same reason we have fire drills. **Just in case**

### Benefits of Penetration Testing
- Provides an assessment of organizations security robustness.
	- *Leading to lower insurance rates?*
- In the case "Red Team" CTF "Blue Team" can analyze the steps used, and fix now known security holes.
- Great for testing a new critical system before deployment.
	- The internet is vast

#### Threat Hunting
- They search for evidence that a past attack had occurred.
- cybersecurity philosophy known as the “presumption of compromise”

### Penetration Test Types
- 4 major categories:
	1. *Physical* security controls: doors, locks, cameras, etc...
	2. *Offensive* tests: networks, systems, and applications
	3. *Defensive* tests "Blue Team" active skills
	4. *Integrated* combines offensive and defensive pentesting
- 3 types of pentester's knowledge:
	1.  *Known environment* complete scope, beyond a normal attacker
		1. *Maybe tests against an insider threat? Former employee.*
	2. *Unknown environment* replicate attacker's real-world experience.
		1. Only as valuable as the skillset of the "Red Team"
	3. *Partially known environment* used to focus the pentesting toward relevant systems, and create a more efficient test, without going fully Known Environment.

##### EXAM NOTE
- Know the 4 pentest categories and 3 pentest types 

### Rules of Engagement
- *rules of engagement* (**RoE**)
	- *timeline* window for the attack
	- *locations, systems, applications, potential targets* especially where 3rd party services are involved
	- *Data handling* NDAs for the data found, and procedures for shredding after
	- *behaviors* what defenses the "Blue Team" will use during the test
	- *resources* usually how many man hours will be committed
	- *Legal concerns* (*physical pentest needs a waver for law enforcement just in case?*)
	- *communications* when to send updates, and what to do when evidence of  breach is found

#### Permission
- "get our of jail free card"

### Reconnaissance
- *Passive reconnaissance* was partially covered in [Cybersecurity Threat Landscape](https://pbrazeale.github.io/Security+-Study-Guide-02-Cybersecurity-Threat-Landscape/) **OSINT**
- *Active reconnaissance*:
	- intelligence gathering [Social Engineering And Password Attacks](https://pbrazeale.github.io/Security+-Study-Guide-04-Social-Engineering-and-Password-Attacks/)
	- *footprinting* identify OS and applications
	- Port scanning
	- Vulnerability scanning

##### EXAM NOTE
- Know the difference between passive and active reconnaissance

- *war driving* using a mobile vehicle with powerful antennas to capture wireless packets
- *war flying* is above but with UAVs

### Running the Test
- covered more about *Cyber Kill Chain* in Ch14 Monitoring and Incident Response
- Key phases:
	- *Initial access*
	- *Privilege escalation*
	- *Pivoting and lateral movement*
	- *Persistence*
- *Exploitation frameworks* (**Metasploit**) provide a modular approach

### Cleaning Up
- remove all tool installed
- delete all data exfiltrated
- provided report of what was found and how to patch/protect against it


## Audits and Assessments
- 3 major components of a security assessment program
	1. Security tests
	2. Security assessments
	3. Security audits

### Security Tests
- verify control is functional
- should occur on a regularly scheduled timeframe

#### WARNING
"Experimentation with new tools is fine, but security testing programs should be carefully designed and include rigorous, routine testing of systems using a risk-prioritized approach."

##### Responsible Disclosure Programs
"Bug bounty programs are a type of responsible disclosure program that incentivizes responsible disclosure submissions by offering financial rewards (or “bounties”) to testers who successfully discover vulnerabilities."
- *Funnel curiosity toward a productive end rather than risk selling to the highest bidder?*
 
### Security Assessments
- Comprehensive reviews of the system and application
- Normally result in a non-technical report to upper management about the risks and possible solutions.
- Often conducted by outside teams

### Security Audits
- Similar to assessments, but **must** be conducted by an independent auditor.
- Assessments are internal benchmarks.
- Audits are meant for reporting to third parties.
- Objective is *attestation*: the auditor signs off that the controls are "adequate to meet the control objectives and working properly"

#### Internal Audits
- Report direct to the CEO or sometimes the Chief Audit Executive (**CAE**)
- Often prepare in advance of an external audit

#### External Audits
- Big 4 Firms:
	- Ernst & Young
	- Deloitte
	- PricewaterhouseCoopers (PwC)
	- KPMG

#### Independent Third-Party Audits
- A regulatory body contracts them out.

##### EXAM NOTE
Independent Third-Party Audits are a subcategory of external, and are differentiated based on if the organization requests the audit, or third party (IE regulators)

"The *American Institute of Certified Public Accountants* (**AICPA**) released a standard designed to alleviate this burden. The *Statement on Standards for Attestation Engagements document 18* (**SSAE 18**), titled Reporting on Controls, provides a common standard to be used by auditors performing assessments of service organizations with the intent of **allowing the organization to conduct an external assessment** instead of multiple third-party assessments and then sharing the resulting report with customers and potential customers.

SSAE 18 engagements are commonly referred to as *service organization controls* **(SOC) audits**."

#### Auditing Standards
- *Control Objectives for Information and related Technologies* (**COBIT**)
	- *Information Systems Audit and Control Association* (**ISACA**)
		- *Certified Information Systems Auditor* (**CISA**)
		- *Certified Information Security Manager* (**CISM**)
- ISO 27001 security management system
- ISO 27002 information security controls


## Vulnerability Life Cycle
- LOOP
	- Identification
	- Analysis
	- Response and Remediation
	- Validation of Remediation
	- Reporting


## Review Questions (13/20) 65%
4.0 Security Operations is 28% of the exam, 5.0 Security Program Management and Oversight is 20%. With a 65% knowledge coverage, I'd fail the certification exam, and rightfully so. Again I second guessed myself during the test, but that's obviously a root issue of not fully knowing the information. 

At this rate I'll not sit the exam next month, and instead need another month to drill this information. Especially the acronyms!

### Correct
1, 3, 5, 6, 8, 10, 12, 13, 14, 16, 17, 18, 19

### Incorrect
2, 4, 7, 9, 11, 15, 20
- 2, I should have known better. Obviously "read-only"
- 4, Misread the question, but no excuse
- 7, Took a guess based on word recognition
- 9, second guessed myself
- 11, second guessed myself
- 15, second guessed myself, but I really didn't know
- 20, second guessed myself, but again need to drill acronyms.
