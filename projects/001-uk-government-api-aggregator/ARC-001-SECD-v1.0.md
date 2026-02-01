# UK Government Secure by Design Assessment

> **Template Status**: Beta | **Version**: 1.1.0 | **Command**: `/arckit.secure`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-SECD-v1.0 |
| **Document Type** | Secure by Design Assessment |
| **Project** | UK Government API Aggregator (Project 001) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-02-01 |
| **Last Modified** | 2026-02-01 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-01 |
| **Owner** | Security Architect, GDS |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | SIRO, Security Team, Architecture Team, NCSC Advisor, DPO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-01 | ArcKit AI | Initial creation from `/arckit.secure` command | PENDING | PENDING |

## Document Purpose

This document assesses the security posture of the **UK Government API Aggregator** platform against the NCSC Cyber Assessment Framework (CAF), Cyber Essentials, and UK GDPR requirements. The platform aggregates APIs from 34+ government departments through a unified gateway, handling OFFICIAL and OFFICIAL-SENSITIVE data. This assessment identifies security controls required, gaps in the current design, and remediation actions needed before progressing through Alpha, Beta, and Live phase gates.

**Project Context**:
- **Department**: Government Digital Service (GDS) / Central Digital and Data Office (CDDO)
- **Data Classification**: OFFICIAL (catalogue metadata, developer accounts); OFFICIAL-SENSITIVE (upstream API credentials, some proxied personal data from NHS/DWP/HMRC)
- **Project Phase**: Discovery/Alpha
- **User Base**: Public-facing (developer portal) + internal (platform admin, department admins)
- **Hosting Approach**: Cloud-first (UK data centres)
- **Integration Scope**: 240+ upstream APIs across 34 departments, multiple authentication patterns (open, API key, OAuth 2.0, JWT, mutual TLS, NHS CIS2)

---

## Executive Summary

**Overall Security Posture**: Needs Improvement (Architecture phase — controls designed but not yet implemented)

**NCSC Cyber Assessment Framework (CAF) Score**: 6/14 principles achieved or partially achieved at design level

**Key Security Findings**:
- **High-Value Target**: The platform aggregates credentials for 34+ government departments — a single compromise could expose multiple department APIs. This is explicitly flagged by NCSC (SD-4) as the primary security concern.
- **Credential Isolation**: The architecture specifies per-department credential isolation (NFR-SEC-005), which is essential but complex to implement. This must be validated before Beta.
- **Multi-Auth Gateway**: Supporting 6+ authentication patterns (none, API key, OAuth 2.0, JWT, mTLS, NHS CIS2) increases the attack surface significantly.
- **Personal Data Proxying**: When the gateway proxies HMRC, NHS, or DWP APIs returning personal data, the platform becomes a data processor under UK GDPR — requiring DPIA before any personal data flows.
- **Strong Security Requirements**: The requirements document (ARC-001-REQ-v1.0) contains 7 comprehensive security NFRs (SEC-001 through SEC-007) and 4 compliance NFRs — a solid foundation.

**Cyber Essentials Status**: Not Started (required before Beta)

**Risk Summary**: **High** — The platform's role as a credential aggregator creates a uniquely high-value target. Security architecture is well-specified in requirements but unimplemented. Critical path: credential isolation, DPIA, penetration testing.

---

## 1. NCSC Cyber Assessment Framework (CAF) Assessment

### Objective A: Managing Security Risk

**A1: Governance**

**Status**: ⚠️ Partially Achieved

**Evidence**:
The project has identified NCSC as a key stakeholder (SD-4) and established security as a core architecture principle (Principle 4: Security by Design). The SRO is identified (SD-6) as accountable for programme governance. However, a SIRO has not yet been formally appointed for this specific platform, and security policies specific to the API Aggregator have not been drafted.

**Security Governance**:
- [x] Senior leadership owns information security (SRO identified — SD-6)
- [ ] Senior Information Risk Owner (SIRO) appointed for this platform
- [ ] Security policies and standards defined (platform-specific)
- [x] Security roles and responsibilities documented (NFR-SEC-002 defines roles)
- [x] Security risk management process established (risk flagged in stakeholder analysis)
- [ ] Security oversight and reporting in place

**Gaps/Actions**:
- **CRITICAL**: Appoint SIRO for the API Aggregator platform — must be Director-level within GDS/CDDO (0-30 days)
- **HIGH**: Draft platform-specific security policies: acceptable use, access control, data protection, cryptography (30-60 days)
- **MEDIUM**: Establish quarterly security review cadence with SIRO and NCSC advisor

---

**A2: Risk Management**

**Status**: ⚠️ Partially Achieved

**Evidence**:
The stakeholder analysis (ARC-001-STKE-v1.0) identifies 5 stakeholder risks including the high-value target concern (SD-4). The requirements document specifies comprehensive security NFRs. However, a formal threat model for the platform has not been completed, and a security risk register does not yet exist.

**Risk Management Process**:
- [x] Information assets identified and classified (data entities defined in REQ, data classification per-API)
- [ ] Threats and vulnerabilities assessed (no formal threat model)
- [x] Risk assessment methodology defined (stakeholder risks identified)
- [ ] Risk register maintained and reviewed
- [ ] Risk treatment plans implemented
- [ ] Residual risks accepted by SIRO

**Gaps/Actions**:
- **CRITICAL**: Complete STRIDE threat model for the gateway, focusing on: credential aggregation attack surface, upstream API impersonation, consumer token theft, rate limit bypass, response data leakage (0-30 days)
- **HIGH**: Create security risk register with: credential compromise scenarios, upstream API dependency risks, DDoS against gateway, insider threat from platform admins (30-60 days)
- **HIGH**: Define risk appetite with SIRO — particularly for cascading credential compromise

---

**A3: Asset Management**

**Status**: ⚠️ Partially Achieved

**Evidence**:
The data source discovery document (ARC-001-DSCT-v1.0) catalogues 240+ upstream APIs across 34 departments. Data entities are well-defined in requirements (API Catalogue Entry, Developer Account, API Key, Department, Usage Record). However, no formal asset register exists for the platform's own infrastructure.

**Asset Management**:
- [x] Hardware inventory maintained (not yet — design phase, cloud infrastructure not provisioned)
- [x] Software inventory maintained (not yet — design phase)
- [x] Data assets catalogued (data entities defined in ARC-001-REQ-v1.0, upstream APIs catalogued in ARC-001-DSCT-v1.0)
- [x] Asset ownership assigned (department ownership model defined)
- [ ] Asset lifecycle management
- [ ] Secure disposal procedures

**Gaps/Actions**:
- **MEDIUM**: Establish asset register template for cloud infrastructure (to be populated during implementation)
- **LOW**: Define secure disposal procedures for API keys and developer accounts (aligned with NFR-C-001 retention policy)

---

**A4: Supply Chain**

**Status**: ⚠️ Partially Achieved

**Evidence**:
The platform integrates with 34+ government departments as upstream API providers. The data source discovery document identifies authentication methods, rate limits, and SLAs per department. However, no formal supply chain security assessment has been conducted for upstream departments or cloud hosting providers.

**Supply Chain Security**:
- [x] Supplier security requirements defined (NFR-SEC-005 credential isolation, per-department circuit breakers)
- [ ] Supplier security assessments conducted (upstream department security not assessed)
- [ ] Contracts include security obligations (no data sharing agreements with upstream departments yet)
- [x] Third-party access controlled (tiered access model in requirements)
- [ ] Supply chain risk register
- [ ] Open source software risks managed

**Gaps/Actions**:
- **HIGH**: Assess upstream department API security posture — particularly for departments where the aggregator stores credentials (HMRC, DVLA, NHS, HMLR)
- **HIGH**: Establish data sharing/processing agreements with each upstream department before proxying their APIs
- **MEDIUM**: Define open source dependency management policy (SCA scanning specified in NFR-SEC-006)
- **MEDIUM**: Create supply chain risk register for cloud provider, upstream departments, and third-party libraries

---

### Objective B: Protecting Against Cyber Attack

**B1: Service Protection Policies and Processes**

**Status**: ❌ Not Achieved

**Evidence**:
The requirements document specifies security controls but platform-specific security policies have not been drafted. Architecture principles (ARC-000-PRIN-v1.0, Principle 4) establish security-by-design intent but are not operational policies.

**Protection Policies**:
- [ ] Acceptable Use Policy
- [ ] Access Control Policy (requirements define roles but no policy document)
- [ ] Data Protection Policy
- [ ] Secure Development Policy
- [ ] Network Security Policy
- [ ] Cryptography Policy

**Gaps/Actions**:
- **HIGH**: Draft 6 core security policies aligned with requirements NFR-SEC-001 through NFR-SEC-007 (60 days)
- **MEDIUM**: Align policies with GDS existing organisational policies where available

---

**B2: Identity and Access Control**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Comprehensive IAM requirements exist: RBAC with 4 roles (NFR-SEC-002), MFA for portal and admin (NFR-SEC-001), session management (30-min idle, 8-hour absolute), API key + OAuth 2.0 for gateway access. The requirements are well-specified but unimplemented.

**Access Controls**:
- [x] User accounts managed centrally (requirement specified — Developer, Dept Admin, Platform Admin, Viewer)
- [x] Multi-factor authentication (MFA) enabled (requirement specified — authenticator app, hardware key)
- [x] Privileged access management (PAM) (requirement specified — Platform Admin role, re-auth for sensitive actions)
- [x] Least privilege principle enforced (requirement specified — RBAC with 4 roles)
- [ ] Regular access reviews (not specified — add quarterly access review requirement)
- [ ] Account provisioning/deprovisioning process (not detailed)
- [x] Strong password policy (not explicitly specified — add 12+ character requirement)

**Authentication Method**: API Key + OAuth 2.0 (gateway); GOV.UK One Login or equivalent (portal)

**Gaps/Actions**:
- **MEDIUM**: Add quarterly access review requirement for all privileged accounts
- **MEDIUM**: Define account deprovisioning process for departed staff and revoked consumers
- **LOW**: Specify minimum password complexity (12+ characters, align with NCSC guidance)

---

**B3: Data Security**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Strong encryption requirements: TLS 1.2+ (1.3 preferred) in transit, AES-256 at rest, per-department credential encryption, API keys hashed in storage (NFR-SEC-003). Secrets management with 90-day rotation (NFR-SEC-004). UK data residency required (NFR-C-001). However, DPIA has not been completed.

**Data Protection**:
- [x] Data classification scheme implemented (OFFICIAL for catalogue, OFFICIAL-SENSITIVE for credentials and personal data)
- [x] Encryption at rest (AES-256 minimum) — specified in NFR-SEC-003
- [x] Encryption in transit (TLS 1.3 minimum) — specified in NFR-SEC-003
- [ ] Data loss prevention (DLP) controls — not specified
- [ ] Secure data destruction — not specified
- [x] UK GDPR compliance — requirements specified in NFR-C-001
- [x] Data retention policy — defined (active + 30 days for accounts, 2 years for audit logs)

**Personal Data Processing**: Yes (developer accounts contain PII; proxied responses from HMRC/NHS/DWP may contain taxpayer/patient/benefit data)

**DPIA Completed**: No — **REQUIRED before processing any personal data through the gateway**

**Gaps/Actions**:
- **CRITICAL**: Complete DPIA before Beta phase — covers developer account PII and proxied personal data from upstream APIs (0-60 days)
- **HIGH**: Implement Data Loss Prevention (DLP) controls to prevent personal data leakage through gateway logs or analytics (60-90 days)
- **HIGH**: Define secure data destruction procedures for developer accounts, API keys, and cached upstream responses
- **MEDIUM**: Implement no-cache policy for all proxied responses containing personal data (NFR-C-001 specifies this)

---

**B4: System Security**

**Status**: ⚠️ Partially Achieved

**Evidence**:
The requirements specify comprehensive vulnerability management (NFR-SEC-006): SAST on every PR, DAST in staging, dependency scanning, penetration testing at phase gates, remediation SLAs (critical: 24h, high: 7d, medium: 30d). Input validation requirements (NFR-SEC-007) address OWASP API Security Top 10. However, no baseline configurations or hardening standards are specified.

**System Hardening**:
- [ ] Secure baseline configurations (not specified — need CIS benchmarks for cloud infrastructure)
- [x] Unnecessary services disabled (implied by cloud-native architecture)
- [x] Security patches applied timely (NFR-SEC-006 specifies remediation SLAs)
- [ ] Anti-malware deployed (cloud-native — need container scanning instead)
- [ ] Application whitelisting (where appropriate)
- [ ] Host-based firewalls (cloud security groups specified)
- [ ] Endpoint Detection and Response (EDR)

**Operating Systems**: Linux (cloud-native, containerised)

**Gaps/Actions**:
- **HIGH**: Define CIS-benchmarked secure baseline for container images and cloud infrastructure
- **MEDIUM**: Implement container image scanning in CI/CD pipeline
- **MEDIUM**: Specify runtime security monitoring for containers (Falco, Aqua, or equivalent)

---

**B5: Resilient Networks**

**Status**: ⚠️ Partially Achieved

**Evidence**:
The architecture requires: circuit breakers per upstream API (FR-013), bulkhead isolation between adapters (NFR-A-003), DDoS protection (implied by rate limiting FR-012), network segmentation between gateway, portal, and admin components. Multi-AZ deployment specified (NFR-A-002).

**Network Security**:
- [x] Network segmentation by function/sensitivity (gateway, portal, admin, database — implied)
- [ ] Firewalls at network boundaries (cloud security groups — not explicitly specified)
- [ ] Intrusion Detection/Prevention Systems (IDS/IPS) — not specified
- [x] DDoS protection (rate limiting specified — FR-012, multi-tier)
- [ ] Secure remote access (VPN) — not specified for platform admin
- [ ] Network Access Control (NAC)
- [ ] WiFi security (N/A — cloud-hosted)

**Network Architecture**: Cloud (UK data centres, multi-AZ)

**Gaps/Actions**:
- **HIGH**: Specify Web Application Firewall (WAF) for the developer portal and gateway endpoint
- **HIGH**: Implement IDS/IPS for gateway traffic — detect anomalous API usage patterns
- **MEDIUM**: Specify VPN or zero-trust network access for platform administration
- **MEDIUM**: Define network security groups with explicit deny-all default

---

**B6: Staff Awareness and Training**

**Status**: ❌ Not Achieved

**Evidence**:
No security awareness programme has been defined for the platform team. GDS organisational training may exist but platform-specific training (e.g., handling upstream credentials, incident response for credential compromise) is not specified.

**Security Training**:
- [ ] Mandatory security awareness training
- [ ] Phishing awareness training
- [ ] Role-based security training (credential handling for ops team)
- [ ] Annual security refresher
- [ ] Security incident reporting awareness
- [ ] Data protection training (UK GDPR)
- [ ] Social engineering awareness

**Training Completion Rate**: N/A (not established)

**Gaps/Actions**:
- **HIGH**: Define platform-specific security training covering: upstream credential handling, incident response for credential compromise, personal data handling rules (60-90 days)
- **MEDIUM**: Ensure all platform team members complete GDS security awareness and UK GDPR training before Beta
- **LOW**: Implement phishing simulation for platform admin accounts

---

### Objective C: Detecting Cyber Security Events

**C1: Security Monitoring**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Comprehensive observability requirements exist (NFR-M-001): structured JSON logs with correlation IDs, distributed tracing, real-time dashboards, SLO-based alerting. Audit logging (NFR-C-002) specifies tamper-evident logs with 2-year retention. However, no SIEM solution is specified and security-specific monitoring (vs. operational monitoring) is not differentiated.

**Monitoring Capabilities**:
- [x] Centralized logging (SIEM) — structured logging specified, SIEM solution not chosen
- [x] Real-time security alerting — SLO-based alerting specified
- [x] Log retention (minimum 12 months) — 2-year retention specified
- [ ] Security event correlation — not differentiated from operational monitoring
- [ ] User behavior analytics — not specified
- [ ] Threat intelligence integration — not specified
- [ ] File integrity monitoring — not specified

**SIEM Solution**: Not yet selected

**Gaps/Actions**:
- **HIGH**: Select and specify SIEM solution (Azure Sentinel, Splunk, or AWS Security Hub) for security event correlation distinct from operational monitoring
- **HIGH**: Define security-specific alerting rules: failed authentication patterns, credential access anomalies, rate limit abuse, unusual API traversal patterns
- **MEDIUM**: Implement user behaviour analytics for platform admin and department admin accounts
- **MEDIUM**: Integrate NCSC threat intelligence feeds

---

**C2: Proactive Security Event Discovery**

**Status**: ⚠️ Partially Achieved

**Evidence**:
Requirements specify: SAST on every PR, DAST in staging, dependency scanning, and penetration testing before each phase gate (NFR-SEC-006). OWASP API Security Top 10 explicitly addressed. However, no threat hunting capability, red team exercises, or security posture reviews are specified.

**Proactive Measures**:
- [ ] Threat hunting activities
- [x] Vulnerability scanning (weekly/monthly) — automated in CI/CD
- [x] Penetration testing (annual minimum) — before each phase gate
- [ ] Red team exercises
- [ ] Security posture reviews
- [ ] Threat modeling (not yet completed)

**Last Penetration Test**: Not Conducted (pre-implementation phase)
**Pen Test Findings**: N/A

**Gaps/Actions**:
- **CRITICAL**: Complete threat model before Beta (STRIDE methodology targeting credential aggregation attack surface)
- **HIGH**: Schedule independent penetration testing before Beta gate — must specifically test: credential isolation, auth bypass between departments, API key enumeration, rate limit bypass, response data leakage
- **MEDIUM**: Plan red team exercise for Live phase — simulate credential compromise scenario

---

### Objective D: Minimising the Impact of Cyber Security Incidents

**D1: Response and Recovery Planning**

**Status**: ⚠️ Partially Achieved

**Evidence**:
DR requirements specify RTO of 4 hours, RPO of 1 hour (NFR-A-002). Automatic failover to secondary AZ within 5 minutes. ICO breach notification within 72 hours (NFR-C-001). However, no incident response plan, incident classification scheme, or communication plan has been documented.

**Incident Response**:
- [ ] Incident response plan documented
- [ ] Incident response team defined
- [ ] Incident classification scheme
- [ ] Escalation procedures defined
- [ ] Communication plan for incidents
- [x] Regulatory reporting process (ICO) — 72-hour notification specified
- [ ] Lessons learned process

**IR Plan Last Tested**: Not Tested

**Business Continuity**:
- [x] Business continuity plan (BCP) — high-level requirements exist
- [x] Disaster recovery plan (DRP) — NFR-A-002 specifies RPO/RTO
- [x] Recovery time objective (RTO) defined — 4 hours
- [x] Recovery point objective (RPO) defined — 1 hour
- [ ] BC/DR testing conducted

**RTO**: 4 hours
**RPO**: 1 hour

**Gaps/Actions**:
- **CRITICAL**: Document incident response plan with specific scenarios: (1) upstream credential compromise, (2) platform-wide breach, (3) single-department credential leak, (4) DDoS, (5) data breach affecting personal data (0-30 days)
- **HIGH**: Define incident response team, escalation matrix, and communication plan including department notification
- **HIGH**: Define credential compromise playbook: detect → isolate affected department → rotate credentials → notify department → forensics → ICO notification if personal data affected
- **MEDIUM**: Plan BC/DR testing before Beta

---

**D2: Improvements**

**Status**: ❌ Not Achieved

**Evidence**:
No continuous improvement process for security has been established. No security metrics are defined beyond the operational SLOs.

**Continuous Improvement**:
- [ ] Post-incident reviews conducted
- [ ] Security metrics tracked
- [ ] Security improvements implemented
- [ ] Lessons learned documented
- [ ] Security trends analyzed
- [ ] Security roadmap maintained

**Gaps/Actions**:
- **MEDIUM**: Define security metrics: mean time to detect (MTTD), mean time to respond (MTTR), vulnerability remediation rates, failed auth rates, credential rotation compliance
- **MEDIUM**: Establish post-incident review (PIR) process
- **LOW**: Create security improvement roadmap aligned with platform phases

---

## 2. Cyber Essentials / Cyber Essentials Plus

### Cyber Essentials Status

**Current Status**: Not Started

**Certification Date**: N/A
**Expiry Date**: N/A

**Cyber Essentials Requirements**:

| Control Area | Status | Evidence |
|--------------|--------|----------|
| **Firewalls** | ⚠️ Partially | Cloud security groups specified; WAF not yet specified |
| **Secure Configuration** | ⚠️ Partially | Container security specified; CIS benchmarks not adopted |
| **Access Control** | ⚠️ Partially | RBAC + MFA specified in requirements; not implemented |
| **Malware Protection** | ❌ Not Achieved | Container scanning not yet specified |
| **Patch Management** | ✅ Achieved (Design) | Remediation SLAs defined (critical: 24h, high: 7d) |

**Cyber Essentials Plus Additional Requirements**:
- [ ] External vulnerability scan passed
- [ ] Internal vulnerability scan passed
- [ ] System configuration review passed

**Target Certification Level**: Cyber Essentials Plus (required before Live — platform handles personal data and upstream credentials)

**Gaps/Actions**:
- **CRITICAL**: Obtain Cyber Essentials Basic before Beta phase gate
- **HIGH**: Obtain Cyber Essentials Plus before Live phase gate
- **HIGH**: Engage Cyber Essentials certification body early in Beta

---

## 3. UK GDPR and Data Protection

### 3.1 Data Protection Compliance

**Data Protection Officer (DPO) Appointed**: Required (GDS is a public authority)

**ICO Registration**: Required (processing personal data — developer accounts, proxied responses)

**UK GDPR Compliance**:
- [x] Lawful basis for processing identified (legitimate interests for developer accounts; contract/legal obligation for proxied data depends on upstream API)
- [ ] Privacy notice published
- [ ] Data subject rights procedures (access, deletion, portability for developer accounts)
- [x] Data retention policy defined (active + 30 days for accounts; 2 years for audit/analytics)
- [x] Data breach notification process (72 hours) — specified in NFR-C-001
- [ ] Data processing agreements with suppliers (upstream departments, cloud provider)
- [ ] Records of processing activities (ROPA)

**Personal Data Processed**: Yes
- Developer accounts: email, name, organisation (OFFICIAL)
- Proxied API responses: may contain taxpayer data (HMRC), patient data (NHS), benefit data (DWP), driver data (DVLA) — all OFFICIAL-SENSITIVE

**Special Category Data**: Potentially Yes (NHS APIs may return health data — special category under UK GDPR Article 9)

**Gaps/Actions**:
- **CRITICAL**: Publish privacy notice for developer portal before Beta (0-30 days)
- **CRITICAL**: Establish data subject rights procedures for developer accounts (0-30 days)
- **HIGH**: Execute data processing agreements with each upstream department before proxying personal data
- **HIGH**: Create Records of Processing Activities (ROPA) — Article 30 UK GDPR
- **MEDIUM**: Clarify controller/processor status: platform is a processor when proxying upstream personal data; controller for developer account data

### 3.2 Data Protection Impact Assessment (DPIA)

**DPIA Required**: Yes — high-risk processing (aggregating personal data from multiple government departments at scale)

**DPIA Status**: Not Started

**DPIA Findings**:
- High risks identified: N/A (DPIA not started)
- Mitigations implemented: N/A
- Residual risks accepted: N/A

**ICO Consultation Required**: Potentially — depends on DPIA findings. The aggregation of credentials for 34+ departments and potential personal data proxying may require prior consultation under Article 36.

**Gaps/Actions**:
- **CRITICAL**: Complete DPIA before processing any personal data through the gateway — must cover: developer account PII, proxied personal data from HMRC/NHS/DWP/DVLA, credential aggregation risk, breach notification cascading to multiple departments (0-60 days)
- **HIGH**: Consult DPO on whether ICO prior consultation is required under Article 36
- **MEDIUM**: Conduct separate DPIAs for each department's personal data APIs as they are onboarded (Phase 2)

---

## 4. Secure Development Practices

### 4.1 Secure Software Development Lifecycle (SDLC)

**Development Methodology**: DevOps / Agile

**Secure Development Practices**:
- [x] Secure coding standards defined (implied by NFR-SEC-007 input validation)
- [x] Security requirements in user stories (7 security NFRs specified)
- [ ] Threat modeling in design phase (not completed)
- [ ] Code review includes security (not specified — add to definition of done)
- [x] Static Application Security Testing (SAST) — specified in NFR-SEC-006
- [x] Dynamic Application Security Testing (DAST) — specified in NFR-SEC-006
- [x] Software Composition Analysis (SCA) — dependency scanning specified
- [x] Dependency vulnerability scanning — specified in NFR-SEC-006

**OWASP API Security Top 10 Mitigation** (per NFR-SEC-007):
- [x] Broken Object Level Authorization — RBAC with per-department isolation
- [x] Broken Authentication — MFA, session management, API key hashing
- [x] Broken Object Property Level Authorization — RBAC roles specified
- [x] Unrestricted Resource Consumption — Multi-tier rate limiting (FR-012)
- [x] Broken Function Level Authorization — Role-based endpoint access
- [x] Unrestricted Access to Sensitive Business Flows — Rate limiting + circuit breakers
- [x] Server Side Request Forgery — Gateway routes only to known upstream APIs
- [x] Security Misconfiguration — Hardening requirements specified
- [x] Improper Inventory Management — API catalogue with versioning (FR-015)
- [x] Unsafe Consumption of APIs — Input validation, circuit breakers, timeout controls

**Gaps/Actions**:
- **HIGH**: Complete STRIDE threat model before implementation begins
- **MEDIUM**: Add security-focused code review to Definition of Done
- **MEDIUM**: Specify OWASP ZAP or equivalent for automated DAST in staging

### 4.2 DevSecOps

**CI/CD Security Integration**:
- [x] Automated security testing in pipeline — SAST + dependency scanning specified
- [x] Secrets scanning (no hardcoded credentials) — NFR-SEC-004
- [ ] Container image scanning — not specified
- [ ] Infrastructure as Code (IaC) security — not specified
- [ ] Build artifact signing — not specified
- [ ] Automated deployment security checks — not specified

**Gaps/Actions**:
- **HIGH**: Add container image scanning to CI/CD pipeline (Trivy, Snyk, or equivalent)
- **HIGH**: Add IaC security scanning (Checkov, tfsec, or equivalent) for cloud infrastructure templates
- **MEDIUM**: Implement build artifact signing for deployment artifacts
- **MEDIUM**: Add automated security gate in deployment pipeline (block deployment if critical/high vulnerabilities)

---

## 5. Cloud Security

### 5.1 Cloud Service Provider

**Cloud Provider**: To be determined (UK cloud region required — AWS London, Azure UK South, or GCP London)

**Cloud Deployment Model**: Public cloud

**Data Residency**: UK (mandatory — NFR-C-001)

**Cloud Security Controls**:
- [ ] Cloud Security Posture Management (CSPM)
- [x] Identity and Access Management (IAM) — RBAC specified
- [x] Encryption key management — per-department key isolation specified (NFR-SEC-005)
- [ ] Network security groups — not specified (implied by cloud architecture)
- [ ] Cloud Access Security Broker (CASB)
- [ ] Cloud security monitoring
- [x] Multi-region redundancy — multi-AZ specified (NFR-A-002)

**NCSC Cloud Security Principles**: Assessment required once cloud provider selected

**Gaps/Actions**:
- **HIGH**: Select cloud provider and conduct NCSC Cloud Security Principles assessment (14 principles)
- **HIGH**: Implement CSPM (AWS Security Hub, Azure Defender, or equivalent)
- **MEDIUM**: Define network security groups with explicit deny-all default
- **MEDIUM**: Implement cloud-native WAF for gateway and portal endpoints

---

## 6. Vulnerability and Patch Management

### 6.1 Vulnerability Management

**Vulnerability Scanning Frequency**: Continuous (CI/CD integrated) + Weekly (infrastructure)

**Scanning Coverage**: Target 100% of deployed assets

**Vulnerability Management Process**:
- [x] Automated vulnerability scanning — SAST, DAST, SCA specified
- [x] Vulnerability prioritization (CVSS scores) — implied by remediation tiers
- [x] Remediation SLAs defined — Critical: 24h, High: 7d, Medium: 30d
- [ ] Exception process for unfixable vulnerabilities
- [ ] Vulnerability remediation tracking
- [ ] Metrics and reporting

**Remediation SLAs** (from NFR-SEC-006):
- Critical vulnerabilities: Within 24 hours
- High vulnerabilities: Within 7 days
- Medium vulnerabilities: Within 30 days
- Low vulnerabilities: Next scheduled release

**Current Vulnerability Status**: N/A (pre-implementation)

**Gaps/Actions**:
- **MEDIUM**: Define vulnerability exception process for cases where patching would break upstream API compatibility
- **LOW**: Define vulnerability metrics dashboard

### 6.2 Patch Management

**Patch Management Process**:
- [x] Patch assessment and testing — CI/CD pipeline
- [ ] Patch deployment schedule
- [ ] Emergency patching process (aligned with 24h critical SLA)
- [ ] Patch compliance monitoring
- [ ] Rollback procedures

**Patch Compliance**: N/A (pre-implementation)

**Critical Patch SLA**: Within 24 hours (NFR-SEC-006)

**Gaps/Actions**:
- **MEDIUM**: Define emergency patching process aligned with 24-hour critical SLA
- **MEDIUM**: Define rollback procedures for failed security patches

---

## 7. Third-Party and Supply Chain Risk

### 7.1 Third-Party Risk Management

**Third-Party Security Assessment**:
- [ ] Vendor security questionnaires
- [ ] Vendor security certifications verified
- [ ] Data Processing Agreements (DPAs) in place
- [x] Third-party access controls — tiered access model specified
- [ ] Vendor risk register
- [ ] Ongoing vendor monitoring

**Key Third Parties**:

| Vendor/Department | Service | Security Rating | Risk Level | Mitigations |
|-------------------|---------|-----------------|------------|-------------|
| HMRC | Tax APIs (31) | High (NCSC-engaged) | Medium | OAuth 2.0, per-dept credential isolation |
| Companies House | Company data APIs | Medium | Low | API key, OGL data |
| DVLA | Vehicle/driver APIs | High | Medium | API key + JWT, PII handling |
| NHS Digital | Health APIs (93) | High (NHS IG Model) | High | OAuth 2.0 + NHS CIS2, clinical data controls |
| DWP | Benefits APIs (10) | High | High | OAuth 2.0 enhanced, sensitive PII |
| Environment Agency | Environmental data (10) | Low (open data) | Low | No auth, no PII |
| Ordnance Survey | Geospatial APIs (5) | Medium | Low | API key, commercial licensing |
| HM Land Registry | Property APIs (13) | Medium | Medium | API key + mTLS, PII (owners) |
| Cloud Provider (TBD) | Infrastructure | TBD | High | TBD — NCSC Cloud Security Principles |
| VE3 Global | Fuel Finder data | TBD | Low | Open data scheme |

**Gaps/Actions**:
- **HIGH**: Conduct security assessment of cloud provider against NCSC 14 Cloud Security Principles
- **HIGH**: Establish data processing agreements with HMRC, DVLA, NHS, DWP, HMLR before proxying personal data
- **MEDIUM**: Create supply chain risk register covering all upstream departments and cloud provider

### 7.2 Open Source Security

**Open Source Components**: To be determined (design phase)

**OSS Security Controls**:
- [x] Software Bill of Materials (SBOM) — dependency scanning implies SCA
- [x] Automated dependency scanning — specified in NFR-SEC-006
- [x] Known vulnerability detection (CVE) — CI/CD integrated
- [ ] License compliance checks
- [ ] OSS component lifecycle management

**Gaps/Actions**:
- **MEDIUM**: Add open source license compliance scanning (FOSSA, Black Duck, or equivalent)
- **LOW**: Define OSS component selection criteria and lifecycle management

---

## 8. Backup and Recovery

### 8.1 Backup Strategy

**Backup Method**: To be determined (cloud-native approach expected)

**Backup Controls**:
- [ ] Automated backups scheduled
- [x] Backup encryption enabled — AES-256 at rest specified
- [x] Offsite/cloud backups — separate UK availability zone (NFR-A-002)
- [ ] Immutable backups (ransomware protection)
- [ ] Backup integrity testing
- [ ] Backup restoration testing

**Backup Frequency**: Hourly for transactional data, daily for configuration (NFR-A-002)

**Backup Retention**: 30 days for operational, 2 years for audit data (NFR-A-002)

**Last Successful Backup**: N/A (pre-implementation)

**Last Restoration Test**: N/A

**Gaps/Actions**:
- **HIGH**: Specify immutable backup storage for ransomware protection
- **MEDIUM**: Define backup restoration testing schedule (quarterly minimum)
- **MEDIUM**: Ensure backup strategy covers: developer accounts, API keys, audit logs, platform configuration, upstream credential vault

### 8.2 Recovery Capabilities

**Recovery Time Objective (RTO)**: 4 hours (NFR-A-002)
**Recovery Point Objective (RPO)**: 1 hour (NFR-A-002)

**Recovery Testing**: Not Tested

**Recovery Success Rate**: N/A

**Gaps/Actions**:
- **HIGH**: Document and test DR procedures before Beta
- **MEDIUM**: Define automated failover testing schedule

---

## Overall Security Assessment Summary

### NCSC CAF Scorecard

| CAF Objective | Principles Achieved | Status |
|---------------|---------------------|--------|
| A. Managing Security Risk | 0/4 fully achieved (4/4 partially) | ⚠️ |
| B. Protecting Against Cyber Attack | 0/6 fully achieved (4/6 partially, 2 not achieved) | ⚠️ |
| C. Detecting Cyber Security Events | 0/2 fully achieved (2/2 partially) | ⚠️ |
| D. Minimising Impact of Incidents | 0/2 fully achieved (1/2 partially, 1 not achieved) | ❌ |
| **Overall** | **0/14 fully achieved (11/14 partially)** | **⚠️ Needs Improvement** |

### Security Posture Summary

**Strengths**:
- Comprehensive security requirements specified (7 security NFRs, 4 compliance NFRs)
- Per-department credential isolation designed (NFR-SEC-005)
- Multi-tier rate limiting architecture (FR-012)
- Circuit breaker and fault isolation patterns (FR-013, NFR-A-003)
- Strong encryption requirements (TLS 1.3, AES-256, key isolation)
- OWASP API Security Top 10 explicitly addressed (NFR-SEC-007)
- DevSecOps pipeline specified (SAST, DAST, SCA, pen testing)

**Critical Gaps**:
- No SIRO appointed for the platform
- No threat model completed
- No DPIA completed (legally required before processing personal data)
- No incident response plan (especially credential compromise scenarios)
- No Cyber Essentials certification
- Security policies not drafted
- SIEM not selected

**Overall Risk Rating**: **High** — The platform's role as a credential aggregator for 34+ government departments creates a uniquely high-value target. Security architecture is well-specified in requirements but entirely unimplemented. The gap between design intent and operational reality must be closed before Beta.

### Critical Security Issues

1. **No DPIA for personal data processing** (CAF B3, UK GDPR Art. 35) — **CRITICAL** — Legally required before any personal data flows through the gateway. Blocks Beta.
2. **No SIRO appointed** (CAF A1) — **CRITICAL** — No senior executive accountable for platform security risk. Blocks formal risk acceptance.
3. **No threat model** (CAF A2, C2) — **CRITICAL** — The credential aggregation attack surface has not been formally analysed. Must complete before implementation.
4. **No incident response plan** (CAF D1) — **HIGH** — No playbook for credential compromise affecting multiple departments. A breach could cascade across government.
5. **No Cyber Essentials certification** (CE) — **HIGH** — Required for government service handling personal data. Must achieve Basic before Beta.
6. **Security policies not drafted** (CAF B1) — **HIGH** — Architecture principles exist but operational security policies do not.
7. **No SIEM solution selected** (CAF C1) — **HIGH** — Security monitoring indistinguishable from operational monitoring.

### Recommendations

**Critical Priority** (0-30 days — must resolve before Alpha gate):
- Appoint SIRO — GDS Director level — Security Architect to recommend — 14 days
- Complete STRIDE threat model for credential aggregation attack surface — Security Architect — 30 days
- Begin DPIA — DPO — 30 days (complete within 60 days)
- Document incident response plan with credential compromise playbook — Security Architect — 30 days

**High Priority** (1-3 months — must resolve before Beta gate):
- Obtain Cyber Essentials Basic certification — IT Security — 60 days
- Draft 6 core security policies — Security Architect — 60 days
- Select SIEM solution and define security alerting rules — Security Architect — 60 days
- Execute data processing agreements with upstream departments — Legal/DPO — 90 days
- Conduct independent penetration test before Beta — External tester — 90 days
- Define CIS-benchmarked secure baselines for cloud infrastructure — DevSecOps — 60 days
- Add container image scanning and IaC security to CI/CD — DevSecOps — 60 days

**Medium Priority** (3-6 months — continuous improvement towards Live):
- Obtain Cyber Essentials Plus — IT Security — 6 months
- Implement DLP controls for gateway logs — DevSecOps — 90 days
- Implement WAF for gateway and portal — DevSecOps — 90 days
- Platform-specific security training for team — Security Architect — 90 days
- Quarterly access reviews for privileged accounts — Security Architect — Ongoing
- Supply chain risk register for all upstream departments — Security Architect — 90 days
- Plan red team exercise for Live phase — NCSC Advisor — 6 months

---

## Next Steps and Action Plan

**Immediate Actions** (0-30 days):
- [ ] Appoint SIRO — GDS Director — 14 days
- [ ] Complete STRIDE threat model — Security Architect — 30 days
- [ ] Begin DPIA — DPO — 30 days
- [ ] Document incident response plan — Security Architect — 30 days
- [ ] Publish developer portal privacy notice — DPO — 30 days

**Short-term Actions** (1-3 months):
- [ ] Complete DPIA — DPO — 60 days
- [ ] Obtain Cyber Essentials Basic — IT Security — 60 days
- [ ] Draft security policies — Security Architect — 60 days
- [ ] Select SIEM solution — Security Architect — 60 days
- [ ] Execute DPAs with departments — Legal/DPO — 90 days
- [ ] Independent penetration test — External — before Beta gate
- [ ] Container image + IaC scanning in CI/CD — DevSecOps — 60 days

**Long-term Actions** (3-12 months):
- [ ] Obtain Cyber Essentials Plus — IT Security — 6 months
- [ ] Implement WAF + DLP — DevSecOps — 90 days
- [ ] Red team exercise — NCSC Advisor — before Live
- [ ] Annual penetration test programme — External — ongoing
- [ ] Quarterly security reviews with SIRO — Security Architect — ongoing

**Next Security Review**: 2026-05-01 (quarterly during development, annually in Live)

---

## Approval and Sign-Off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Project Lead | PENDING | | |
| Security Architect | PENDING | | |
| Senior Information Risk Owner (SIRO) | PENDING (to be appointed) | | |
| Data Protection Officer (DPO) | PENDING | | |
| NCSC Advisor | PENDING | | |

---

**Document Control**:
- **Version**: 1.0
- **Classification**: OFFICIAL-SENSITIVE
- **Last Reviewed**: 2026-02-01
- **Next Review**: 2026-05-01
- **Document Owner**: Security Architect, GDS

---

**Generated by**: ArcKit `/arckit.secure` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.1.0
**Project**: UK Government API Aggregator (Project 001)
**Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
**Generation Context**: Assessment based on ARC-001-REQ-v1.0 (55 requirements including NFR-SEC-001–007, NFR-C-001–004), ARC-001-STKE-v1.0 (stakeholder drivers including SD-4 NCSC), ARC-001-DSCT-v1.0 (240+ upstream APIs, 34 departments), ARC-000-PRIN-v1.0 (Principle 4: Security by Design)
