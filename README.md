# Pipeline Security

Repository for gathering information about pipeline security in form of notes.

## CI/CD pipeline security

### CI/CD Pipeline and CI/CD Security: Defined and Explained

Material:

* <https://www.strongdm.com/blog/ci-cd-security-and-ci-cd-pipeline>

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

#### Top 10 CI/CD Security Risks - OWASP

1. **Not Enough Security Controls to Manage Process Flow:** a lack of approval or review processes enables attackers to introduce malicious code
2. **Weak Identity and Access Management:** poorly managed accounts and access controls give attackers more ways to break into systems
3. **Fetching and Executing Dangerous Dependencies:** misconfigurations cause systems to pull and execute malicious code packages, allowing attackers to steal credentials
4. **Poisoned Pipeline Execution (PPE):** attackers inject commands into the build process
5. **Missing Access Controls within the Pipeline:** poorly scoped access gives attackers free rein within pipeline systems
6. **Poor Credentialing Practices:** maintaining static credentials, unnecessary access, or unchanged admin credentials gives attackers ongoing access
7. **System Misconfigurations:** overlooked security settings leaves CI/CD systems exposed to breaches
8. **Excessive Access Granted to Third Parties:** connecting external resources to the CI/CD pipeline without managing access expands the DevOps attack surface
9. **Poor Artifact Validation:** without validation controls, attackers can push infected artifacts or code through the pipeline
10. **Lack of Observability:** inability to detect threats due to poor logging or visibility

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
