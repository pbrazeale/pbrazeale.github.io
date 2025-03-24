+++
tags = ['CompTIA', 'Security+', 'Linux', 'Networking', 'Cybersecurity']
title = 'Security+ Study Guide: Ch02 Cybersecurity Threat Landscape'
date = 2025-03-14T08:34:07+01:00
draft = false
+++

"Cybersecurity threats have become increasingly sophisticated and diverse over the past few decades. An environment that was once populated by lone hobbyists is now shared by skilled technologists, organized criminal syndicates, and even government-sponsored attackers, all seeking to exploit the digital domain to achieve their own objectives."

## Exploring Cybersecurity Threats

### Classifying Cybersecurity Threats

- **Internal vs. External**
- **Level of Sophistication/Capability**
  - _advanced persistent threat_ (**APT**)
- **Resources/Funding**
- **Intent/Motivation**

##### The Hats Hackers Wear

- "White Hat" Authorized attackers
- "Black Hat" Malicious attackers
- "Gray Hat" Semi-authorized attackers
  - "They act without proper authorization, but they do so with the intent of informing their targets of any security vulnerabilities."
  - Fully punishable under the law, regardless of intent.
  - _Does bounty hunting count as Gray or White?_

### Threat Actors

##### Exam Note

"Be certain that you understand the differences between unskilled attackers; hacktivists; organized crime; advanced persistent threats (**APT**s), including nation-state actors; and shadow IT."

#### Unskilled Attackers

- _script kiddie_ is a derogatory term for _unskilled attackers_
  - Often rely entirely on tools/scripts downloaded from the internet.
  - denial-of-service (**DoS**)
- Technical skills are no longer a barrier to attacking a network.
- Often targets are random and hacking is done simply to prove skills.
  - _Done for the LOLz_

#### Hacktivists

- hack to accomplish an activist goal.
  - _cyber terrorism?_
- "They may even view being caught as a badge of honor and a sacrifice for their cause."
- Some hacktivists are cybersecurity professionals by day.
- some are part of organized efforts
  - Anonymous
- sometimes internal employees turn hacktivist.
  - many people consider Edward Snowden a hacktivist

#### Organized Crime

- Almost entirely motivated by financial gain.
- In their 2021 Internet Organized Crime Threat Assessment (IOCTA), the European Union Agency for Law Enforcement Cooperation (EUROPOL) found that organized crime groups were active in a variety of cybercrime categories, including the following:
  - _Cyber-dependent crime_
    - ransomware
  - _Child sexual abuse material_
  - _Online fraud_
    - CC fraud
  - _Dark web activity_
    - sale of illegal goods and services
  - _Cross-cutting crime factors_
    - social engineering
    - money mules

#### Nation-State Attackers

- "_advanced persistent threats_ (**APT**s) describes a series of attacks that they first traced to sources connected to the Chinese military."
  - Room 39
- motive can be political or economic
  - often traditional espionage goals

##### Zero-Day Attacks

- unknown security vulnerability
  - "Attacks that exploit these vulnerabilities are known as zero-day attacks."
  - "The Stuxnet attack, traced to the U.S. and Israeli governments, exploited zero-day vulnerabilities to compromise the control networks at an Iranian uranium enrichment facility."

#### Insider Threat

- "Behavioral assessments are a powerful tool in identifying insider attacks. Cybersecurity teams should work with human resources partners to identify insiders exhibiting unusual behavior and intervene before the situation escalates."

##### The Threat of Shadow IT

- Dropbox to sync work and personal computers
  - Not malicious, actually meant to increase productivity.
- "Cybersecurity teams should remain vigilant for shadow IT adoption and remember that the presence of shadow IT in an organization means that business needs are not being met by the enterprise IT team."

#### Competitors

- Corporate espionage in the 21st century.
  - Hackers sell stolen data from a breach.
  - Insiders sell smuggled data for revenge.
  - Some dark web markets advertise to buy confidential data.
- "You should conduct periodic organizational threat assessments to determine what types of threat actors are most likely to target your organization, and why."

### Attacker Motivations

Primary motivations behind cyberattacks:

- _Data exfiltration_
- _Espionage_
- _Service disruption_
- _Blackmail_
- _Financial gain_
- _Philosophical/political_
- _Ethical/White Hat_
- _Revenge_
- _Disruption/chaos_
- _War_

##### Exam Note

"It is very likely you will be asked to compare and contrast the various threat actors on the exam. You should know the attributes and motivations behind each."

### Threat Vectors and Attack Surfaces

**_Attack Surface_**

- System
- Application
- Service

**_Threat Vector_**

- the means that threat actors use to obtain access.

#### Message-Based Threat Vectors

1. Email
   1. Phishing
   2. Spam
   3. Email-born attacks
      1. (_malware attachments?_)

Also includes all other digital communication.

- _Short Message Service_ (**SMS**)
- _Instant Messaging_ (**IM**)
- "Voice calls may also be used to conduct _vishing_ (**voice phishing**) attacks"
- Social Media more broadly
  - see Chapter 4 Social Engineering and Password Attacks

#### Wired Networks

- Unprotected/monitored ethernet plugs
  - see Chapter 9 Resilience and Physical Security

#### Wireless Networks

- Wireless networks are even easier.
  - _Pineapple router_
  - Bluetooth can also prove an attack vector
  - see Chapter 13 Wireless and Mobile Security

#### Systems

"The operating system configuration may expose open service ports that are not necessary to meet business needs or that allow the use of well-known default credentials that were never changed."

- Old software with known vulnerabilities
- Outdated OS (_Windows XP_)
- see Chapter 11 Endpoint Security

#### Files and Images

- file that contains embedded malicious code

#### Removable Devices

- Malicious USBs
- see Chapter 11 Endpoint Security

#### Cloud

- Accidently leaked API keys
- see Chapter 10 Cloud and Virtualization Security

#### Supply Chain

- Attacks on the IT supply chain
- Also known to attack software
- _managed service providers_ (**MSP**s)

## Threat Data and Intelligence

"_Threat intelligence_ is the set of activities and resources available to cybersecurity professionals seeking to learn about changes in the threat environment."

- Can also be used for _predictive analysis_ to predict likely risks.
  - _open source intelligence_ (**OSINT**)
  - Threat Feeds
    - _Common Vulnerabilities and Exposures_ (**CVE**)
    - A must have for organizations
  - _Vulnerability databases_
    - _indicators of compromise_ (**IoCs**)

### Open Source Intelligence

- acquired from publicly available sources
- Senki.org provides a list: www.senki.org/operators-security-toolkit/open-source-threat-intelligence-feeds
- [Open Threat Exchange operated by AT&T](https://cybersecurity.att.com/open-threat-exchange)
- [MISP Threat Sharing project](www.misp-project.org/feeds)
- [https://threatfeeds.io](https://threatfeeds.io)

_Cybersecurity & Infrastructure Security Agency_ (**CISA**)

- Government sites:
  - [www.cisa.gov](www.cisa.gov)
  - U.S. Department of Defense Cyber Crime Center: [www.dc3.mil](www.dc3.mil)
- Vendor websites:
  - [www.microsoft.com/en-us/security/blog/topic/threat-intelligence](www.microsoft.com/en-us/security/blog/topic/threat-intelligence)
  - [https://sec.cloudapps.cisco.com/security/center/publicationListing.x](https://sec.cloudapps.cisco.com/security/center/publicationListing.x)
- Public sources:
  - SANS Internet Storm Center: [https://isc.sans.org](https://isc.sans.org)
  - VirusTotal: [https://virusshare.com](https://virusshare.com)
  - [www.spamhaus.org](www.spamhaus.org)

##### Exploring the Dark Web

- "The dark web is a network run over standard Internet connections but using multiple layers of encryption to provide anonymous communication."
- "The sudden appearance of credentials on dark web marketplaces likely indicates that a successful attack took place and requires further investigation."
- Tor browser: [www.torproject.org](www.torproject.org)

### Proprietary and Closed-Source Intelligence

- _Closed-Source Intelligence_ Commercial Security Vendors
  - "Commercial closed-source intelligence is often part of a service offering, which can be a compelling resource for security professionals."

##### When a Threat Feed Fails

- "In one case, a critical Microsoft vulnerability was announced, and exploit code was available and in active use within less than 48 hours. Despite repeated queries, the vendor did not provide detection rules for over two weeks."
- Have multiple feeds to check against each other

"_Threat maps_ provide a geographic view of threat intelligence."

### Assessing Threat Intelligence

- Evaluate a threat intelligence source:
  1.  Is it timely?
  2.  Is the information accurate?
  3.  Is the information relevant?
- Give it a _confidence score_

##### Assessing the Confidence Level of Your Intelligence

- Threat feeds use a score range
  - _Confirmed_ (90–100) uses independent sources or direct analysis to prove that the threat is real.
  - _Probable_ (70–89) relies on logical inference but does not directly confirm the threat.
  - _Possible_ (50–69) is used when some information agrees with the analysis, but the assessment is not confirmed.
  - _Doubtful_ (30–49) is assigned when the assessment is possible but not the most likely option, or the assessment cannot be proven or disproven by the information that is available.
  - _Improbable_ (2–29) means that the assessment is possible but is not the most logical option, or it is refuted by other information that is available.
  - _Discredited_ (1) is used when the assessment has been confirmed to be inaccurate or incorrect.

### Threat Indicator Management and Exchange

- "_Structured Threat Information eXpression_ (**STIX**) is an XML language originally sponsored by the U.S. Department of Homeland Security."
- STIX has been handed off to the _Organization for the Advancement of Structured Information Standards_ (**OASIS**)
- _Trusted Automated eXchange of Intelligence Information_ (**TAXII**)

### Information Sharing Organizations

- _Information Sharing and Analysis Centers_ (**ISAC**s) help infrastructure owners and operators share threat information
  - In 1998: part of _Presidential Decision Directive-63_ (**PDD-63**)

### Conducting Your Own Research

- Focus on: _tactics, techniques, and procedures_ (**TTP**s)

## Review Questions (17/20) 85%

Studied last night, and took this test during the afternoon without review. 85% is not great, but I think spacing out the studying and testing phases will provide a more accurate assessment of how much of the information has stuck.

### Correct

2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 14, 16, 17, 18, 19, 20

### Incorrect

1, 13, 15

- 1. need to review threat ratings
- 13. not sure why I chose source-code over API keys.
- 15. guessed RFC, likely from question 12, instead of IoC. Need to study my Acronym list/cards. [Security+ Acronym List](https://pbrazeale.github.io/Security+-6.0-Acronym-List/)
