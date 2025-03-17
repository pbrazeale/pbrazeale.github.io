"Social engineering techniques focus on the human side of information security."

## Social Engineering and Human Vectors
- Social Engineering Key Principles:
	- **Authority**, people tend to obey those who appear in charge.
		- *Wear a business casual dress and walk around the backroom of a retail store.*
	- **Intimidation**
	- **Consensus-based**, *social-proof* using a groups actions to influence a target into compliance.
	- **Scarcity**
	- **Familiarity-based**
	- **Trust**
		- The [xz-utils backdoor](https://www.kali.org/blog/about-the-xz-backdoor/)
			- "The xz-utils package, starting from versions 5.6.0 to 5.6.1, was found to contain a backdoor (CVE-2024-3094). This backdoor could potentially allow a malicious actor to compromise sshd authentication, granting unauthorized access to the entire system remotely."
	- **Urgency**

"Many, if not most, social engineering efforts in the real world combine multiple principles into a single attack. If a penetration tester calls, claiming to be a senior leader's assistant in another part of your company (thus leading *authority* and possibly *familiarity* responses), and then insists that that senior leader has an urgent need (*urgency*) and informs their target that they could lose their job if they don't do something immediately (*intimidation*), they are more likely to be successful in many cases than if they only used one principle. A key part of social engineering is understanding the target, how humans react, and how stress reactions can be leveraged to meet a goal."

### Social Engineering Techniques
#### Phishing
- The process of gaining personal information
	- *smishing* phishing SMS
		- *MultiFactor Authentication* (**MFA**) attacks
	- *vishing* phishing via phone
	- *Spear phishing* targeted attacks
		- *Whaling* spear phishing CEOs/VIPs
	- 

#### Impersonation
- key tool in social engineer's toolkit
- identity fraud

#### Business Email Compromises
- **BEC**
- spoofing email domains (amazon, google, etc...)

#### Watering Hole Attacks
- "Watering hole attacks use websites that targets frequent to attack them."

#### Brand Impersonation
- Websites or emails made to look legitimate
	- Often used to get fake logins to gain username and passwords

#### Typosquatting
- using URLs that only one character off to appear legit
- *pharming* attacks DNS entries to redirect to a lookalike site


## Password Attacks
- *Brute-force attacks* iterate through password lists
	- *Password spraying attacks* use a refined list against multiple accounts
	- *Dictionary attacks* use known passwords often via breaches
		- John the Ripper common password cracking tool

##### Exam Note
spraying and brute force are the focus of the exam.

- *rainbow tables* are the known hashes to compare against a hashed database
	- Use of salt and pepper can mitigate the effectiveness of rainbow tables. 


## Review Questions (19/20) 95%
Waited two day on this test likewise, but obviously did far better. If there is time during the real exam, I'd for sure review my answers if I felt unsure. 

### Correct
2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20

### Incorrect
1

- 1, I over fixated on the typo rather than the method of messaging. The funny part is when I marked typosquatting later in the test, I figured something was wrong. *I'm unsure if I'll have time to review questions during the test, so I'm moving forward with zero review.*
