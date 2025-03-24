+++
tags = ['CompTIA', 'Security+', 'Linux', 'Networking', 'Cybersecurity']
title = "Security+ Study Guide: Ch01 Today's Security Professional"
date = 2025-03-14T07:34:07+01:00
draft = false
+++

## Cybersecurity Objectives

![Triads](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.infosectrain.com%2Fwp-content%2Fuploads%2F2019%2F10%2Fpentester.jpg&f=1&nofb=1&ipt=666ab2d2e3465f5f18f1fdffda7ac3981a2ab6a1ce05001d132b9f89c2ba0bd4&ipo=images)

1. **Confidentiality** authorized users only.
2. **Integrity** authorized data modification only.
3. **Availability** proper redundancy of data and physical resources (_power, computers, etc..._)

"**Nonrepudiation**, while not part of the **CIA** triad, is also an important goal of some cybersecurity controls. Nonrepudiation means that someone who performed some action, such as sending a message, cannot later deny having taken that action."

## Data Breach Risks

**Security incidents** happen when the **CIA** is broken/violated.

- Malicious attack
- Accidental oversight
- Natural disaster

### The DAD Triad

![Triads](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.infosectrain.com%2Fwp-content%2Fuploads%2F2019%2F10%2Fpentester.jpg&f=1&nofb=1&ipt=666ab2d2e3465f5f18f1fdffda7ac3981a2ab6a1ce05001d132b9f89c2ba0bd4&ipo=images)

1. **Disclosure** when data violates the _confidentiality_ principle
   1. otherwise known as _data loss_
   2. Attackers remove information, _data exfiltration_
   3. Accidental, employee loses a device
2. **Alteration** when data violates _integrity_
   1. Attackers modify records
   2. power surge causing a “bit flip”
      1. [Cosmic particles change elections](https://www.independent.co.uk/news/science/subatomic-particles-cosmic-rays-computers-change-elections-planes-autopilot-a7584616.html)
         1. **In 2003 in Schaerbeek, Belgium, an SEU** (_single-event upset_) was responsible for giving a candidate in an election an extra 4,096 votes.
3. **Denial** violates the principle of availability
   1. **DDoS** distributed denial-of-service

The **CIA** and **DAD** triads are very useful tools for cybersecurity planning and risk analysis.

### Breach Impact

#### Financial Risk

- monetary damage to the organization as the result of a data breach.
- second-order consequence
  - Lost laptop _1st order_
  - _2nd order_ competitors gain hold of product plans on the laptop and beat the organization to market.

#### Reputational Risk

- when the negative publicity surrounding a security breach causes the loss of goodwill among customers, employees, suppliers, and other stakeholders.
- Identity Theft
  - The most common impact on these groups is the risk of identity theft posed by the exposure of _personally identifiable information_ (**PII**) to unscrupulous individuals.

#### Strategic Risk

- organization will become less effective in meeting its major goals and objectives as a result of the breach.
  - See laptop example above.
  - If the product plans were stolen, it would directly impact the organizations market strategies.

#### Operational Risk

- organization's ability to carry out its day-to-day functions.
  - Ransomware data encryption of hospital databases
    - [UnitedHealth ransomware attack](https://www.kaspersky.com/blog/unitedhealth-ransomware-attack/53065/)
- _Operational risk and strategic risk are closely related, so it might be difficult to distinguish between them._
  - If it could end the organization - Strategic
  - If it merely delays (recover via backups) - Operational

#### Compliance Risk

- _Health Insurance Portability and Accountability Act_ (**HIPAA**) requires that health-care providers and other covered entities protect the confidentiality, integrity, and availability of _protected health information_ (**PHI**).
  - see Chapter 16 Security Governance and Compliance

In most cases, a risk will cross multiple risk categories.

## Implementing Security Controls

- _control objectives_ level of protection required to preserve the confidentiality, integrity, and availability of data and systems.
- _Security controls_ are specific measures that fulfill the security objectives of an organization.

### Gap Analysis

- "During a gap analysis, the cybersecurity professional reviews the control objectives for a particular organization, system, or service and then examines the controls designed to achieve those objectives."
  - Chapter 5 Security Assessment and Testing

### Security Control Categories

Four categories based on their mechanism of action:

1. _Technical controls_ enforce **CIA** in digital space.
   1. Firewalls
   2. Access control lists
   3. intrusion prevention systems
   4. encryption
2. _Operational controls_: access reviews, log monitoring, and vulnerability management.
3. _Managerial controls_: mechanics of risk management process.
   1. Risk assessments
   2. security planning exercises
   3. incorporation of security into daily processes
4. _Physical controls_: typical thoughts of security.
   1. Locks
   2. Fire alarms
   3. etc...

### Security Control Types

1. _Preventive controls_
2. _Deterrent controls_
3. _Detective controls_
4. _Corrective controls_
5. _Compensating controls_: mitigate the risk associated with exceptions made to a security policy.
6. _Directive controls_:
   1. Policies and procedures are examples of directive controls.

#### Exploring Compensating Controls

_Payment Card Industry Data Security Standard_ (**PCI DSS**) sets 3 criteria:

1. Meet the rigor of the original.
2. Similar level of defense.
3. “above and beyond” other PCI DSS requirements.

**Example**: Running an outdated OS for a specific piece of software.

- Run the system on an isolated network, with little or no access to main/other networks.

Compensating Controls should only be used if absolutely necessary and only for as long as required to "bring the organization back into compliance".

## Data Protection

Data Three States:

1. _Data at rest_: resides on hard drives, tapes, in the cloud, or on other storage media.
2. _Data in transit_: motion/transit over a network.
3. _Data in use_: actively in use by a computer system.

### Data Encryption

- _Encryption_ technology uses mathematical algorithms to protect information.
- Chapter 7 Cryptography and the PKI

### Data Loss Prevention

- _Data loss prevention_ (**DLP**)
  DLP systems work in two different environments:

1. Agent-based DLP
   1. uses software to search systems for sensitive information.
      1. Can be removed or encrypted when found.
   2. monitor system configuration and user actions
      1. for instance blocking USB devices
2. Agentless (network-based) DLP
   1. Monitor the outbound traffic for unencrypted sensitive information.
   2. Can automatically encrypt all transitions, common for email.

DLP systems also have two mechanisms of action:

1. _pattern matching_: telltale signs of sensitive information.
   1. for instance unencrypted CCs and SSNs
2. _watermarking_: tags applied to sensitive information.
   1. also commonly used in _digital rights management_ (**DRM**)

see Chapter 5 Security Assessment and Testing

### Data Minimization

- reduce sensitive information on hand.
  - "destroy data when it is no longer necessary to meet our original business purpose."
- _deidentification_ process removes the ability to link data back to an individual.
  - Alternatively, _data obfuscation_: format where the original information can't be retrieved.
    - _Hashing_: apply a hash function (limited encryption)
      - vulnerable to a _rainbow table attack_.
    - _Tokenization_: replace data with an id and lookup table.
    - _Masking_: replace sensitive fields with blank characters (password login screen)
      - "replace all but the last four digits of a credit card number with X's"

### Access Restrictions

Two common types of access restrictions are geographic restrictions and permission restrictions:

1. _Geographic restrictions_ limit access based on physical location. (must be inside the building to palm scan)
2. _Permission restrictions_ (most common, should be default) limit "resources based on the user's role or level of authorization"
   1. Groups and Permissions inside admin panels

see Chapter 8 Identity and Access Management

### Segmentation and Isolation

- "_Segmentation_ places sensitive systems on separate networks where they may communicate with each other but have strict restrictions on their ability to communicate with systems on other networks."
- "_Isolation_ goes a step further and completely cuts a system off from access to or from outside networks."

## Review Question (17/20) 85%

Not good, given I just read the chapter. I'll need to review again before testing, and _take a full practice test_!

### Correct

2, 3, 4, 5, 6, 7, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 20

### Incorrect

1, 8, 19

- 19, I was thinking from the system admin perspective not the user. _Need to not overly focus on keywords_
- 8, Makes sense now that I read the answer LOL.
- 1, No excuses. It was self-explanatory and I just failed to recall correctly. _More review needed._
