# Stakeholder Drivers & Goals Analysis: UK Government API Aggregator

> **Template Status**: Live | **Version**: 1.1.0 | **Command**: `/arckit.stakeholders`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-STKE-v1.0 |
| **Document Type** | Stakeholder Drivers & Goals Analysis |
| **Project** | UK Government API Aggregator (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-02-01 |
| **Last Modified** | 2026-02-01 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-01 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Programme Board, Architecture Team, GDS, Department API Owners, Security Team |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-01 | ArcKit AI | Initial creation from `/arckit.stakeholders` command | PENDING | PENDING |

---

## Executive Summary

### Purpose
This document identifies key stakeholders for the UK Government API Aggregator platform, their underlying drivers (motivations, concerns, needs), how these drivers manifest into goals, and the measurable outcomes that will satisfy those goals. This analysis ensures stakeholder alignment and provides traceability from individual concerns to project success metrics.

### Key Findings
The platform sits at the intersection of multiple powerful stakeholder groups with largely aligned but occasionally competing interests. The strongest alignment exists around improving developer experience and reducing integration complexity across government. The primary tension is between the pace of delivery desired by the GDS leadership and the cautious approach required by department API owners who must protect their existing services. A secondary tension exists between the open-by-default transparency agenda and the security constraints imposed by NCSC and departmental information assurance teams.

### Critical Success Factors
- Secure buy-in from at least 5 major department API owners (HMRC, Companies House, DVLA, NHS Digital, Environment Agency) within the first 6 months
- Demonstrate measurable reduction in developer integration effort through a public beta with real consumers
- Pass GDS Service Standard assessment at Alpha and Beta gates
- Maintain zero security incidents involving upstream API credentials or government data
- Achieve and sustain platform availability independent of upstream API failures

### Stakeholder Alignment Score
**Overall Alignment**: MEDIUM

Most stakeholders share the vision of simplified government API access, but the path to get there surfaces legitimate conflicts around control, security, pace, and funding. Department API owners fear loss of autonomy. Security teams worry about a high-value target. Treasury wants evidence of value before committing. These conflicts are resolvable through a phased, trust-building approach but require active management.

---

## Stakeholder Identification

### Internal Stakeholders

| Stakeholder | Role/Department | Influence | Interest | Engagement Strategy |
|-------------|----------------|-----------|----------|---------------------|
| GDS Director of Technology | Executive Sponsor, GDS | HIGH | HIGH | Active involvement, decision authority, weekly steering |
| Senior Responsible Owner (SRO) | Programme Governance | HIGH | HIGH | Monthly programme board, exception reporting |
| GDS Service Owner | Product leadership | MEDIUM | HIGH | Day-to-day collaboration, sprint reviews |
| Enterprise Architect | Architecture governance | MEDIUM | HIGH | Architecture decisions, design reviews |
| GDS Delivery Manager | Programme delivery | MEDIUM | HIGH | Sprint planning, risk management |
| NCSC Advisor | Cyber security guidance | HIGH | MEDIUM | Security design reviews, threat modelling gates |
| Cabinet Office Digital Team | Cross-government digital strategy | HIGH | MEDIUM | Quarterly strategy alignment |
| Department API Owners (HMRC, CH, DVLA, etc.) | Upstream API providers | HIGH | HIGH | Co-design workshops, bilateral agreements |
| HM Treasury Spending Team | Budget approval | HIGH | LOW | Business case gates, spending reviews |
| Government Internal Audit Agency (GIAA) | Assurance | MEDIUM | LOW | Audit readiness, controls evidence |
| GDS Operations / WebOps | Live service operation | MEDIUM | HIGH | Transition planning, runbooks, on-call |
| GDS User Researchers | User needs evidence | LOW | HIGH | Research sessions, evidence gathering |

### External Stakeholders

| Stakeholder | Organization | Relationship | Influence | Interest |
|-------------|--------------|--------------|-----------|----------|
| Third-party developers | Private sector, civic tech | API consumers / beneficiaries | LOW | HIGH |
| Local authority digital teams | Local government | API consumers | LOW | HIGH |
| Other government departments (non-API-owning) | Cross-government | Potential consumers | LOW | MEDIUM |
| Information Commissioner's Office (ICO) | Regulator | Data protection oversight | HIGH | MEDIUM |
| National Audit Office (NAO) | Oversight | Value-for-money scrutiny | HIGH | LOW |
| Public Accounts Committee (PAC) | Parliamentary oversight | Accountability | HIGH | LOW |
| Open data community | Civil society | Advocacy, feedback | LOW | MEDIUM |
| Technology vendors / suppliers | Private sector | Platform delivery partners | MEDIUM | HIGH |

### Stakeholder Power-Interest Grid

```
                          INTEREST
              Low                         High
        ┌─────────────────────┬─────────────────────┐
        │                     │                     │
        │   KEEP SATISFIED    │   MANAGE CLOSELY    │
   High │                     │                     │
        │  • HM Treasury      │  • GDS Director     │
        │  • NAO              │  • SRO              │
        │  • PAC              │  • Dept API Owners   │
        │  • ICO              │  • Cabinet Office    │
 P      │  • NCSC Advisor     │  • NCSC Advisor*    │
 O      ├─────────────────────┼─────────────────────┤
 W      │                     │                     │
 E      │      MONITOR        │    KEEP INFORMED    │
 R      │                     │                     │
   Low  │  • GIAA             │  • 3rd-party devs   │
        │                     │  • Local authorities │
        │                     │  • GDS Operations    │
        │                     │  • Service Owner     │
        │                     │  • User Researchers  │
        │                     │  • Vendors/Suppliers │
        └─────────────────────┴─────────────────────┘

* NCSC spans both quadrants: high power on security decisions,
  high interest when threat model is active
```

| Stakeholder | Power | Interest | Quadrant | Engagement Strategy |
|-------------|-------|----------|----------|---------------------|
| GDS Director of Technology | HIGH | HIGH | Manage Closely | Weekly steering, decision escalation |
| Senior Responsible Owner (SRO) | HIGH | HIGH | Manage Closely | Monthly programme board |
| Department API Owners | HIGH | HIGH | Manage Closely | Bilateral co-design sessions, MoUs |
| Cabinet Office Digital Team | HIGH | MEDIUM | Manage Closely | Quarterly strategy reviews |
| NCSC Advisor | HIGH | MEDIUM | Keep Satisfied / Manage Closely | Security gate reviews, threat model workshops |
| HM Treasury | HIGH | LOW | Keep Satisfied | Business case submissions, spending review evidence |
| NAO | HIGH | LOW | Keep Satisfied | Audit trail, VfM evidence |
| PAC | HIGH | LOW | Keep Satisfied | Transparent reporting, ministerial briefings |
| ICO | HIGH | MEDIUM | Keep Satisfied | DPIA reviews, privacy by design evidence |
| GDS Service Owner | MEDIUM | HIGH | Keep Informed | Sprint reviews, roadmap input |
| GDS Operations / WebOps | MEDIUM | HIGH | Keep Informed | Release planning, ops handover |
| Technology vendors | MEDIUM | HIGH | Keep Informed | Contract reviews, delivery governance |
| Third-party developers | LOW | HIGH | Keep Informed | Public beta, developer community, feedback channels |
| Local authority digital teams | LOW | HIGH | Keep Informed | Demos, documentation, support channels |
| GDS User Researchers | LOW | HIGH | Keep Informed | Research findings integration |
| GIAA | MEDIUM | LOW | Monitor | Annual audit engagement |
| Open data community | LOW | MEDIUM | Monitor | Blog posts, open-source contributions |

---

## Stakeholder Drivers Analysis

### SD-1: GDS Director of Technology — Cross-Government Platform Delivery

**Stakeholder**: GDS Director of Technology (Executive Sponsor)

**Driver Category**: STRATEGIC

**Driver Statement**: Deliver a cross-government platform that demonstrates GDS's mandate to simplify and standardise government digital services, reinforcing GDS's relevance and leadership position within the cross-government technology landscape.

**Context & Background**:
GDS's role as the centre of government digital capability has been under ongoing scrutiny since its inception. The API aggregator represents a concrete, high-visibility deliverable that demonstrates the value of centralised platforms. The Director needs visible wins that justify GDS's budget allocation and mandate. The API landscape at api.gov.uk is fragmented — successfully unifying it would be a signature achievement.

**Driver Intensity**: CRITICAL

**Enablers**:
- Ministerial support for cross-government platforms
- Existing relationships with department CDOs/CTOs through the CTO Council
- api.gov.uk catalogue providing baseline discovery data
- GDS's existing platform delivery track record (GOV.UK Pay, Notify, Verify)

**Blockers**:
- Department resistance to centralised control of their APIs
- Budget constraints in current spending review period
- Competing GDS priorities (GOV.UK, One Login)
- Historical friction between GDS and departments over autonomy

**Related Stakeholders**: SRO, Cabinet Office, Department API Owners, HM Treasury

---

### SD-2: Department API Owners — Protect Service Integrity and Autonomy

**Stakeholder**: Department API Owners (HMRC, Companies House, DVLA, NHS Digital, Environment Agency, Ordnance Survey)

**Driver Category**: RISK / OPERATIONAL

**Driver Statement**: Ensure that the aggregation layer does not introduce instability, security vulnerabilities, or loss of control over their APIs, while potentially benefiting from increased developer adoption and reduced support burden.

**Context & Background**:
Each department has invested significant effort in building, securing, and operating their APIs. They manage their own rate limits, authentication, developer onboarding, and SLAs. An aggregation layer introduces a new intermediary that could: mask abuse patterns, bypass rate limits, create a single point of failure, or misrepresent their data. Department teams are protective of their services — they carry the operational risk if something goes wrong, regardless of whether the aggregator caused it. However, they also spend significant effort on developer support and onboarding that could be partially offloaded.

**Driver Intensity**: HIGH

**Enablers**:
- Clear MoU/agreement framework that preserves department control
- Transparent passthrough of rate limits and authentication
- Real-time visibility into traffic patterns via the aggregator
- Evidence from pilot that aggregator increases quality developer adoption

**Blockers**:
- Aggregator obscuring abuse patterns or masking problematic consumers
- Perception that GDS is taking over department services
- Additional operational dependency on a centrally-managed component
- Unclear liability model if aggregator causes upstream API issues

**Related Stakeholders**: GDS Director, NCSC, third-party developers

---

### SD-3: Third-Party Developers — Simplified Government API Integration

**Stakeholder**: Third-party developers (private sector, civic tech, GovTech startups)

**Driver Category**: CUSTOMER / OPERATIONAL

**Driver Statement**: Access government data and services through a single, well-documented, consistent interface rather than navigating dozens of separate developer portals, registration processes, authentication schemes, and data formats.

**Context & Background**:
Developers building applications that use government data currently face a fragmented landscape: each department has its own developer portal, registration process, API key management, authentication mechanism, rate limiting policy, data format, and error handling convention. Building an application that combines data from Companies House, HMRC, and DVLA requires integrating with three completely separate ecosystems. This friction suppresses innovation and limits the range of services built on government data.

**Driver Intensity**: HIGH

**Enablers**:
- Single developer portal with unified registration
- Consistent authentication across all aggregated APIs
- Normalised data formats and error responses
- Sandbox environment for testing without registration complexity
- Comprehensive, searchable API catalogue

**Blockers**:
- Platform not aggregating the specific APIs developers need
- Aggregator adding latency or reducing reliability compared to direct access
- Restrictive rate limits or usage policies on the aggregated layer
- Poor documentation or stale API catalogue

**Related Stakeholders**: GDS Service Owner, Department API Owners, local authorities

---

### SD-4: NCSC Advisor — Secure-by-Design Government Platform

**Stakeholder**: NCSC Cyber Security Advisor

**Driver Category**: COMPLIANCE / RISK

**Driver Statement**: Ensure the aggregation platform is designed and operated securely, does not create a high-value target that could be exploited to access multiple government APIs simultaneously, and complies with NCSC guidance for government platforms.

**Context & Background**:
The API aggregator, by design, concentrates access credentials and routing to multiple government APIs in a single platform. This makes it an attractive target for adversaries — compromising the aggregator could grant access to HMRC tax data, DVLA vehicle records, and NHS patient information simultaneously. NCSC must be confident that the platform's security architecture prevents credential leakage, enforces least privilege, implements defence in depth, and can detect and respond to compromise rapidly.

**Driver Intensity**: CRITICAL

**Enablers**:
- Early engagement in threat modelling and security architecture
- Dedicated security engineering resource on the team
- Adoption of NCSC Cloud Security Principles and CAF
- Regular penetration testing and red team exercises
- Credential isolation architecture (no single key accesses all upstream APIs)

**Blockers**:
- Insufficient security budget or expertise
- Pressure to ship quickly at the expense of security review cycles
- Upstream APIs with weak security postures that the aggregator inherits
- Unclear security responsibility boundaries between aggregator and upstream APIs

**Related Stakeholders**: Department API Owners, GDS Director, ICO

---

### SD-5: HM Treasury — Value for Money and Controlled Spending

**Stakeholder**: HM Treasury Spending Team

**Driver Category**: FINANCIAL

**Driver Statement**: Ensure the API aggregator programme demonstrates clear value for money, stays within approved spending limits, and generates measurable benefits that justify the investment against competing demands for government technology funding.

**Context & Background**:
Treasury scrutinises all significant technology programmes through spending controls. The aggregator must demonstrate that centralised investment produces benefits that exceed what departments could achieve individually. Treasury will benchmark against the "do nothing" counterfactual and the "departments invest individually" alternative. They expect a clear business case with quantified benefits, realistic cost estimates, and phased delivery that allows stop/go decisions.

**Driver Intensity**: HIGH

**Enablers**:
- Strong business case with quantified benefits (developer time savings, reduced duplication)
- Phased delivery model with clear stop/go decision points
- Evidence of department co-investment or contribution
- Comparison with international equivalents (data.gov APIs, EU interoperability)

**Blockers**:
- Inability to quantify benefits in financial terms
- Cost overruns or scope creep
- Departments refusing to participate (undermining the value proposition)
- Competing programmes with stronger business cases

**Related Stakeholders**: NAO, PAC, GDS Director, SRO

---

### SD-6: Senior Responsible Owner (SRO) — Successful Programme Delivery

**Stakeholder**: Senior Responsible Owner

**Driver Category**: PERSONAL / RISK

**Driver Statement**: Deliver the programme successfully within agreed parameters (scope, time, cost, quality) while managing political risks and maintaining ministerial confidence. Avoid the programme becoming a high-profile government IT failure.

**Context & Background**:
The SRO carries personal accountability for the programme's success. Government IT programmes have a well-documented history of high-profile failures (Universal Credit, NHS NPfIT, Verify). The SRO must navigate between ambitious delivery expectations and prudent risk management. Their professional reputation is directly tied to the outcome. They need early warning of problems, credible delivery plans, and clear escalation routes.

**Driver Intensity**: CRITICAL

**Enablers**:
- Experienced delivery team with government platform track record
- Agile delivery methodology with frequent demonstrations of progress
- Clear governance structure with escalation routes
- Independent assurance reviews at key milestones
- Realistic planning that builds in contingency

**Blockers**:
- Overly ambitious timelines set without team input
- Scope creep driven by political pressure to add departments quickly
- Key person dependencies on specialist skills
- Department non-cooperation creating delivery blockers

**Related Stakeholders**: GDS Director, HM Treasury, NAO, Delivery Manager

---

### SD-7: ICO — Data Protection Compliance

**Stakeholder**: Information Commissioner's Office

**Driver Category**: COMPLIANCE

**Driver Statement**: Ensure the platform processes personal data lawfully, transparently, and securely in compliance with UK GDPR and the Data Protection Act 2018, with appropriate DPIAs and clear data controller/processor relationships.

**Context & Background**:
The aggregator will route requests that may contain or return personal data (DVLA vehicle keeper information, HMRC tax data, NHS patient data). The ICO needs clarity on: who is the data controller vs processor for aggregated requests, what lawful basis applies, how data minimisation is enforced, and how data subjects can exercise their rights when data flows through an intermediary. The novel architecture of an aggregation layer raises questions that don't have established precedent in government.

**Driver Intensity**: HIGH

**Enablers**:
- Early DPIA engagement before processing begins
- Clear data controller/processor agreements with each department
- Privacy by design embedded in architecture (data minimisation, no unnecessary caching of personal data)
- Transparent privacy notice explaining the aggregator's role

**Blockers**:
- Unclear data controller responsibilities in aggregated request scenarios
- Caching of personal data without appropriate lawful basis
- Inability to fulfil data subject access requests across aggregated APIs
- Departments with inconsistent privacy practices

**Related Stakeholders**: Department API Owners, NCSC, GDS Service Owner

---

### SD-8: GDS Operations / WebOps — Operable and Sustainable Platform

**Stakeholder**: GDS Operations / WebOps Team

**Driver Category**: OPERATIONAL

**Driver Statement**: Receive a platform that is operable, observable, well-documented, and sustainable to run at scale without requiring constant development team intervention or heroic operational effort.

**Context & Background**:
GDS WebOps already operates GOV.UK, GOV.UK Pay, GOV.UK Notify, and other platforms. Each new platform adds to their operational burden. They need the aggregator to be built with operational excellence from the start — comprehensive monitoring, automated recovery, clear runbooks, and manageable on-call burden. They have been burned by platforms handed over without adequate operational documentation or observability.

**Driver Intensity**: HIGH

**Enablers**:
- Observability built in from day one (structured logs, metrics, distributed tracing)
- Automated deployment and rollback
- Comprehensive runbooks for common failure scenarios
- Clear SLO/SLI definitions before go-live
- Gradual operational handover with embedded ops engineer during beta

**Blockers**:
- Platform delivered without adequate monitoring or documentation
- Complex operational procedures requiring deep platform knowledge
- Upstream API failures generating excessive noise in alerting
- Insufficient staffing to cover additional on-call rotation

**Related Stakeholders**: GDS Delivery Manager, Enterprise Architect

---

### SD-9: GDS User Researchers — Evidence-Based Design

**Stakeholder**: GDS User Researchers

**Driver Category**: CUSTOMER / COMPLIANCE

**Driver Statement**: Ensure the platform and developer portal are designed based on validated user needs, not assumptions, and that evidence is maintained to satisfy GDS Service Standard assessment requirements.

**Context & Background**:
GDS Service Standard Point 1 requires understanding users and their needs. For the API aggregator, "users" are primarily developers — a group with specific needs around documentation quality, SDK availability, sandbox environments, and error message clarity. User researchers need access to real developers, time to conduct research, and influence over design decisions. The service assessment will specifically examine whether user research has driven the design.

**Driver Intensity**: MEDIUM

**Enablers**:
- Access to developer communities for research recruitment
- Regular research sessions built into sprint cadence
- Design decisions documented with user research evidence
- Usability testing of developer portal and API documentation

**Blockers**:
- Difficulty recruiting developer participants for research
- Pressure to ship without waiting for research findings
- Research treated as checkbox exercise rather than input to design
- Limited budget for incentives and recruitment

**Related Stakeholders**: GDS Service Owner, third-party developers, GDS assessors

---

### SD-10: Local Authority Digital Teams — Affordable Access to Government Data

**Stakeholder**: Local authority digital teams

**Driver Category**: OPERATIONAL / FINANCIAL

**Driver Statement**: Access government APIs without the overhead of navigating multiple department registration processes, managing multiple sets of credentials, or building custom integrations for each data source needed.

**Context & Background**:
Local authorities build digital services that depend on central government data — council tax relies on property data, planning applications require environmental data, social care needs benefit status information. Most local authorities have small digital teams (often 2-5 developers) who cannot afford the overhead of integrating with dozens of separate APIs. A unified aggregation layer would dramatically reduce the barrier to building cross-government digital services at the local level.

**Driver Intensity**: MEDIUM

**Enablers**:
- Free or low-cost access tier for public sector consumers
- Pre-built integration patterns for common local authority use cases
- Sandbox environment for testing without formal registration
- Community forum for sharing integration patterns

**Blockers**:
- Platform not aggregating the APIs local authorities need most
- Complex onboarding process despite aggregation
- Rate limits too restrictive for local authority batch processing needs
- Lack of awareness that the platform exists

**Related Stakeholders**: Third-party developers, Department API Owners, Cabinet Office

---

## Driver-to-Goal Mapping

### Goal G-1: Unified Developer Onboarding

**Derived From Drivers**: SD-1, SD-3, SD-10

**Goal Owner**: GDS Service Owner

**Goal Statement**: Reduce the average time for a developer to discover, register for, and make their first successful API call from 5+ days (current multi-department process) to under 1 hour through a single unified portal by end of Beta phase.

**Why This Matters**: This directly addresses the fragmentation pain that developers experience (SD-3, SD-10) and provides the visible, measurable win that GDS leadership needs (SD-1). If developers cannot onboard quickly, the platform fails its core value proposition.

**Success Metrics**:
- **Primary Metric**: Time from portal visit to first successful API call
- **Secondary Metrics**:
  - Developer registration completion rate
  - Number of APIs accessible through single registration
  - Developer satisfaction score (post-onboarding survey)

**Baseline**: 5-10 working days across multiple department portals (estimated from developer interviews)

**Target**: Under 1 hour for first API call, under 5 minutes for registration

**Measurement Method**: Instrumented portal funnel analytics tracking each step from landing page to first successful API response

**Dependencies**:
- At least 5 department APIs integrated into the platform
- Developer portal built and tested with real users
- Unified authentication mechanism operational

**Risks to Achievement**:
- Departments requiring separate registration even through the aggregator
- Authentication complexity preventing streamlined flow
- API key provisioning bottlenecks

---

### Goal G-2: Cross-Department API Aggregation Coverage

**Derived From Drivers**: SD-1, SD-2, SD-3

**Goal Owner**: GDS Director of Technology

**Goal Statement**: Aggregate APIs from at least 8 government departments (covering the top 10 most-used government APIs by developer request volume) within 18 months of programme start.

**Why This Matters**: The platform's value is directly proportional to the breadth of APIs available. Without critical mass, developers will continue using direct department APIs (SD-3 unsatisfied). GDS needs this coverage to demonstrate cross-government impact (SD-1). Departments must see peer participation to reduce resistance (SD-2).

**Success Metrics**:
- **Primary Metric**: Number of department APIs accessible through the aggregator
- **Secondary Metrics**:
  - Percentage of api.gov.uk catalogue covered
  - Number of unique API endpoints available
  - API availability through aggregator vs direct access

**Baseline**: 0 departments integrated (new platform)

**Target**: 8+ departments, covering top 10 most-used APIs

**Measurement Method**: Platform catalogue metrics, monthly coverage reports

**Dependencies**:
- MoU agreements signed with each department
- Technical integration with each department's API infrastructure
- Department API documentation sufficient for adapter development

**Risks to Achievement**:
- Key departments refusing to participate
- Technical incompatibility with legacy department API infrastructure
- Resource constraints limiting parallel adapter development
- Department API changes breaking integrations during development

---

### Goal G-3: Platform Security Assurance

**Derived From Drivers**: SD-4, SD-2, SD-6

**Goal Owner**: NCSC Advisor (with Enterprise Architect)

**Goal Statement**: Achieve NCSC security review approval with no critical or high findings unresolved, maintain zero security incidents involving credential leakage or unauthorised data access, and pass independent penetration testing before public beta.

**Why This Matters**: Security is the non-negotiable foundation. A security incident involving the aggregator could compromise multiple government APIs simultaneously (SD-4), undermine department trust (SD-2), and create a high-profile failure (SD-6). The platform cannot go live without robust security assurance.

**Success Metrics**:
- **Primary Metric**: Zero critical/high security findings unresolved at each gate
- **Secondary Metrics**:
  - Penetration test pass rate
  - Mean time to remediate vulnerabilities
  - Security incident count (target: zero)
  - Credential rotation compliance rate

**Baseline**: N/A (new platform)

**Target**: Clean NCSC review, zero incidents, pen test pass

**Measurement Method**: NCSC review reports, penetration test reports, security incident tracking, vulnerability management dashboard

**Dependencies**:
- Threat model completed and reviewed
- Security architecture approved before development
- Dedicated security engineering resource
- Penetration testing budget and supplier

**Risks to Achievement**:
- Insufficient security expertise on team
- Pressure to bypass security gates for delivery pace
- Upstream API security weaknesses inherited by aggregator
- Novel attack vectors in aggregation architecture not covered by standard testing

---

### Goal G-4: Demonstrable Value for Money

**Derived From Drivers**: SD-5, SD-1, SD-6

**Goal Owner**: SRO

**Goal Statement**: Demonstrate a positive cost-benefit ratio within 2 years of launch, with quantified benefits (developer time savings, reduced department support costs, new services enabled) exceeding programme costs by at least 1.5:1.

**Why This Matters**: Treasury will not continue funding without evidence of value (SD-5). The SRO's credibility depends on delivering benefits, not just outputs (SD-6). GDS needs the business case to justify the platform's existence alongside other priorities (SD-1).

**Success Metrics**:
- **Primary Metric**: Cost-benefit ratio (benefits delivered / programme costs)
- **Secondary Metrics**:
  - Developer time savings (hours saved per integration)
  - Department support cost reduction
  - Number of new services/applications enabled by the platform
  - Cost per API transaction through aggregator vs direct

**Baseline**: Current cost for developers to integrate with 5 government APIs: estimated £50,000-£100,000 per integration project

**Target**: 1.5:1 benefit-cost ratio by Year 2; integration cost reduction of 60%+

**Measurement Method**: Benefits realisation tracking framework, developer survey data, department support ticket analysis

**Dependencies**:
- Sufficient platform adoption to generate measurable benefits
- Departments providing baseline data on current support costs
- Developer community providing feedback on time savings

**Risks to Achievement**:
- Low adoption undermining benefits case
- Benefits difficult to attribute directly to the aggregator
- Programme costs exceeding estimates
- Departments not sharing baseline cost data

---

### Goal G-5: GDS Service Standard Compliance

**Derived From Drivers**: SD-9, SD-1, SD-6

**Goal Owner**: GDS Service Owner

**Goal Statement**: Pass GDS Service Standard assessment at Alpha and Beta gates, with documented evidence against all 14 points, particular strength in Points 1 (user needs), 5 (agile), 9 (secure), and 12 (technology).

**Why This Matters**: Service Standard compliance is mandatory for government services (SD-9). Failing assessment would be embarrassing for GDS — the organisation that created the standard (SD-1). The SRO cannot take a non-compliant service to public beta (SD-6).

**Success Metrics**:
- **Primary Metric**: Service Standard assessment outcome (Pass/Not Pass per point)
- **Secondary Metrics**:
  - User research sessions conducted per sprint
  - Accessibility compliance score (WCAG 2.2 AA)
  - Open source code published
  - Performance against web performance budgets

**Baseline**: N/A (new service)

**Target**: Pass at Alpha and Beta assessments

**Measurement Method**: GDS assessment panel reports, internal readiness reviews

**Dependencies**:
- User research programme resourced and active
- Accessibility testing integrated into development workflow
- Open source repository maintained
- Performance monitoring in place

**Risks to Achievement**:
- Insufficient user research evidence
- Accessibility issues discovered late
- Assessment panel concerns about cross-department governance model
- Technical debt accumulation reducing confidence in sustainability

---

### Goal G-6: Operational Sustainability

**Derived From Drivers**: SD-8, SD-2, SD-6

**Goal Owner**: GDS Operations Lead

**Goal Statement**: Achieve operational readiness with documented runbooks, automated recovery, defined SLOs, and manageable on-call burden (no more than 2 out-of-hours pages per week on average) before transitioning from beta to live.

**Why This Matters**: Operations teams must be confident they can run the platform sustainably (SD-8). Departments need assurance that the aggregator will be reliably operated (SD-2). The SRO cannot approve go-live without operational readiness (SD-6).

**Success Metrics**:
- **Primary Metric**: Operational readiness score (checklist completion percentage)
- **Secondary Metrics**:
  - Mean time to detect (MTTD) incidents
  - Mean time to recover (MTTR)
  - Out-of-hours page frequency
  - Runbook coverage (percentage of known failure modes documented)

**Baseline**: N/A (new platform)

**Target**: 100% operational readiness checklist, MTTR < 30 minutes for P1, < 2 OOH pages/week average

**Measurement Method**: Operational readiness review, incident tracking, on-call reports

**Dependencies**:
- Observability instrumented across all components
- Automated deployment and rollback tested
- On-call rotation staffed
- Upstream API health monitoring operational

**Risks to Achievement**:
- Platform handed to ops without adequate documentation
- Upstream API instability creating excessive operational noise
- Insufficient ops staffing for additional platform
- Complex architecture requiring specialist knowledge for troubleshooting

---

### Goal G-7: Data Protection Compliance

**Derived From Drivers**: SD-7, SD-4

**Goal Owner**: Data Protection Officer (DPO)

**Goal Statement**: Complete and publish DPIAs for all personal data processing activities before public beta, establish clear data controller/processor agreements with all participating departments, and achieve ICO confirmation that the processing model is compliant.

**Why This Matters**: The aggregator routes potentially sensitive personal data between consumers and government APIs. Without clear data protection compliance, the platform cannot process personal data lawfully (SD-7), and security architecture cannot be finalised without understanding data flows (SD-4).

**Success Metrics**:
- **Primary Metric**: DPIA completion and ICO engagement status
- **Secondary Metrics**:
  - Data controller/processor agreements signed per department
  - Privacy notice published and reviewed
  - Data subject rights fulfilment process tested

**Baseline**: N/A (new platform)

**Target**: DPIAs complete, agreements signed with all participating departments, ICO engagement completed before public beta

**Measurement Method**: DPIA register, agreement tracking, ICO correspondence log

**Dependencies**:
- Data flow mapping completed for each integrated API
- Legal team engaged on controller/processor analysis
- Departments agreeable to data sharing frameworks

**Risks to Achievement**:
- Novel aggregation model creates regulatory uncertainty
- Departments with different interpretations of controller/processor roles
- ICO requiring changes that impact architecture
- Data subject rights fulfilment complexity across aggregated APIs

---

## Goal-to-Outcome Mapping

### Outcome O-1: Developer Ecosystem Growth

**Supported Goals**: G-1, G-2, G-5

**Outcome Statement**: Build a thriving developer ecosystem with 500+ registered developers and 50+ applications in production within 12 months of public beta launch.

**Measurement Details**:
- **KPI**: Registered developers, active applications, API call volume
- **Current Value**: 0 (new platform)
- **Target Value**: 500 registered developers, 50 production applications, 1M+ API calls/month
- **Measurement Frequency**: Monthly
- **Data Source**: Platform analytics, developer portal registration data
- **Report Owner**: GDS Service Owner

**Business Value**:
- **Financial Impact**: Estimated £5M+ in developer time savings across ecosystem annually (based on average integration cost reduction)
- **Strategic Impact**: Positions UK Government as leader in API-driven government services
- **Operational Impact**: Increased reuse of government data, reduced duplicate data collection
- **Customer Impact**: Better digital services for citizens built on reliable government data

**Timeline**:
- **Phase 1 (Months 1-3)**: Private beta with 20 invited developers, 3 departments
- **Phase 2 (Months 4-6)**: Public beta, target 100 developers, 5 departments
- **Phase 3 (Months 7-12)**: Live service, target 500 developers, 8 departments
- **Sustainment (Year 2+)**: 1000+ developers, self-sustaining growth

**Stakeholder Benefits**:
- **GDS Director**: Visible cross-government impact, quantifiable platform adoption
- **Third-party developers**: Dramatically reduced integration effort and cost
- **Department API Owners**: Increased quality adoption of their APIs, reduced support burden
- **Local authorities**: Affordable access to government data for local services

**Leading Indicators**:
- Developer registration rate per week
- Time to first API call trending downward
- Developer satisfaction survey scores
- API documentation page views

**Lagging Indicators**:
- Number of production applications using the platform
- Total API call volume
- Developer retention rate (monthly active developers)

---

### Outcome O-2: Secure and Trusted Platform

**Supported Goals**: G-3, G-7

**Outcome Statement**: Maintain zero security incidents and full data protection compliance, establishing the aggregator as a trusted intermediary that departments and developers rely on.

**Measurement Details**:
- **KPI**: Security incident count, vulnerability remediation time, compliance audit results
- **Current Value**: N/A
- **Target Value**: Zero security incidents, all critical vulnerabilities remediated within 48 hours, clean compliance audits
- **Measurement Frequency**: Continuous (incidents), Monthly (vulnerability review), Quarterly (compliance)
- **Data Source**: Security monitoring, vulnerability scanner, audit reports
- **Report Owner**: NCSC Advisor / Security Lead

**Business Value**:
- **Financial Impact**: Avoidance of breach costs (estimated £1M-£10M per significant government data breach)
- **Strategic Impact**: Trust foundation enabling future government platform expansion
- **Operational Impact**: Departments confident in aggregator's security posture
- **Customer Impact**: Citizens' data protected in transit through the aggregator

**Timeline**:
- **Phase 1 (Months 1-3)**: Threat model complete, security architecture approved
- **Phase 2 (Months 4-6)**: Penetration test passed, DPIA complete
- **Phase 3 (Months 7-12)**: Live security monitoring operational, incident response tested
- **Sustainment (Year 2+)**: Continuous assurance, annual pen tests, ongoing compliance

**Stakeholder Benefits**:
- **NCSC**: Confidence in government platform security
- **ICO**: Compliant data processing model
- **Department API Owners**: Trust that their APIs are accessed securely
- **SRO**: Avoidance of high-profile security failure

**Leading Indicators**:
- Vulnerability scan results trending clean
- Security review gate pass rate
- Mean time to patch critical vulnerabilities

**Lagging Indicators**:
- Zero security incidents sustained over time
- Clean annual penetration test results
- ICO no concerns/enforcement actions

---

### Outcome O-3: Demonstrated Return on Investment

**Supported Goals**: G-4, G-2

**Outcome Statement**: Achieve measurable cost-benefit ratio of 1.5:1 or better within 24 months, with benefits independently verified by internal audit.

**Measurement Details**:
- **KPI**: Benefits realised (£), programme costs (£), cost-benefit ratio
- **Current Value**: 0 benefits / programme investment TBC
- **Target Value**: 1.5:1 cost-benefit ratio
- **Measurement Frequency**: Quarterly
- **Data Source**: Benefits realisation tracker, finance reports, developer surveys
- **Report Owner**: SRO

**Business Value**:
- **Financial Impact**: Net positive return on government investment
- **Strategic Impact**: Justification for continued and expanded investment in government platforms
- **Operational Impact**: Reduced duplication of integration effort across government
- **Customer Impact**: More services available to citizens at lower cost

**Timeline**:
- **Phase 1 (Months 1-6)**: Costs incurred, early adoption metrics tracked
- **Phase 2 (Months 7-12)**: First benefits measurable (developer time savings)
- **Phase 3 (Months 13-24)**: Benefits accumulate, ratio target achieved
- **Sustainment (Year 3+)**: Benefits compound as adoption grows, marginal cost of new APIs decreases

**Stakeholder Benefits**:
- **HM Treasury**: Evidence of value for money in government technology spending
- **SRO**: Programme success demonstrated quantitatively
- **GDS Director**: Business case for continued platform investment
- **NAO**: Clear audit trail of benefits realisation

**Leading Indicators**:
- Developer adoption rate
- Number of integrations replacing direct department API connections
- Department support ticket volume reduction

**Lagging Indicators**:
- Independently verified cost-benefit ratio
- Total quantified benefits (£)
- Number of new citizen-facing services enabled

---

### Outcome O-4: Operationally Sustainable Service

**Supported Goals**: G-5, G-6

**Outcome Statement**: Platform operates as a sustainable live service with 99.9%+ availability, passing annual GDS service assessment reviews, and maintained by a right-sized operations team.

**Measurement Details**:
- **KPI**: Platform availability, incident frequency, operational cost per API call
- **Current Value**: N/A
- **Target Value**: 99.9% availability, < 2 P1 incidents per quarter, declining cost per transaction
- **Measurement Frequency**: Real-time (availability), Monthly (incidents), Quarterly (cost)
- **Data Source**: Platform monitoring, incident management system, finance reports
- **Report Owner**: GDS Operations Lead

**Business Value**:
- **Financial Impact**: Predictable, declining operational cost per transaction
- **Strategic Impact**: Reliable foundation for cross-government digital services
- **Operational Impact**: Manageable operational burden, sustainable on-call
- **Customer Impact**: Developers and their end-users experience reliable service

**Timeline**:
- **Phase 1 (Months 1-6)**: Operational tooling built, beta stability established
- **Phase 2 (Months 7-12)**: Live service with full monitoring, initial SLOs met
- **Phase 3 (Year 2)**: Operational maturity, toil reduction, automated remediation
- **Sustainment (Year 3+)**: Self-sustaining operations with continuous improvement

**Stakeholder Benefits**:
- **GDS Operations**: Manageable platform with clear runbooks and automation
- **Department API Owners**: Reliable intermediary that doesn't add instability
- **Developers**: Consistent service they can depend on for production applications
- **SRO**: Sustainable service that doesn't require ongoing crisis management

**Leading Indicators**:
- Runbook coverage percentage
- Automated recovery success rate
- On-call page volume trend

**Lagging Indicators**:
- 99.9%+ availability sustained quarterly
- GDS live service assessment pass
- Operations team satisfaction score

---

## Complete Traceability Matrix

### Stakeholder → Driver → Goal → Outcome

| Stakeholder | Driver ID | Driver Summary | Goal ID | Goal Summary | Outcome ID | Outcome Summary |
|-------------|-----------|----------------|---------|--------------|------------|-----------------|
| GDS Director | SD-1 | Cross-government platform delivery | G-1 | Unified developer onboarding | O-1 | Developer ecosystem growth |
| GDS Director | SD-1 | Cross-government platform delivery | G-2 | API aggregation coverage | O-1 | Developer ecosystem growth |
| GDS Director | SD-1 | Cross-government platform delivery | G-5 | Service Standard compliance | O-4 | Sustainable service |
| Dept API Owners | SD-2 | Protect service integrity | G-2 | API aggregation coverage | O-1 | Developer ecosystem growth |
| Dept API Owners | SD-2 | Protect service integrity | G-3 | Platform security assurance | O-2 | Secure platform |
| Dept API Owners | SD-2 | Protect service integrity | G-6 | Operational sustainability | O-4 | Sustainable service |
| Third-party devs | SD-3 | Simplified integration | G-1 | Unified developer onboarding | O-1 | Developer ecosystem growth |
| Third-party devs | SD-3 | Simplified integration | G-2 | API aggregation coverage | O-1 | Developer ecosystem growth |
| NCSC Advisor | SD-4 | Secure-by-design platform | G-3 | Platform security assurance | O-2 | Secure platform |
| NCSC Advisor | SD-4 | Secure-by-design platform | G-7 | Data protection compliance | O-2 | Secure platform |
| HM Treasury | SD-5 | Value for money | G-4 | Demonstrable VfM | O-3 | Return on investment |
| SRO | SD-6 | Successful programme delivery | G-4 | Demonstrable VfM | O-3 | Return on investment |
| SRO | SD-6 | Successful programme delivery | G-5 | Service Standard compliance | O-4 | Sustainable service |
| SRO | SD-6 | Successful programme delivery | G-6 | Operational sustainability | O-4 | Sustainable service |
| ICO | SD-7 | Data protection compliance | G-7 | Data protection compliance | O-2 | Secure platform |
| GDS Operations | SD-8 | Operable platform | G-6 | Operational sustainability | O-4 | Sustainable service |
| User Researchers | SD-9 | Evidence-based design | G-1 | Unified developer onboarding | O-1 | Developer ecosystem growth |
| User Researchers | SD-9 | Evidence-based design | G-5 | Service Standard compliance | O-4 | Sustainable service |
| Local authorities | SD-10 | Affordable API access | G-1 | Unified developer onboarding | O-1 | Developer ecosystem growth |
| Local authorities | SD-10 | Affordable API access | G-2 | API aggregation coverage | O-1 | Developer ecosystem growth |

### Conflict Analysis

**Competing Drivers**:

- **Conflict 1**: GDS Director (SD-1) wants rapid cross-government coverage to demonstrate impact, but Department API Owners (SD-2) want careful, controlled integration that preserves their autonomy and doesn't rush security.
  - **Resolution Strategy**: Phased onboarding starting with willing "early adopter" departments. Begin with departments that already have mature, well-documented APIs (Companies House, Environment Agency). Use early successes to build trust and demonstrate the model before approaching more cautious departments (HMRC, NHS Digital). Set clear MoU templates that preserve department control over rate limits, authentication upgrades, and API retirement decisions.

- **Conflict 2**: HM Treasury (SD-5) wants quantified value before committing full funding, but meaningful benefits require critical mass of department APIs which requires the full funding to build.
  - **Resolution Strategy**: Phased business case with stage-gate funding. Alpha funding to prove the concept with 2-3 departments. Beta funding contingent on demonstrated developer adoption and department willingness. Full funding only after measurable benefits from beta. Include "do minimum" and "do more" options at each gate.

- **Conflict 3**: NCSC (SD-4) requires thorough security review cycles, but delivery pressure (SD-1, SD-6) pushes for faster deployment.
  - **Resolution Strategy**: Embed security from sprint 1, not as a gate at the end. Engage NCSC advisor as a permanent team member, not an external reviewer. Conduct threat modelling early and iterate. Build security testing into CI/CD pipeline so every deployment is security-tested. This front-loads security effort but avoids late-stage blocking reviews.

- **Conflict 4**: Third-party developers (SD-3) want maximum API access with minimal friction, but ICO (SD-7) requires careful controls on personal data processing.
  - **Resolution Strategy**: Tiered access model. Open data and non-personal APIs available with lightweight registration. APIs returning personal data require enhanced verification, terms of use, and purpose declaration. This satisfies developer needs for most APIs while maintaining ICO compliance for sensitive data.

**Synergies**:

- **Synergy 1**: GDS Director's platform delivery goal (SD-1) aligns with third-party developers' integration needs (SD-3) and local authorities' access needs (SD-10) — all are served by the same platform capability. Building the platform creates value for all three simultaneously.

- **Synergy 2**: NCSC's security requirements (SD-4) align with Department API Owners' service integrity concerns (SD-2) — a well-secured aggregator actually improves the security posture for departments by providing consistent authentication, rate limiting, and abuse detection.

- **Synergy 3**: GDS Operations' sustainability requirements (SD-8) align with the SRO's risk management needs (SD-6) — a well-operated platform reduces the risk of embarrassing failures that threaten the programme.

- **Synergy 4**: User Researchers' evidence-based design (SD-9) supports Service Standard compliance (G-5) which supports GDS Director's credibility goal (SD-1) — investing in user research serves multiple stakeholders simultaneously.

---

## Communication & Engagement Plan

### GDS Director of Technology

**Primary Message**: The API aggregator is progressing on track to deliver cross-government impact, with [X] departments onboarded and [Y] developers registered. Key risks are being actively managed.

**Key Talking Points**:
- Platform adoption metrics and growth trajectory
- Department onboarding pipeline and any blockers
- Strategic alignment with cross-government digital strategy
- Comparison with international equivalents

**Communication Frequency**: Weekly

**Preferred Channel**: 30-minute weekly steering meeting + written dashboard

**Success Story**: "The API aggregator now serves 500 developers accessing 8 department APIs — the first cross-government API platform to reach this scale."

---

### Department API Owners

**Primary Message**: The aggregator increases quality developer adoption of your APIs while preserving your control over authentication, rate limits, and API lifecycle. We are a channel, not a replacement.

**Key Talking Points**:
- Developer adoption metrics specifically for their APIs
- Transparency of traffic patterns and consumer behaviour
- Their continued control over API access policies
- Reduction in their developer support burden

**Communication Frequency**: Bi-weekly during integration, monthly thereafter

**Preferred Channel**: Bilateral technical meetings + monthly metrics report

**Success Story**: "Since integration with the aggregator, Companies House API adoption increased 40% while developer support tickets decreased 25%."

---

### HM Treasury

**Primary Message**: The programme is delivering measurable benefits on budget, with clear evidence of developer time savings and department support cost reduction. Phased delivery ensures stop/go control.

**Key Talking Points**:
- Benefits realisation data (quantified in £)
- Programme spend vs budget
- Adoption metrics demonstrating demand
- Comparison with counterfactual (cost of departments doing this individually)

**Communication Frequency**: Quarterly

**Preferred Channel**: Written benefits realisation report aligned with spending review cycles

**Success Story**: "The platform has delivered £3M in estimated developer time savings in its first year against a programme cost of £2M."

---

### Third-Party Developers

**Primary Message**: One registration, one API key, access to government data from multiple departments. Better documentation, consistent error handling, sandbox environments.

**Key Talking Points**:
- New APIs available on the platform
- Developer portal improvements
- Known issues and workarounds
- Roadmap and upcoming features

**Communication Frequency**: Monthly newsletter, real-time status page

**Preferred Channel**: Developer blog, email newsletter, GitHub discussions, status page

**Success Story**: "A GovTech startup built a cross-department business intelligence tool in 2 weeks that would have taken 3 months integrating directly."

---

### NCSC Advisor

**Primary Message**: Security is embedded in every sprint, threat model is current, and all identified risks have mitigations in place or documented exceptions.

**Key Talking Points**:
- Threat model updates and new attack vectors considered
- Penetration test results and remediation status
- Security architecture changes and rationale
- Incident response readiness

**Communication Frequency**: Bi-weekly during development, monthly in live service

**Preferred Channel**: Security review meetings, written security assessment reports

**Success Story**: "Independent penetration testing found no critical or high vulnerabilities. Credential isolation architecture successfully prevents cross-department credential exposure."

---

## Change Impact Assessment

### Impact on Stakeholders

| Stakeholder | Current State | Future State | Change Magnitude | Resistance Risk | Mitigation Strategy |
|-------------|---------------|--------------|------------------|-----------------|---------------------|
| Dept API Owners | Full control of developer onboarding and API access | Share access channel with aggregator while retaining policy control | MEDIUM | HIGH | Co-design workshops, MoU preserving control, transparent traffic visibility |
| Third-party devs | Navigate multiple portals, registrations, auth schemes | Single portal, unified access, consistent experience | HIGH (positive) | LOW | Early beta invitations, feedback channels, responsive iteration |
| GDS Operations | Operating existing GDS platforms | Additional platform to operate and support | MEDIUM | MEDIUM | Early ops engagement, embedded ops engineer, comprehensive runbooks |
| Local authorities | Build custom integrations per department | Use aggregated APIs with simpler onboarding | HIGH (positive) | LOW | Tailored onboarding guides, local authority use case examples |
| GDS User Researchers | Research for existing GDS services | Additional service requiring developer-focused research | LOW | LOW | Clear research brief, access to developer communities |

### Change Readiness

**Champions** (Enthusiastic supporters):
- **Third-party developers** — Direct beneficiaries, vocal advocates for simplified government API access
- **GDS Service Owner** — Product leadership driving the vision
- **Local authority digital teams** — Underserved by current fragmented approach
- **Companies House / Environment Agency** — Historically open to cross-government collaboration

**Fence-sitters** (Neutral, need convincing):
- **GDS Operations** — Supportive in principle but need confidence in operational readiness before committing
- **HM Treasury** — Need evidence of value, open to phased approach
- **Cabinet Office Digital Team** — Supportive of strategy, need to see execution
- **Ordnance Survey** — Commercially operated APIs, need to understand revenue impact

**Resisters** (Opposed or skeptical):
- **HMRC API team** — Highly protective of their API estate due to sensitivity of tax data, concerned about credential security — Strategy: Start with low-sensitivity HMRC APIs, demonstrate security architecture, build trust gradually
- **NHS Digital** — Patient data sensitivity creates high barriers, separate regulatory regime (NHS specific IG requirements) — Strategy: Defer NHS API integration to later phase, engage early on architecture to address concerns
- **Some department CTOs** — View aggregator as GDS overreach into department territory — Strategy: Position as opt-in channel that increases department API adoption, not a replacement for direct access

---

## Risk Register (Stakeholder-Related)

### Risk R-1: Department Non-Participation

**Related Stakeholders**: Department API Owners, GDS Director, HM Treasury

**Risk Description**: Key departments refuse to participate or delay integration indefinitely, preventing the platform from reaching critical mass needed to demonstrate value.

**Impact on Goals**: G-2 (coverage), G-4 (VfM), O-1 (ecosystem growth), O-3 (ROI)

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Start with willing departments, demonstrate value through early adopters, build peer pressure. Secure ministerial-level support for cross-government participation. Offer departments tangible benefits (adoption metrics, reduced support burden, usage analytics).

**Contingency Plan**: If fewer than 5 departments participate by Month 12, reduce scope to "API catalogue and documentation aggregation" (lower value but still useful) while continuing to pursue full integration.

---

### Risk R-2: Security Incident Destroys Trust

**Related Stakeholders**: NCSC, Department API Owners, SRO, ICO

**Risk Description**: A security breach or credential leakage incident undermines department trust and public confidence, potentially causing participating departments to withdraw.

**Impact on Goals**: G-3 (security), G-2 (coverage), O-2 (trust)

**Probability**: LOW

**Impact**: CRITICAL

**Mitigation Strategy**: Defence in depth architecture, credential isolation (no single credential accesses all upstream APIs), continuous security monitoring, regular penetration testing, embedded security engineer, NCSC advisory relationship.

**Contingency Plan**: Pre-prepared incident response plan, department notification procedures, transparent public communication, independent security review, remediation plan with verifiable evidence before service restoration.

---

### Risk R-3: Programme Classified as Failing

**Related Stakeholders**: SRO, GDS Director, HM Treasury, NAO, PAC

**Risk Description**: Programme falls behind schedule or over budget, triggering IPA review or NAO investigation, creating negative political attention.

**Impact on Goals**: G-4 (VfM), G-5 (Service Standard), G-6 (sustainability)

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Agile delivery with frequent demonstrations of working software. Phased delivery with clear stop/go decision points. Honest reporting of risks and issues to steering committee. Independent assurance at key milestones. Realistic planning with contingency built in.

**Contingency Plan**: If programme is at risk, descope to minimum viable product (API catalogue + gateway for 3 departments), declare reduced scope as Phase 1 success, seek re-approval for expanded scope in subsequent spending review.

---

### Risk R-4: Data Protection Regulatory Challenge

**Related Stakeholders**: ICO, Department API Owners, GDS Service Owner

**Risk Description**: ICO determines that the aggregation model creates unacceptable data protection risks, requires fundamental architectural changes, or issues enforcement notice.

**Impact on Goals**: G-7 (data protection), G-2 (coverage for personal data APIs)

**Probability**: LOW

**Impact**: HIGH

**Mitigation Strategy**: Early and proactive ICO engagement. Complete DPIA before processing personal data. Clear data controller/processor agreements. Privacy by design architecture. Conservative approach to personal data caching (no caching unless explicitly required and lawfully based).

**Contingency Plan**: If ICO raises fundamental concerns, restrict platform to non-personal data APIs initially while addressing architectural requirements. Engage ICO sandbox process for novel processing models.

---

### Risk R-5: Low Developer Adoption

**Related Stakeholders**: Third-party developers, GDS Director, HM Treasury

**Risk Description**: Despite building the platform, developers continue using direct department APIs, preferring established integrations over a new intermediary.

**Impact on Goals**: G-1 (onboarding), G-4 (VfM), O-1 (ecosystem growth), O-3 (ROI)

**Probability**: MEDIUM

**Impact**: MEDIUM

**Mitigation Strategy**: User research-driven design ensuring the platform genuinely reduces friction. Active developer relations programme. SDK and code example development. Conference talks and blog posts. Sandbox environment for frictionless experimentation. Feedback loop incorporating developer needs into roadmap.

**Contingency Plan**: If adoption is below target at Month 6, conduct rapid developer research to understand barriers. Pivot to address specific pain points identified. Consider partnering with GovTech accelerators to seed adoption.

---

## Governance & Decision Rights

### Decision Authority Matrix (RACI)

| Decision Type | Responsible | Accountable | Consulted | Informed |
|---------------|-------------|-------------|-----------|----------|
| Programme budget approval | SRO | GDS Director | HM Treasury, Finance | All stakeholders |
| Department onboarding priority | Service Owner | GDS Director | Dept API Owners, Architect | Developers, Ops |
| Architecture decisions | Enterprise Architect | SRO | NCSC, Dept API Owners, Ops | Developers |
| Security architecture | Security Lead | NCSC Advisor | Enterprise Architect, Dept API Owners | SRO, Ops |
| API design standards | Service Owner | Enterprise Architect | Developers (research), Dept API Owners | All |
| Go/no-go for public beta | SRO | GDS Director | All stakeholders | All |
| Incident response (P1) | Ops Lead | SRO | NCSC, affected Dept API Owners | All stakeholders |
| Data protection decisions | DPO | SRO | ICO, Dept API Owners, Legal | Service Owner |
| Service Standard assessment readiness | Service Owner | SRO | User Researchers, Architect, Ops | GDS Director |
| Vendor/supplier selection | Delivery Manager | SRO | Procurement, Architecture | Finance |

### Escalation Path

1. **Level 1**: Service Owner / Delivery Manager (day-to-day product and delivery decisions)
2. **Level 2**: Programme Steering Committee — SRO, GDS Director, Enterprise Architect (scope changes, timeline variances > 2 weeks, budget variances > 10%, stakeholder conflicts)
3. **Level 3**: GDS Director General / Permanent Secretary (strategic direction, ministerial escalation, cross-department disputes, programme stop/continue decisions)

---

## Validation & Sign-off

### Stakeholder Review

| Stakeholder | Review Date | Comments | Status |
|-------------|-------------|----------|--------|
| GDS Director of Technology | PENDING | | PENDING |
| SRO | PENDING | | PENDING |
| NCSC Advisor | PENDING | | PENDING |
| Department API Owner representative | PENDING | | PENDING |
| GDS Operations Lead | PENDING | | PENDING |
| ICO engagement lead | PENDING | | PENDING |

### Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Programme Sponsor | | | |
| Senior Responsible Owner | | | |
| Enterprise Architect | | | |

---

## Appendices

### Appendix A: Stakeholder Interview Summaries

_Interviews to be conducted during Discovery phase. This section will be populated with findings from structured interviews with each key stakeholder group._

#### Planned Interviews

| Stakeholder Group | Target Date | Method | Status |
|-------------------|-------------|--------|--------|
| Department API Owners (HMRC, CH, DVLA, EA, OS) | TBC | 1:1 sessions | PLANNED |
| Third-party developers | TBC | Group sessions + survey | PLANNED |
| NCSC Advisory | TBC | 1:1 workshop | PLANNED |
| GDS Operations | TBC | Team session | PLANNED |
| Local authority digital teams | TBC | Survey + 3 interviews | PLANNED |

---

### Appendix B: Survey Results

_Developer survey to be conducted during Discovery phase to validate assumptions about integration pain points and platform requirements._

---

### Appendix C: References

- ARC-000-PRIN-v1.0 — Architecture Principles (UK Government API Aggregator)
- UK Government Technology Code of Practice
- GDS Service Standard (14 points)
- NCSC Cloud Security Principles
- NCSC Cyber Assessment Framework
- UK GDPR / Data Protection Act 2018
- HM Treasury Green Book (business case guidance)
- api.gov.uk — existing UK Government API catalogue

---

**Generated by**: ArcKit `/arckit.stakeholders` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.1.0
**Project**: UK Government API Aggregator (Project 001)
**AI Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
