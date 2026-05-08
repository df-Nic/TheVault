---
Title: Security Testing
Date Created: 22-March-2026
Last Updated: 04-May-2026
Tags:
  - CS4218
  - SWE/Testing/SecurityTesting
---
# The 5W1H Of Security Testing
---
<b><span style='color: #87CEEB'>Security testing</span></b> is the process of <b><span style='color: #FFD700'>identifying vulnerabilities, risks, and weaknesses</span></b> in software, systems, or infrastructure to <b><span style='color: #98FB98'>prevent unauthorized access or data breaches</span></b>.

Robust, continuous **security testing** must be an <b><span style='color: #FFD700'>integral, non-negotiable</span></b> part of our development and operations processes.

>[!warning] If not done properly
><b><span style='color: var(--mk-color-red)'>It can lead to issues</span></b>:
> - Financial
> - Reputational
> - Legal

Security testing are **done by** Security testers, QA engineers, ethical hackers (*penetration testers who mimic real attacks*), or external security consultants. And they are done <b><span style='color: #FFD700'>primarily in a controlled test environment</span></b> (*if you want to do a lot of probing*) and sometimes on <b><span style='color: #FFD700'>production environment</span></b> (*for audits of the live system*)

Typically done <b><span style='color: #FFD700'>throughout the development lifecycle</span></b> as <b><span style='color: #FFD700'>security as to be implement from the beginning</span></b> and throughout the SWE lifecycle.

In software testing we <b><span style='color: #FFD700'>combine automated tools, manual testing, static/dynamic analysis and risk assessment</span></b>. Some tools include:
- DAST

While in testing we check if the function works as intended. **Security testing ensures that**:
- Operations that should not be allowed are not allowed
- Ensures that mitigations are working
## Making Security Test Cases

In security testing we typically **target the following**:
- **Integer overflows**, checks that what our <b><span style='color: #FFD700'>established out-of-range values is detected & rejection works</span></b>
- **Memory management problems**, verifies <b><span style='color: #FFD700'>how code handles large data values</span></b> & rejects them if it's too large
- **Untrusted inputs**, all inputs are untrusted & must be <b><span style='color: #FFD700'>rejected or converted to a valid form</span></b> to safely process it
- Web security
- Exception handling flaws

Security test cases must **fulfil the following**:
- Confirms that a specific <b><span style='color: #FFD700'>security failure does not occur</span></b>
- Checks that <b><span style='color: #FFD700'>protective mechanisms work correctly</span></b>, often involves rejection / neutralisation of invalid inputs and disallowed operations

>[!info] It is created when writing other unit tests & also whenever a security mechanism exist
>These security mechanisms protect valuable resources by blocking improper actions, rejecting malicious inputs, denying access etc.
>

>[!warning] We do not create test cases as a reaction to finding vulnerabilities
>This follows the <b><span style='color: #87CEEB'>shift left approach</span></b>, where we do thing earlier in the SWE development lifecycle
# Basic Security Concepts
---
The <b><span style='color: #87CEEB'>core goals of information security</span></b> are **6 security concepts**:

1) **Confidentiality**

Ensures <b><span style='color: #FFD700'>sensitive data is only accessible to authorized users</span></b>. Prevents unauthorized access, leaks, or exposure of private information.

Protects data in <b><span style='color: #FFD700'>all states, through encryption, access controls, & data masking</span></b>: 
- At rest
- In transit
- In use

So typically **during testing** we will anonymize real data, use secure test environments, restrict access to different types of data.

>[!goal] Ensure personal, financial, and confidential data remains private

>[!fail] Common threats
> Exposed credentials, data in error messages, access control flaws.

2) **Integrity**

Ensures <b><span style='color: #FFD700'>data is accurate, complete, unaltered</span></b>, Prevents unauthorized or accidental modifications to data. This <b><span style='color: #98FB98'>maintains trustworthiness of data</span></b> throughout its lifecycle.

Enforced through: 
- Checksums, hashing
- Digital signatures, 
- Access controls

So typically **during testing**, we will verify that inputs/outputs are consistent and unchanged.

>[!goal] Ensure data remains reliable and authentic from creation to use

>[!fail] Common threats
> Data tampering, man-in-the-middle attacks, unauthorized edits.

3) **Authentication**

<b><span style='color: #FFD700'>Verifies the identity of a user, system, or app</span></b>. Ensures only legitimate users can access resources & this is our <b><span style='color: #FFD700'>first line of defense</span></b> in securing systems and data.

Typically we will use:
- Passwords
- Biometrics
- OTPs
- Security tokens
- OAuth

**During testing** we will check for weak logins, brute-force vulnerabilities, session handling.

>[!danger] Weak authentication leads to impersonation and unauthorized access

>[!goal] Confirm "Who are you?" before granting access

4) **Authorization**

<b><span style='color: #FFD700'>Determines what actions / resources a user is allowed to access</span></b>. This happens after authentication (*after you know the user's identity*), to ensures users can only access what they’re permitted to.

Enforced through:
- Roles
- Permissions
- Access control lists (ACLs)

**During testing**, we will verify access restrictions, test with users of different roles

>[!fail] Common threats
> Privilege escalation, insecure direct object references (*IDOR, modifying credentials to access things*).

>[!goal] Enforce "What are you allowed to do?"

5) **Non-repudiation**

Ensures that a <b><span style='color: #FFD700'>user cannot deny performing an action</span></b>. Provides a proof of origin, delivery, and action. 

Achieved through:
- Digital signatures
- Logs, timestamps
- Audit trails

Prevents users from denying sending messages, making transactions, or modifying data. Essentially it <b><span style='color: #98FB98'>supports accountability and traceability in systems</span></b>.

**During testing**, we will verify logging, signature validation, and audit mechanisms

>[!goal] Ensure actions can be traced and verified beyond dispute

6) **Availability**

Ensures that <b><span style='color: #FFD700'>systems, services, and data are accessible when needed</span></b>. <b><span style='color: #98FB98'>Prevents downtime and ensures reliable access</span></b> for authorized users.

Protected through:
- Redundancy
- Failover systems
- Backups
- DDoS protection

**During testing** we will, check system uptime, response times, and failover mechanisms.

>[!fail] Common threats
> Hardware failures, cyberattacks (e.g., DDoS), software bugs.

>[!goal] Ensure users can access resources without interruption
# Security Techniques
---
To **ensure that the basic security** concepts are covered, we can use these techniques to test for loopholes:
- Security scanning
- Penetration testing
- Threat modeling
- Risk assessment
- Security auditing

>[!success] These techniques can actively test for loopholes or weakness in the system
 We are **not just finding** vulnerability but <b><span style='color: #98FB98'>understanding ,prioritizing and mitigating them</span></b>.
## Security Scanning

It is <b><span style='color: #FFD700'>automated process to identify security vulnerabilities</span></b> in systems, applications, or networks.

Typically we are **trying to detect**:
- SQL injections
- Cross-site scripting (*XSS*)
- Misconfiguration
- Outdated libraries

>[!success] Early vulnerability detection

>[!success] Faster & scalable

>[!success] Reduces manual effort

There are **2 types** of security scanning:
1) **Static application security testing** (*SAST*)

This is a <b><span style='color: #FFD700'>white box approach</span></b> which <b><span style='color: #FFD700'>scans code source code without code execution</span></b> (*find coding flaws like unvalidated inputs*). This is typically done by [[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Automated Software Testing.md#Static Analysis|static analysis tools]] which analyse based on a <b><span style='color: #FFD700'>set of coding rules</span></b>.

>[!success] Scales well as it can run on a lot of software repeatedly

>[!success] Identifies well-known vulnerabilities
>Some of these includes, buffer overflows, SQL injection flaws

>[!success] Provides helpful actionable outputs
> It pinpoints problematic code (*which file, what line number*). This allows <b><span style='color: #98FB98'>developers to quickly and efficiently fix issues</span></b>.

When **choosing a static analyser** consider the following:
1) Choose your programming language
2) Ensure it can detect vulnerabilities (*based on OWASP top 10 or other criteria*) 
3) Evaluate accurate rates (*false positive / negative rates using the OWASP benchmark*)
4) Must understand the libraries and frameworks used
5) Availability as a plugin into preferred developer IDEs
6) Easy to use
7) <b><span style='color: #FFD700'>Ability to include in Continuous Integration / Deployment tools</span></b> (*this is non negotiable*)
8) License cost (*may vary by user, organization, app, lines of code*)

>[!example] An example of a static analysis tool is SonarQube

2) **Dynamic application security testing** (*DAST*)

This is a <b><span style='color: #FFD700'>black box approach</span></b> which <b><span style='color: #FFD700'>scans running applications</span></b> by simulating attacks, identifying runtime vulnerabilities and misconfigurations.
### Source Code Review

Process of <b><span style='color: #FFD700'>manually checking of source code</span></b> of a web application for security issues (*not like SAST where you use a tool*). And there is no substitute for looking directly at the code.

>[!question] Why manually?
>Many <b><span style='color: var(--mk-color-red)'>serious security vulnerabilities cannot be detected</span></b> with any other form of **analysis or testing or tools**.

>[!question] What can we find?
>We can find a long list of issues, Concurrency problems, Flawed business logic, Access control problems, Cryptographic weaknesses Backdoors, Trojans, Other forms of malicious code, Easter eggs, Time bombs, Logic bombs.

>[!example] Password handling using source code review
>In manual source code review you can identify if the ways we handle password it strong or not. for instance: 
>- Checking strength of the password
>- Storing passwords in a unreadable format using a one way hashing algorithm (*SHA-256*)
>- Compare using the hash value or the actual value itself
>  
>  >[!fail] Rainbow table attacks
>  >Rainbow table attacks is basically when a attacker has access to a hash value which he can then use a table of precomputed password to hash mappings to <b><span style='color: var(--mk-color-red)'>reverse engineer the password</span></b>.
>  >
>  >>[!important] Hashing & encryption are 2 different things
>  >><b><span style='color: var(--mk-color-red)'>Encryption is reversible</span></b> while hashing is not.
>  >
>  >Even hashing alone is not enough as 2 same password will have the same hash. So what you can do is to do <b><span style='color: #87CEEB'>salting</span></b>, which is a <b><span style='color: #FFD700'>randomly generate value for each user so that it adds a modifier for the hash function</span></b> (*we need to store the salt value in a hashed format*).
>  
## Penetration Testing

Also known as <b><span style='color: #87CEEB'>Pen test</span></b>. It is a <b><span style='color: #FFD700'>simulated cyberattack by ethical hackers</span></b> on a system to find exploitable vulnerabilities (*before real attackers*).

Depending on the testing style it can be:
- Black box (*no prior knowledge*)
- White box (*full knowledge*)
- Grey box (*partial knowledge*)

Typically in penetration testing has **4 phases**:
1) Planning & reconnaissance
2) Scanning
3) Exploitation
4) Reporting

>[!success] Provides real world attack simulation

>[!success] Uncover complex vulnerabilities within complex logic flows

>[!success] Improve incident response readiness
## Threat Modelling

It is a <b><span style='color: #FFD700'>proactive security measure</span></b>. It can be seen as a <b><span style='color: #FFD700'>risk assessment for applications</span></b> (*data flows, thrust boundary, etc*).

>[!goal] The goal of threat modeling is to help system designers think about security threats that their systems and applications might face
>So <b><span style='color: #FFD700'>mitigation strategies can be designed</span></b> in the <b><span style='color: #98FB98'>early stages</span></b> of development (*or even before coding begins*).

>[!success] Uses less resources
>Because major vulnerabilities are identified early so we can implement security features in the architecture or within the functions early on.

It is **recommended** that all applications have a threat model developed and documented.
## Risk Assessment

It is the <b><span style='color: #FFD700'>process of identifying, analyzing, and evaluating potential security risks</span></b>.

>[!goal] Understand threats and their impact to prioritize mitigation

Here are the **key steps**:
- Identify assets (*risk components like your data your security components etc*)
- Identify threats & vulnerabilities (*cyber, data, insider threats*)
- Assess likelihood & impact
- Determine risk level (*how high level events impact to business*)
- Recommend controls or mitigation

>[!success] Proactive threat management

>[!success] Helps make informed decision making
>Like what to prioritise first and what is not important

>[!success] Better resource allocation

**Identifying** <b><span style='color: #87CEEB'>risk components</span></b> are important as without them you do not know where to manage or mitigate these risks. From these risk components we can <b><span style='color: #FFD700'>understand how to secure and manage them</span></b> within an organization.

>[!tldr] Risk components
>These include the following:
>- Threats
>- Vulnerabilities
>- Assets (*and their relative value, like personal data can be of high value*)
>- Controls associated with the organisation's information resources

**Risk can be computed** using the following formula:
$$
\text{Risk} = \text{No of Assets} \times \text{Unmanaged Asset Groups} + \text{No of Assets} \times \text{Managed Asset Groups}
$$
**Unmanaged asset groups** can be computed as such:
$$
\text{Unmanaged Asset Groups} = \frac{\text{Threats} \times \text{Vulnerabilities} \times \text{Asset Value}}{\text{Weak Controls}}
$$

Then for **managed asset groups** can be computed as such:
$$
\text{Managed Asset Groups} = \frac{\text{Threats} \times \text{Vulnerabilities} \times \text{Asset Value}}{\text{Strong Controls}}
$$
### Identifying Business Assets

>[!abstract] Assets
>They are not just data but <b><span style='color: #FFD700'>things that the business relies upon</span></b>, these includes:
>- Data
>- Important people
>- Technology
>- Processes

It is important to identify business assets as then you can <b><span style='color: #FFD700'>pin point where are the potential entry points to attacks</span></b> (*and what to focus on*).
### Identify the Value of the Assets

Essentially is to <b><span style='color: #FFD700'>categorise your assets</span></b> from very valuable to less valuable. Each organisation will have its own categories and ranges but the idea remains the same which is to <b><span style='color: #FFD700'>prioritise your efforts to protect these assets</span></b>.

You can ask the following question to start determining its value:
-  Make the asset public or not (*what happens if its public*)?
- What if the asset is inaccurate or damaged?
- What if users cannot access this asset?
### Determine & Document Impact of Compromised Assets

<b><span style='color: #FFD700'>Consider the impact to your business if each asset</span></b> were lost, damaged, or reduced in value (*what happens if data is leaked*).

You can also categorise the impact in to different levels with their own ranges / thresholds.

>[!important] This impact may differ from the asset value determined
>High value assets does not mean a greater impact if compromised.
### Identify Likelihood of Compromised Assets

In this step we also concurrently <b><span style='color: #FFD700'>identify possible threats</span></b> to the asset (*or can be done earlier*). And then the <b><span style='color: #FFD700'>likelihood of this threat happening</span></b>.

You can also categorise the impact in to different levels with their own ranges / thresholds.
### Identify Priorities & Potential Solutions

Now with everything all listed out and categorized you can then <b><span style='color: #FFD700'>prioritise which security measure to focus on to protect these assets</span></b>.

What to prioritise depends on what the company wants to focus on. But **typically, assets with high impact and/or likelihood scores should be prioritise first**.

So at this stage you will:
1) Identify priorities
2) Identify potential solutions
3) Develop a plan, including funding to implement the solutions
## Security Auditing

It is a <b><span style='color: #FFD700'>formal review & evaluation</span></b> of an organization's security policies, controls, and practices.

>[!goal] Ensure compliance with security standards and identify weaknesses

These audits can be done:
- **Internally** (*done by the organisation*)
- **Externally** (*conducted by third-party experts*)

Typically these things are being audited:
- Access controls
- System configurations
- User activity logs
- Policy compliance
# Secure Development Life Cycle
---
There are **5 key phases in developing security** in our development lifecycle.
## Phase 1: Before Development

### Define SDLC

In this stage we first need to <b><span style='color: #FFD700'>define an adequate SDLC</span></b>. This means that <b><span style='color: #FFD700'>security is considered and integrated at every stage</span></b> of the development life cycle (*planning to deployment & maintenance*).

Then we need to <b><span style='color: #FFD700'>review the policies and standards set</span></b>. Ensure that there are appropriate policies, standards, and documentation in place.
### Review Policies & Standards

**Documentation** is extremely important as it gives development teams <b><span style='color: #FFD700'>guidelines and policies that they can follow</span></b>. People can only do the right thing if they know what the right thing is.

>[!note] No policies or standards can cover every situation that the development team will face
>By documenting the **common and predictable issues**, there will be <b><span style='color: #98FB98'>fewer decisions that need to be made</span></b> during the development process.
### Develop Measurement & Metrics Criteria

Then lastly with the policies in place, we need to <b><span style='color: #FFD700'>develop measurement and metrics criteria and ensure traceability</span></b>.

>[!question] Why do we need to define measurement & metrics
>This is because we need to <b><span style='color: #FFD700'>know what it means to be compliant</span></b> with this policy. In addition how we measure <b><span style='color: #FFD700'>affects our design choices</span></b> as well (*do this approach to be able to capture this*).
>
>It also <b><span style='color: #98FB98'>enables visibility into defects</span></b> since we can tell if something is wrong through our defined measurements & metrics.
## Phase 2: During Definition & Design

This is where the <b><span style='color: #FFD700'>scope of the project is defined</span></b> and is an important decision to know what security systems to build.
### Review Security Requirements

>[!abstract] Security requirements
>Define how an application works from a security perspective.
>
>>[!example] All passwords must be hashed using this algorithm

By **reviewing the security requirements** we can <b><span style='color: #FFD700'>prevent security flaws from entering the system</span></b>. It is <b><span style='color: #98FB98'>easier to fix a security flaw on a document</span></b> than on code in a system.

>[!important] Ensure that requirements are as unambiguous as possible

Here are some things to review:
- User authentication
- Data confidentiality
- Accountability
- Session management
- etc
### Review Design & Architecture

Here we ensure that the <b><span style='color: #FFD700'>security requirements we have defined are translated into our design</span></b> or architecture.

Typically this design & architecture are all documented (*includes models, text or other artifacts*). We are essentially <b><span style='color: #FFD700'>testing these documents to ensure that the design and architecture enforce the appropriate level of security as defined in the requirements</span></b>.

>[!success] Identifying security flaws in the early stages is the most cost-efficient & one of the most effective places to make changes
### Create & Review UML Models

With our design & architecture complete we can <b><span style='color: #FFD700'>build Unified Modeling Language</span></b> (UML) <b><span style='color: #FFD700'>models</span></b> that describe how the application works.

In a **security standpoint**, these UML just <b><span style='color: #FFD700'>confirm</span></b> with the systems designers an exact <b><span style='color: #FFD700'>understanding of how the application works</span></b>.

>[!note] If there are any weaknesses discovered it should be brought up to the system architect
### Create & Review Threat Model

>[!abstract] Threat model
>It is essentially comming up with a <b><span style='color: #FFD700'>list of realistic threat scenarios, how can it happen and check if our system mitigates it</span></b>.

So with our threat model just check with our architecture to ensure it has been either:
- Mitigated
- Accepted by the business (*sometimes not all threats can be mitigated*)
- Handled by some third party (*insurance*)

>[!warning] If there are threats that have no mitigation strategies, then revisit the design & architecture
>Go through with the systems architect to modify it to cover these threats. <b><span style='color: var(--mk-color-red)'>Do not accept and move on</span></b>.
## Phase 3: During Development

Development is the implementation of a design. In a perfect world we can just translate the blueprint into code. But that is not the case as **many design decisions are made during code development**.

>[!info] These decisions are typically very detailed something that will not be captured in a high level diagram
>But still **important** as usually these decisions have <b><span style='color: var(--mk-color-red)'>no policy or standard guidance</span></b>.

If our **design and architecture is not done properly**, then the <b><span style='color: var(--mk-color-red)'>developers will have a lot of decisions to make</span></b>.

>[!goal] Provide tools, knowledge and guardrails to help developers make the right security decisions
>Even though they face a lot of decisions due to bad planning.
### Code Walkthrough

The security team should perform a code walkthrough with the developers, and in some cases, the system architects

A code walkthrough is a <b><span style='color: #FFD700'>high-level look</span></b> at the code during which the developers can <b><span style='color: #FFD700'>explain the logic & flow of the implemented code</span></b>. This allows the developers to justify their choices.

>[!success] The review teams gets a general understanding of the code

>[!important] We are not to perform a code review, but to understand the application at a high level
### Code Reviews

Armed with a good understanding of how the code is structured and why certain things were coded the way they were, the <b><span style='color: #FFD700'>tester can now examine the actual code for security defects</span></b> (*can be targeted to find specific defects*).

Typically a **static code review** is done <b><span style='color: #FFD700'>validate the code against a set of checklists</span></b>, including:
- Business requirements for availability, confidentiality, and integrity
- OWASP Guide or Top 10 Checklists for technical exposures (*depending on the depth of the review*)
- Specific issues relating to the language or framework in use, such as the Scarlet paper for PHP or Microsoft Secure Coding checklists for ASP.NET
- Any industry-specific requirements (*regulatory compliance*), such as Sarbanes-Oxley 404, COPPA, ISO/IEC 27002, APRA, HIPAA, Visa Merchant guidelines, or other regulatory regimes
## Phase 4: During Deployment

Here we are not analysing individual components but <b><span style='color: #FFD700'>testing the security of the complete integrated system in its operational environment</span></b>.
### Application Penetration Testing

Penetration testing the application after it has been deployed provides an <b><span style='color: #FFD700'>additional check to ensure that nothing has been missed</span></b>.

>[!question] Why do we need it?
>Even if everything is done correctly during development some security issues might not been caught.
### Configuration Management Testing

The application penetration test should include an <b><span style='color: #FFD700'>examination of how the infrastructure was deployed and secured</span></b> (*database, servers, network security measures, configurations*).

It is important to review configuration aspects to ensure that <b><span style='color: var(--mk-color-red)'>none are left at a default setting that may be vulnerable to exploitation</span></b>.
## Phase 5: During Maintenance & Operations

The most important phase because now our **security measures are now being tested and used for a long period of time**.

>[!goal] For this phase we focus to keep the system secure at all times
>Ensuring continuous governance, pro-active validation and secure change management.
### Conduct Operational Management Reviews

There needs to be a formal well documented process in place which <b><span style='color: #FFD700'>details how the operational side of both the application and infrastructure is managed</span></b>.

This includes:
- Procedures for patching
- Indecent response
- User access reviews
- System monitoring
### Conduct Periodic Health Checks

>[!note] Security is not a static state, it degrades or is maintained overtime

Monthly or quarterly <b><span style='color: #FFD700'>health checks should be performed on both the application and infrastructure</span></b>.

>[!goal] Ensure no new security risks have been introduced & that the level of security is still intact.

These includes:
- Vulnerability scanning
- Configuration audits
### Ensure Change Verification

This is to <b><span style='color: #FFD700'>handle evolutions in our application</span></b>. 

After **every change** has been approved and tested in the QA environment and deployed into the production environment, it is vital that the change is <b><span style='color: #FFD700'>checked to ensure that the level of security has not been affected by the change</span></b>.

A minor change can have a big impact on security.

This process should be integrated into the <b><span style='color: #87CEEB'>change management process</span></b>.

>[!abstract] Change management process
>It is just a set of regulatory frameworks.

# Web Application Security Testing
---
Many of the web applications are the entry point to the business, it is essential to ensure security to:
- Gain **trust**
- **Compliance**
- Also ensure **data security**

Here we are focus on <b><span style='color: #FFD700'>evaluating the security of a web application</span></b>, more specifically vulnerabilities within:
- The **code**
- **Business logic**
- **Session management**

There are **2 fundamental approaches**:
1) **Passive** testing
2) **Active** testing
## Passive Testing

The testers goal is to <b><span style='color: #FFD700'>understand the application’s logic and explore it the same way as an end user</span></b> (*observe rather than interact and forcefully attack*).

At the **end** the tester should <b><span style='color: #FFD700'>understand all access points</span></b> (*HTTP headers, cookies, APIs, application pages, etc*) & <b><span style='color: #FFD700'>functionality of the system</span></b>.

>[!goal] To summarise everything, the tester wants to find, various end points, HTTP headers and every parameter which a user can use to enter into our system

Typically **tools are used to assist** with information gathering, they help <b><span style='color: #FFD700'>capture what the application is doing and provide valuable insights</span></b>.

>[!example] A HTTP(S) proxy can be used to observe all HTTP requests & responses
## Active Testing

Active testing **relies on** the various entry points a tester found in [[Year 3/Sem 2/CS4218 - Software Testing/Security Testing.md#Passive Testing|passive testing ]]. Here we will <b><span style='color: #FFD700'>probe every access point in the application</span></b>.

Here is a **list of different categories of testing** one can do in active testing:
![[Testing Methods for Active Testing.png|center]]
### Authentication Testing

This is the front man of your application and we need to make sure it is secure. Here are some tests that can be done:
- Testing for Credentials Transported over an Encrypted Channel

**Use a network proxy** and watch the login request, if you can <b><span style='color: var(--mk-color-red)'>see the user name & password in plain text then there is a major security issue</span></b>. Try and send it through HTTPS or TLS/SSL, <b><span style='color: #FFD700'>this is non-negotiable</span></b>.

>[!danger] Anyone on the network you can just take a person's username or password

>[!warning] having an SSL/TSL certificate does not guarantee it is secure
>The is a <b><span style='color: var(--mk-color-red)'>man in the middle attack called SSLStrip</span></b>. Here the hacker will host a copy of the application in HTTP then takes your information and pass it to the real server for verification.

- Testing for Default Credentials, here we are <b><span style='color: #FFD700'>testing for a list of default or common user names or passwords</span></b>
- Testing for Weak Lock Out Mechanism
- Testing for Bypassing Authentication Schema
- Testing for Vulnerable Remember Password
- Testing for Browser Cache Weaknesses
- Testing for Weak Password Policy
- Testing for Weak Security Question Answer
- Testing for Weak Password Change or Reset Functionalities
- Testing for Weaker Authentication in Alternative Channel
## Input Validation Testing

This is one of the **most important domains in security**, because <b><span style='color: var(--mk-color-red)'>1 flaw can lead to a whole system compromise</span></b>.

>[!quote]  All inputs are malicious until proven otherwise

Here are **some attacks which can happen** if not done properly:
1) **Reflected** cross site scripting, where the <b><span style='color: #FFD700'>website hold a malicious script</span></b> which when clicked will <b><span style='color: var(--mk-color-red)'>execute on the user's browser</span></b>
2) **Stored** cross site scripting, where we <b><span style='color: #FFD700'>inject a script</span></b> which is stored in the application's database, <b><span style='color: var(--mk-color-red)'>anyone who use the application will get attacked</span></b>
3) **HTTP verb tampering**, here we see if we can <b><span style='color: #FFD700'>switch a HTTP request</span></b> from a GET to a POST for example. Essentially <b><span style='color: var(--mk-color-red)'>bypass security filters or access functions</span></b>
4) **HTTP parameter pollution**, where we try and <b><span style='color: #FFD700'>send various inputs</span></b> which when parsed by the backend can <b><span style='color: var(--mk-color-red)'>bypass security or overwrite values</span></b>
5) **SQL injection**, here we try to <b><span style='color: #FFD700'>inject SQL queries</span></b> to do malicious things on our database

>[!tldr] SQL Injection
>Also known as <b><span style='color: #87CEEB'>SQLI</span></b>. To detect potential areas for SQLI we need to <b><span style='color: #FFD700'>know where application interacts with a DB</span></b> server in order to access some data (*login, register, search engines, etc*).
### Testing for Reflected Cross-Site Scripting

**First** for each web page, the tester must <b><span style='color: #FFD700'>determine all the web application’s user-defined variables and how to input them</span></b>, these include:
- HTTP parameters
- POST data
- Hidden form field values
- Predefined radio or selection values

Then we need to <b><span style='color: #FFD700'>analyse these input variables</span></b> to find vulnerabilities. We can <b><span style='color: #FFD700'>inject a simple script and see how the server responds</span></b>.

>[!question] What simple script can we do?
>You can change the URL input to `<script>alert(123)</script>`. And see if an alert happens.

>[!warning] If the script executes then you have identified a vulnerability

