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
### Input validation
Never trust user provided data or data coming from other apps / services. 
1. Input data validations on type, length, limits.
2. Rate Limiting / Throttling
3. Schema based validations
4. White-listing

### Access Control List
Practice least privillege access control, denied by default and ZERO trust.

### Usage of Third-party Libs / Frameworks
1. Review for vulnerablities
2. Use right security alogrithms, libs.

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

### Secure Coding
1. Input validations
2. 

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
