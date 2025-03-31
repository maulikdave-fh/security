## Objective
Notes on my understanding of application security concepts & practices.

## Impact of Security Vulnerability
Security vulnerability impacts availability, integrity and confidentiality of data.

## Security Controls
### Preventive 
1. PCI-DSS Requirements - Secure data in transit and data at rest by secure networks, systems and apps. PCI-DSS has 6 Goals -> 12 Requirements 0> 400+ controls.
2. Shift Security Left - Secure by design, secure coding practices - OWASP (Open Web Application Security Project), CI pipeline with static / dynamic code analysis, code reviews, penetration testing.  
   
### Detective 
1. Intrusion Detection & Alerts
   
### Corrective
1. Incident Response
2. Data Recovery
3. Post-incident Analysis

## Design & Development Practices
### Secure Coding
#### Input validation
Never trust user provided data or data coming from other apps / services. 
1. Input data validations on type, length, limits.
2. Rate Limiting / Throttling
3. Schema based validations
4. White-listing

#### Miscellaneous
1. SQL Injection (%;UPDATE PRODUCT set price=0--) - Use PreparedStatement with parameterized query. JPA's Hibernate implementation is safe.
2. Password - Hashing + Password specific salt	+ work factor (delay factor) using BCrypt , Scrypt, PBKDF2, Argon2. Avoid MD5, SHA
3. Encryption - Use AES with 128/256 bits key, secure mode for Symmetric Key Cryptography
4. File Upload - file name sanitization for path traversal - ensure that it is uploaded to intended directory, check file extension, check file content for allowed type, Minimal access rights on upload directory
5. Use Random Pseudo number generator for session ids, unique ids - sequential ids are more predictable and prone to enumerating attack
6. OWASP's Java encoder
7. SSRF (Server Side Request Forgery) - protech servers from unauthorized internal requests that can lead to data leaks or manipulation.
8. XML Parsing - For XMLs coming from third party services. In XMLReader, use correct feature settings - disable doc types, disable external entities
9. YAML - Use SnameYaml2.x with Spring.

#### Usage of Third-party Libs / Frameworks
1. Review for vulnerablities
2. Use right security alogrithms with correct configurations

### Secure By Design
1. Principle of Least Privillege - allow access for minimal period needed
2. Defence in Depth - Multiple inter-related security measures to secure the system - no single point of failure. For example, ID&V, MFA, Firewalls, Malware detection, ACL, Access Scanning, Cryptography for securing data, Backup & recovery, etc.
3. Fail safe - Murphy's law. If something fails, it should fail in a secured position. For example; if firewall fails, instead of allowing traffic, it should deny all traffic - valid & invalid both.
4. KISS - More complex the system, more difficult to secure
5. SRP - Without SRP, one vulnerable service can make the entire system vulenrable.
6. Segmentation - Provides isolation. Helps reduce the blast radius. E.g.; In cloud, zones can have exclusive power, cooling and network services.
7. Minimize Attack Surface - Limit external interfaces, Limit Remote Access, Limit IPs, Limit No. of Components
8. Secure By Default - Reduce attack surface, Change default passwords, Change default admin ids

### API Security
1. Minimize exposed APIs / services - helps reduce security exposure
2. Use https - prevents eavesdropping, man-in-middle attacks. Provides authentication, encryption and integrity.
3. OAuth2 Authorization
4. Leveled API keys + Key rotation - Read only, write key, admin key, etc. Helps reduce security vulnerability blast radius
5. Authorization - Role based access control
6. Rate limiting / Throttling - Protects against DOS attack. Provides security & helps improve performance & availability.
7. Allowed List (White-listing) - Can be on allowed IPs, User roles, User Ids, API keys. Everything else is Denied by Default
8. Check OWASP API security risks
9. Use API Gateway - Helps centralized implementation of security aspects - rate limiting, authentication, monitoring, logging
10. Error Handling - Descriptive error messages without any sensitive information. No stack-traces. Use appropriate HTTP status codes
11. Input validation - Validate request parameters, headers and payloads to prevent SQL injection, Cross-site Scripting attacks

## Tools & Frameworks
1. Snyk: Dependency vulnerability scanning
2. SonarQube: Static code analysis
3. Fortify: Static code analysis
4. Veracode: Comprehensive application security testing
5. Aqua Security: Container image scanning
6. Checkmarx: IaC (Infrastructure as Code) security scanning
7. Burp Suite: API security testing 
8. Maven Dependency Check plugin - https://mvnrepository.com/artifact/org.owasp/dependency-check-maven/7.1.0
9. ZAP (Zed Attack Proxy) - Open source tool to identify vulnerabilities during testing phase
10. Spring Security

## JWT (JSON Web Token)
1. Secure way of transmitting information between 2 parties in stateless manner - unlike session token where subsequent requests to server with a session token has to land on the same server that issued the session token. JWTs are ideal for distributed systems.
2. User is authenticated once, issued a JWT that contains information like user role. The JWT can be sent to APIs & APIs can authorize the user for granting access. Helps reduce a load on authentication server.
3. PKI is used - private key to sign the JWT and public key to verify the JWT
4. JWT has a. Return address - tells who sent the token, b. Payload - contains claims (Registered claims & Custom claims) c. JWT Wax seal - Signature of JWT to make the JWT temper-proof
5. Registered claims - has JWT issuer details, JWS subject details (id), Audience for the JWT (API endpoint), Expiry, Issue time
6. Custom claims - you can have entities like role or any other custom data that may help authenticate and authorize user
7. JWT is signed and encoded. No sensitive information should be part of JWT.

## OAuth2.0 
1. There are two types of bearer tokens: Identifier-based and Self-contained. Self-contained bearer tokens are easy to scale with distributed applications as they do not require the resource server to validate the token with the authorization server. On the other hand, an Identifier-based token is a hard-to-guess string, which the resource server needs to validate by making a call to the authorisation server's introspection endpoint, which adds latency and makes it difficult to scale with distributed applications.
