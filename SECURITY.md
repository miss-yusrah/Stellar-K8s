# Security Policy

## Supported Versions

We actively support the following versions with security updates:

| Version | Supported          |
| ------- | ------------------ |
| 0.2.x   | :white_check_mark: |
| 0.1.x   | :x:                |

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues.**

If you discover a security vulnerability in the Stellar-K8s operator, please report it by emailing:

**security@stellar-k8s.io**

Please include the following information in your report:

- **Type of issue** (e.g., buffer overflow, SQL injection, cross-site scripting, etc.)
- **Full paths of source file(s)** related to the manifestation of the issue
- **The location of the affected source code** (tag/branch/commit or direct URL)
- **Any special configuration required** to reproduce the issue
- **Step-by-step instructions** to reproduce the issue
- **Proof-of-concept or exploit code** (if possible)
- **Impact of the issue**, including how an attacker might exploit it

### What to Expect

- You will receive an acknowledgment within **48 hours**
- We will provide a more detailed response within **5 business days** indicating the next steps
- We will keep you informed of the progress towards a fix
- We may ask for additional information or guidance

### Disclosure Policy

- Security vulnerabilities will be handled according to responsible disclosure principles
- Once a fix is available, we will:
  1. Notify users through security advisories
  2. Release a patched version
  3. Credit the reporter (unless they wish to remain anonymous)
  4. Publish a security advisory with details

## Security Update Process

1. **Report received** - Security team acknowledges the report
2. **Validation** - Team validates and assesses severity (CVSS scoring)
3. **Fix development** - Patch is developed and tested
4. **Security advisory** - Advisory is drafted (kept private)
5. **Release** - Patched version is released
6. **Public disclosure** - Advisory is published with credits

## Security Best Practices

When deploying the Stellar-K8s operator, we recommend:

### Container Security
- Always use the latest stable version
- Scan container images for vulnerabilities regularly
- Use non-root users (already configured in our images)
- Implement Pod Security Standards/Policies

### Network Security
- Enable mTLS for inter-component communication
- Use network policies to restrict traffic
- Implement proper ingress/egress rules
- Enable audit logging

### RBAC & Permissions
- Follow principle of least privilege
- Use separate service accounts for different components
- Regularly audit RBAC permissions
- Enable admission webhooks

### Secrets Management
- Use Kubernetes secrets or external secret managers
- Enable encryption at rest for etcd
- Rotate secrets regularly
- Never commit secrets to version control

### Monitoring
- Enable security monitoring and alerting
- Review audit logs regularly
- Monitor for suspicious activity
- Set up vulnerability scanning in CI/CD

## Known Security Considerations

### API Authentication
The operator's REST API should be protected by:
- Network policies
- Ingress authentication
- mTLS (when enabled)

### CRD Validation
The operator uses webhook validation to prevent:
- Invalid configurations
- Resource exhaustion
- Privilege escalation

### Dependencies
We use:
- Dependabot for automated dependency updates
- Cargo audit for Rust security advisories
- Trivy for container scanning
- SBOM generation for supply chain security

## Security Scanning & Testing

Our CI/CD pipeline includes comprehensive automated security testing:

### Vulnerability Scanning
- **Trivy** - Container/FS/dependency scanning (CRITICAL/HIGH alerts)
- **Cargo Audit** - Rust crates.io advisories
- **SBOM Generation** - CycloneDX supply chain transparency
- **CodeQL** - Semantic code analysis (GitHub Advanced Security)

### Penetration Testing
- **k6** - API load/penetration scenarios (DDoS, slowloris sim)
- **OWASP ZAP** - Baseline DAST for operator REST API
- **Nuclei** - Template-based vulnerability scanning

### Compliance Testing
- **kube-bench** - CIS Kubernetes Benchmark automation
- **Checkov** - IaC scanning for Helm charts/manifests
- **kube-score** - K8s resource scoring

Run locally: `make security-all`

## Runtime Security Monitoring

- **Prometheus + Grafana** - Security metrics dashboard
- **Falco** - Behavioral runtime security (planned integration)
- **Audit Logs** - API/server audit trails
- **CVE Auto-remediation** - Controller-based patching (src/controller/cve.rs)

## Compliance

The operator is designed with the following standards in mind:
- CIS Kubernetes Benchmark
- NIST Cybersecurity Framework
- OWASP Top 10

## Contact

- **Security Email**: samuelotowo@gmail.com
- **General Issues**: https://github.com/stellar-k8s/issues
- **Discussions**: https://github.com/stellar-k8s/discussions

## Attribution

We appreciate responsible disclosure and will credit security researchers who:
- Report vulnerabilities responsibly
- Allow reasonable time for fixes
- Follow our disclosure policy

Thank you for helping keep Stellar-K8s secure! 🔒
