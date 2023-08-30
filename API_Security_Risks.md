# OWASP Top 10 API Security Risks – 2023
Reference material: https://owasp.org/API-Security/editions/2023/en/0x11-t10/

## API1:2023 Broken Object Level Authorization
Object level authorization is an access control mechanism that is usually implemented at the code level to validate that a user can only access the objects that they should have permissions to access.

Every API endpoint that receives an ID of an object, and performs any action on the object, should implement object-level authorization checks. The checks should validate that the logged-in user has permissions to perform the requested action on the requested object.

Attackers can exploit API endpoints that are vulnerable to broken object-level authorization by manipulating the ID of an object that is sent within the request. Object IDs can be anything from sequential integers, UUIDs, or generic strings. Regardless of the data type, they are easy to identify in the request target (path or query string parameters), request headers, or even as part of the request payload.

**How To Prevent**

* Implement a proper authorization mechanism that relies on the user policies and hierarchy.
* Use the authorization mechanism to check if the logged-in user has access to perform the requested action on the record in every function that uses an input from the client to access a record in the database.
* Prefer the use of random and unpredictable values as GUIDs for records' IDs.
* Write tests to evaluate the vulnerability of the authorization mechanism. Do not deploy changes that make the tests fail.

---
## API2:2023 Broken Authentication
Authentication endpoints and flows are assets that need to be protected. Additionally, "Forgot password / reset password" should be treated the same way as authentication mechanisms.

An API is vulnerable if it:

* Permits credential stuffing where the attacker uses brute force with a list of valid usernames and passwords.
* Permits attackers to perform a brute force attack on the same user account, without presenting captcha/account lockout mechanism.
* Permits weak passwords.
* Sends sensitive authentication details, such as auth tokens and passwords in the URL.
* Allows users to change their email address, current password, or do any other sensitive operations without asking for password confirmation.
* Doesn't validate the authenticity of tokens.
* Accepts unsigned/weakly signed JWT tokens ({"alg":"none"})
* Doesn't validate the JWT expiration date.
* Uses plain text, non-encrypted, or weakly hashed passwords.
* Uses weak encryption keys.

**How To Prevent**

* Make sure you know all the possible flows to authenticate to the API (mobile/ web/deep links that implement one-click authentication/etc.). Ask your engineers what flows you missed.
* Read about your authentication mechanisms. Make sure you understand what and how they are used. OAuth is not authentication, and neither are API keys.
* Don't reinvent the wheel in authentication, token generation, or password storage. Use the standards.
* Credential recovery/forgot password endpoints should be treated as login endpoints in terms of brute force, rate limiting, and lockout protections.
* Require re-authentication for sensitive operations (e.g. changing the account owner email address/2FA phone number).
* Use the OWASP Authentication Cheatsheet.
* Where possible, implement multi-factor authentication.
* Implement anti-brute force mechanisms to mitigate credential stuffing, dictionary attacks, and brute force attacks on your authentication endpoints. This mechanism should be stricter than the regular rate limiting mechanisms on your APIs.
* Implement account lockout/captcha mechanisms to prevent brute force attacks against specific users. * Implement weak-password checks.
* API keys should not be used for user authentication. They should only be used for API clients authentication.

---
## API3:2023 Broken Object Property Level Authorization
When allowing a user to access an object using an API endpoint, it is important to validate that the user has access to the specific object properties they are trying to access.

An API endpoint is vulnerable if:

* The API endpoint exposes properties of an object that are considered sensitive and should not be read by the user. (previously named: "Excessive Data Exposure")
* The API endpoint allows a user to change, add/or delete the value of a sensitive object's property which the user should not be able to access (previously named: "Mass Assignment")

APIs tend to expose endpoints that return all object’s properties. This is particularly valid for REST APIs. For other protocols such as GraphQL, it may require crafted requests to specify which properties should be returned. Identifying these additional properties that can be manipulated requires more effort, but there are a few automated tools available to assist in this task.

**How To Prevent**

* When exposing an object using an API endpoint, always make sure that the user should have access to the object's properties you expose.
* Avoid using generic methods such as to_json() and to_string(). Instead, cherry-pick specific object properties you specifically want to return.
* If possible, avoid using functions that automatically bind a client's input into code variables, internal objects, or object properties ("Mass Assignment").
* Allow changes only to the object's properties that should be updated by the client.
* Implement a schema-based response validation mechanism as an extra layer of security. As part of this mechanism, define and enforce data returned by all API methods.
* Keep returned data structures to the bare minimum, according to the business/functional requirements for the endpoint.

---
## API4:2023 Unrestricted Resource Consumption
Satisfying API requests requires resources such as network bandwidth, CPU, memory, and storage. Sometimes required resources are made available by service providers via API integrations, and paid for per request, such as sending emails/SMS/phone calls, biometrics validation, etc.

Exploitation requires simple API requests. Multiple concurrent requests can be performed from a single local computer or by using cloud computing resources. Most of the automated tools available are designed to cause DoS via high loads of traffic, impacting APIs’ service rate.

**How To Prevent**
* Use a solution that makes it easy to limit memory, CPU, number of restarts, file descriptors, and processes such as Containers / Serverless code (e.g. Lambdas).
* Define and enforce a maximum size of data on all incoming parameters and payloads, such as maximum length for strings, maximum number of elements in arrays, and maximum upload file size (regardless of whether it is stored locally or in cloud storage).
* Implement a limit on how often a client can interact with the API within a defined timeframe (rate limiting).
* Rate limiting should be fine tuned based on the business needs. Some API Endpoints might require stricter policies.
* Limit/throttle how many times or how often a single API client/user can execute a single operation (e.g. validate an OTP, or request password recovery without visiting the one-time URL).
* Add proper server-side validation for query string and request body parameters, specifically the one that controls the number of records to be returned in the response.
* Configure spending limits for all service providers/API integrations. When setting spending limits is not possible, billing alerts should be configured instead.

---
## API5:2023 Broken Function Level Authorization
Exploitation requires the attacker to send legitimate API calls to an API endpoint that they should not have access to as anonymous users or regular, non-privileged users. Exposed endpoints will be easily exploited.

Authorization checks for a function or resource are usually managed via configuration or code level.

**How To Prevent**
* Your application should have a consistent and easy-to-analyze authorization module that is invoked from all your business functions. Frequently, such protection is provided by one or more components external to the application code.
* The enforcement mechanism(s) should deny all access by default, requiring explicit grants to specific roles for access to every function.
* Review your API endpoints against function level authorization flaws, while keeping in mind the business logic of the application and groups hierarchy.
* Make sure that all of your administrative controllers inherit from an administrative abstract controller that implements authorization checks based on the user's group/role.
* Make sure that administrative functions inside a regular controller implement authorization checks based on the user's group and role.

---
## API6:2023 Unrestricted Access to Sensitive Business Flows
When creating an API Endpoint, it is important to understand which business flow it exposes. Some business flows are more sensitive than others, in the sense that excessive access to them may harm the business.<br/>
An API Endpoint is vulnerable if it exposes a sensitive business flow, without appropriately restricting the access to it.

Exploitation usually involves understanding the business model backed by the API, finding sensitive business flows, and automating access to these flows, causing harm to the business.

Lack of a holistic view of the API in order to fully support business requirements tends to contribute to the prevalence of this issue.

**How To Prevent**
Secure and limit access to APIs that are consumed directly by machines (such as developer and B2B APIs). They tend to be an easy target for attackers because they often don't implement all the required protection mechanisms.<br/>
Some of the protection mechanisms are more simple while others are more difficult to implement. The following methods are used to slow down automated threats:
* Device fingerprinting: denying service to unexpected client devices (e.g headless browsers) tends to make threat actors use more sophisticated solutions, thus more costly for them
* Human detection: using either captcha or more advanced biometric solutions (e.g. typing patterns)
* Non-human patterns: analyze the user flow to detect non-human patterns (e.g. the user accessed the "add to cart" and "complete purchase" functions in less than one second)
* Consider blocking IP addresses of Tor exit nodes and well-known proxies

---
## API7:2023 Server Side Request Forgery
Server-Side Request Forgery (SSRF) flaws occur when an API is fetching a remote resource without validating the user-supplied URL. It enables an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall or a VPN.

**How To Prevent**
* Isolate the resource fetching mechanism in your network: usually these features are aimed to retrieve remote resources and not internal ones.
* Whenever possible, use allow lists of:
  * Remote origins users are expected to download resources from (e.g. Google Drive, Gravatar, etc.)
  * URL schemes and ports
  * Accepted media types for a given functionality
  * Disable HTTP redirections.
  * Use a well-tested and maintained URL parser to avoid issues caused by URL parsing inconsistencies.
  * Validate and sanitize all client-supplied input data.
  * Do not send raw responses to clients.

---
## API8:2023 Security Misconfiguration
Security misconfiguration can happen at any level of the API stack, from the network level to the application level. Automated tools are available to detect and exploit misconfigurations such as unnecessary services or legacy options.

**How To Prevent**
The API life cycle should include:
* A repeatable hardening process leading to fast and easy deployment of a properly locked down environment
* A task to review and update configurations across the entire API stack. The review should include: orchestration files, API components, and cloud services (e.g. S3 bucket permissions)
* An automated process to continuously assess the effectiveness of the configuration and settings in all environments

---
## API9:2023 Improper Inventory Management
How the APIs are storing or sharing data with external third parties. The visibility and inventory of sensitive data flows play an important role as part of an incident response plan, in case a breach happens on the third party side.

**How To Prevent**
* Inventory all API hosts and document important aspects of each one of them, focusing on the API environment (e.g. production, staging, test, development), who should have network access to the host (e.g. public, internal, partners) and the API version.
* Inventory integrated services and document important aspects such as their role in the system, what data is exchanged (data flow), and their sensitivity.
* Document all aspects of your API such as authentication, errors, redirects, rate limiting, cross-origin resource sharing (CORS) policy, and endpoints, including their parameters, requests, and responses.
* Generate documentation automatically by adopting open standards. Include the documentation build in your CI/CD pipeline.
* Make API documentation available only to those authorized to use the API.
* Use external protection measures such as API security specific solutions for all exposed versions of your APIs, not just for the current production version.
* Avoid using production data with non-production API deployments. If this is unavoidable, these endpoints should get the same security treatment as the production ones.
* When newer versions of APIs include security improvements, perform a risk analysis to inform the mitigation actions required for the older versions. For example, whether it is possible to backport the improvements without breaking API compatibility or if you need to take the older version out quickly and force all clients to move to the latest version.

---
## API10:2023 Unsafe Consumption of APIs
Developers tend to trust data received from third-party APIs more than user input. This is especially true for APIs offered by well-known companies. Because of that, developers tend to adopt weaker security standards, for instance, in regards to input validation and sanitization.
The API might be vulnerable if:

* Interacts with other APIs over an unencrypted channel;
* Does not properly validate and sanitize data gathered from other APIs prior to processing it or passing it to downstream components;
* Blindly follows redirections;
* Does not limit the number of resources available to process third-party services responses;
* Does not implement timeouts for interactions with third-party services

**How To Prevent**
* When evaluating service providers, assess their API security posture.
* Ensure all API interactions happen over a secure communication channel (TLS).
* Always validate and properly sanitize data received from integrated APIs before using it.
* Maintain an allowlist of well-known locations integrated APIs may redirect yours to: do not blindly follow redirects.