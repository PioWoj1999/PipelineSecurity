# Pipeline Security

Repository for gathering information about pipeline security in form of notes.
CI - Continues Integration
CD - Continues Delivery (package build successful and user manually deploys it)
CD - Continues Deployment (automated deployment to PROD)

| Continues Integration    | Continues Delivery | Continues Deployment |
|--------------------------|--------------------|----------------------|
| Build, Integrate, Test → | Test, Deploy       | Releasae (Prod)      |

## CI/CD pipeline security

What do we understand over this term?

* Building visibility over the engineering ecosystem
* Mapping risks and attakc paths
* Securing the engineering ecosystem - all the way from code to deployment

2021 - the year of CI/CD Security<br/>
Engineering environments have become the new attacker's turf. A single insecure step in the CI, or insecure package import - can expose the organization to critical risks.
Lack of security knowledge and which attack to protect against. <br/>
Top 10 CI/CD Security Risks report url: <https://www.cidersecurity.io/wp-content/uploads/2022/06/Top-10-CICD-Security-Risks-.pdf> <br/>

1. **Insufficient Flow Control Mechanisms**<br/>
The ability of an attacker that has obtained permissions to a system within the CI/CD process (SCM, CI, Artifact repository, etc.) to single handedly push malicious code or artifacts down the pipeline, due to a lack in mechanisms that enforce additional approval or review.<br/>
Ex.: PHP Git infrastructure compromise

2. **Inadequate Identity and Access Management**<br/>
Stems from the difficulties in managing
the vast amount of identities spread across the different systems in the engineering
ecosystem, from source control to deployment. The existence of poorly managed identities both human and programmatic accounts - increases the potential and the extent of
damage of their compromise.<br/>
Ex.: Stack Overflow brach

3. **Dependency Chain Abuse**<br/>
Attacker’s ability to abuse flaws relating to how
engineering workstations and build environments fetch code dependencies. Dependency
chain abuse results in a malicious package inadvertently being fetched and executed locally
when pulled.<br/>
Ex.: Dependency Confusion

4. **Poisoned Pipeline Execution (PPE)**<br/>
Ability of an attacker with access to
source control systems - and without access to the build environment, to manipulate the
build process by injecting malicious code/commands into the build pipeline configuration,
essentially ‘poisoning’ the pipeline and running malicious code as part of the build process.<br/>

5. **Insufficient PBAC (Pipeline-Based Access Controls)**<br/>
Pipeline execution nodes have access to numerous resources and systems within and
outside the execution environment. When running malicious code within a pipeline,
adversaries leverage insufficient PBAC risks to abuse the
permission granted to the pipeline for moving laterally within or outside the CI/CD system.<br/>
Ex.: Environment variables exfiltration, Dependency Confusion

6. **Insufficient Credential Hygiene**<br/>
Risks deal with an attacker’s ability to obtain and use various
secrets and tokens spread throughout the pipeline due to flaws having to do with access
controls around the credentials, insecure secret management and overly permissive credentials.<br/>
Ex.: Stack Overflow brach, Environment variables exfiltration

7. **Insecure System Configuration**<br/>
Stems from flaws in the security settings, configuration
and hardening of the different systems across the pipeline (e.g. SCM, CI, Artifact repository),
often resulting in “low hanging fruits” for attackers looking to expand their foothold in the
environment.<br/>
Ex.:PHP Git infrastructure compromise, Stack Overflow brach

8. **Ungoverned usage of 3rd party services**<br/>
Risks
having to do with ungoverned usage of 3rd party services rely on the extreme ease with
which a 3rd party service can be granted access to resources in CI/CD systems, effectively
expanding the attack surface of the organization.<br/>
Ex.: Environment variables exfiltration

9. **Improper Artifact Integrity Validation**<br/>
Allow an attacker with access to one of the
systems in the CI/CD process to push malicious (although seemingly benign) code or
artifacts down the pipeline, due to insufficient mechanisms for ensuring the validation of
code and artifacts.<br/>
Ex.: PHP Git infrastructure compromise, Environment variables exfiltration

10. **Insufficient logging and visibility** <br/>
Allow an adversary to carry out malicious activities
within the CI/CD environment without being detected during any phase of the attack kill
chain, including identifying the attacker’s TTPs (Techniques, Tactics and Procedures) as part
of any post-incident investigation.<br/>
Ex.: PHP Git infrastructure compromise, Environment variables exfiltration, Dependency Confusion

----

### CI/CD Pipeline and CI/CD Security: Defined and Explained

Materials:

* <https://www.strongdm.com/blog/ci-cd-security-and-ci-cd-pipeline>
* <https://www.youtube.com/watch?v=i3Bx1iSzrUY&ab_channel=DevOpsConference>

**Keywords:**

* CI/CD pipeline security
* DevSecOps
* process workflows
* supply chain attack
* secure merge to master branch (Prod)

#### What is a CI/CD pipeline?

A continuous integration, continuous delivery pipeline—or CI/CD pipeline—is a process workflow companies use to streamline and automate software development. A CI/CD pipeline automatically builds and tests code changes to detect bugs before the new code is merged and deployed.

#### What is a CI/CD Security?

CI/CD security is the process and security controls organizations use to secure applications and reduce risk throughout the software development pipeline.<br/>
DevSecOps initiatives like CI/CD pipeline security prevent malicious actors from breaching the security perimeter through development tools or processes.<br/>
The CI/CD pipeline security is designed to catch insecure code before it is integrated into the central code repository or application. CI/CD pipeline security can go a step further and detect irregular code patterns or find loopholes in new code that could expose the application to a breach risk.<br/>

**A secure CI/CD pipeline relies on a combination of continuous monitoring and code analysis to keep DevOps processes and resources safe.**

#### Importnace of CI/CD Security

**CI/CD security** ensures that the faster and more streamlined development process doesn’t come at the cost of application security. Without sufficient security in the CI/CD pipeline, the software supply chain is rife with breach risks. A CI/CD pipeline breach not only poses a threat to company secrets and data, it can also prompt a larger supply chain attack and expose application users to security risks, too.

#### CI/CD Security Risks

Continuous integration security is important to have in place to reduce the risk of supply chain attacks, i.e.: SolarWinds breach.
Most developers use open source code libraries to develop new features more quickly, but this can introduce insecure code if those code snippets aren’t properly managed, i.e.: Log4j vulnerability.

While automated testing in the CI/CD pipeline may expose broken or insecure code before it’s integrated, the pipeline is only designed to test new code additions. Existing code must be monitored and tested regularly to avoid and mitigate these types of breaches.

#### CI/CD Security Best Practices

Maintain efficiency while limiting access and enforcing the principle of least privilege. Using CI/CD security tools to automate security testing, provide better observability, analyze open source code, or scan your application’s code repository.
Regularly audit their third-party providers to stay ahead of supply chain attacks that may infiltrate their CI/CD pipeline.

#### Access CI/CD Automation

Access automation can help secure the CI/CD pipeline by:

* Limiting access for admins and super users
* Eliminating static credentials or secrets
* Streamlining automatic provisioning based on role-based or attribute-based access control
* Providing just-in-time access to developers
* Maintaining comprehensive logs of all access activity
