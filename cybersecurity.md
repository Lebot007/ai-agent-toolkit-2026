# Cyberseguranca

Guia completo de seguranca: pentesting, OWASP, SAST/DAST, secret scanning, threat modeling, ferramentas ofensivas e defensivas.

## OWASP Top 10 (2021)

### A01: Broken Access Control
- Falhas em restringir acesso a recursos
- IDOR (Insecure Direct Object References)
- Privilege escalation
- Mitigacao: principle of least privilege, deny by default

### A02: Cryptographic Failures
- Dados sensiveis sem encryptacao
- Algoritmos fracos (MD5, SHA1)
- Mitigacao: AES-256, TLS 1.3, bcrypt/Argon2 para passwords

### A03: Injection
- SQL injection, NoSQL injection, command injection
- XSS (Cross-Site Scripting)
- Mitigacao: parameterized queries, input validation, output encoding

### A04: Insecure Design
- Falhas arquiteturais
- Mitigacao: threat modeling, secure design patterns

### A05: Security Misconfiguration
- Default credentials
- Unnecessary services
- Mitigacao: hardening, security baselines

### A06: Vulnerable Components
- Dependencias com CVEs conhecidos
- Mitigacao: dependency scanning, patch management

### A07: Authentication Failures
- Weak passwords
- Session management issues
- Mitigacao: MFA, password policies, secure session handling

### A08: Software and Data Integrity Failures
- Insecure updates
- Mitigacao: code signing, integrity checks

### A09: Security Logging and Monitoring Failures
- Insufficient logging
- Mitigacao: centralized logging, alerting

### A10: Server-Side Request Forgery (SSRF)
- Server faz requests para recursos internos
- Mitigacao: allowlists, network segmentation

## Pentesting Tools

### Reconnaissance
- **Nmap:** nmap.org (network scanning)
- **Shodan:** shodan.io (IoT search engine)
- **theHarvester:** github.com/laramies/theHarvester
- **Recon-ng:** github.com/lanmaster53/recon-ng

### Web Application
- **Burp Suite:** portswigger.net/burp (proxy, scanner)
- **OWASP ZAP:** owasp.org/www-project-zap
- **Nikto:** github.com/sullo/nikto (web scanner)
- **SQLMap:** sqlmap.org (SQL injection)
- **Wfuzz:** github.com/xmendez/wfuzz (fuzzer)

### Exploitation
- **Metasploit:** metasploit.com (exploitation framework)
- **Cobalt Strike:** cobaltstrike.com (red team)
- **Impacket:** github.com/SecureAuthCorp/impacket (Windows attacks)

### Password Cracking
- **Hashcat:** hashcat.net (GPU-based)
- **John the Ripper:** openwall.com/john
- **Hydra:** github.com/vanhauser-thc/thc-hydra (online)

### Wireless
- **Aircrack-ng:** aircrack-ng.org
- **Kismet:** kismetwireless.net

## SAST (Static Application Security Testing)

- **SonarQube:** sonarqube.org (code quality + security)
- **Semgrep:** semgrep.dev (fast, customizable)
- **CodeQL:** github.com/github/codeql (semantic analysis)
- **Bandit:** github.com/PyCQA/bandit (Python)
- **Brakeman:** brakemanscanner.org (Ruby on Rails)
- **ESLint Security:** eslint.org (JavaScript)

## DAST (Dynamic Application Security Testing)

- **OWASP ZAP:** owasp.org/www-project-zap
- **Burp Suite Professional:** portswigger.net
- **Nuclei:** github.com/projectdiscovery/nuclei (template-based)
- **Arachni:** arachni-scanner.com

## SCA (Software Composition Analysis)

- **Snyk:** snyk.io (dependencies, containers, IaC)
- **Dependabot:** github.com (GitHub native)
- **Trivy:** github.com/aquasecurity/trivy (containers, filesystems)
- **npm audit:** built-in (Node.js)
- **Safety:** github.com/pyupio/safety (Python)

## Secret Scanning

- **GitGuardian:** gitguardian.com
- **TruffleHog:** github.com/trufflesecurity/trufflehog
- **Gitleaks:** github.com/gitleaks/gitleaks
- **GitHub Secret Scanning:** built-in

## Threat Modeling

### Metodologias
- **STRIDE:** Spoofing, Tampering, Repudiation, Information Disclosure, DoS, Elevation of Privilege
- **DREAD:** Damage, Reproducibility, Exploitability, Affected users, Discoverability
- **PASTA:** Process for Attack Simulation and Threat Analysis
- **MITRE ATT&CK:** attack.mitre.org (adversary tactics)

### Ferramentas
- **OWASP Threat Dragon:** owasp.org/www-project-threat-dragon
- **Microsoft Threat Modeling Tool:** microsoft.com
- **IriusRisk:** iriusrisk.com

## Container Security

- **Trivy:** aquasec.com/trivy (vulnerability scanner)
- **Clair:** github.com/quay/clair (static analysis)
- **Falco:** falco.org (runtime security)
- **Sysdig:** sysdig.com (runtime protection)

## Kubernetes Security

- **kube-bench:** github.com/aquasecurity/kube-bench (CIS benchmarks)
- **kube-hunter:** github.com/aquasecurity/kube-hunter (pentesting)
- **Kyverno:** kyverno.io (policy engine)
- **OPA Gatekeeper:** open-policy-agent.github.io/gatekeeper

## Network Security

- **Wireshark:** wireshark.org (packet analysis)
- **tcpdump:** tcpdump.org (packet capture)
- **Netcat:** networking utility
- **iptables/nftables:** Linux firewalls

## Incident Response

### Frameworks
- **NIST:** nist.gov/incident-response
- **SANS:** sans.org/incident-response

### Ferramentas
- **TheHive:** thehive-project.org (case management)
- **MISP:** misp-project.org (threat intelligence)
- **GRR:** github.com/google/grr (live forensics)

## Compliance

- **GDPR:** data protection (EU)
- **HIPAA:** healthcare data (US)
- **PCI DSS:** payment card data
- **SOC 2:** service organization controls
- **ISO 27001:** information security management

## Recursos
- OWASP: owasp.org
- PortSwigger Research: portswigger.net/research
- HackerOne Hacktivity: hackerone.com
- Hack The Box: hackthebox.com
- TryHackMe: tryhackme.com