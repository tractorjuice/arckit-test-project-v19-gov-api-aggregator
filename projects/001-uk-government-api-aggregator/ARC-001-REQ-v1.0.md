# Project Requirements: UK Government API Aggregator

> **Template Status**: Live | **Version**: 1.1.0 | **Command**: `/arckit.requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v1.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | UK Government API Aggregator (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-02-01 |
| **Last Modified** | 2026-02-01 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-03-03 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Programme Board, Architecture Team, Development Teams, GDS Assessors, Department API Owners |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-01 | ArcKit AI | Initial creation from `/arckit.requirements` command | [PENDING] | [PENDING] |

## Document Purpose

This document defines the comprehensive business, functional, non-functional, integration, and data requirements for the UK Government API Aggregator platform. It will be used for: vendor evaluation (if applicable), architecture design decisions, development planning, GDS Service Standard assessment evidence, and acceptance testing. Requirements trace back to stakeholder drivers (ARC-001-STKE-v1.0) and comply with architecture principles (ARC-000-PRIN-v1.0).

---

## Executive Summary

### Business Context

The UK Government maintains hundreds of APIs across dozens of departments — HMRC, NHS Digital, Companies House, DVLA, Environment Agency, Ordnance Survey, and many others — catalogued at api.gov.uk. Currently, developers must independently discover, register for, and integrate with each department's API, navigating separate developer portals, authentication schemes, rate limiting policies, data formats, and error handling conventions. This fragmentation suppresses innovation, increases integration costs, and creates barriers particularly for smaller organisations and local authority digital teams.

The UK Government API Aggregator will create a unified platform that discovers, catalogues, and provides standardised access to government APIs. It acts as an intelligent gateway — not replacing department APIs but providing a consistent, well-documented entry point that reduces integration friction while preserving department control over their services.

This project directly supports the Government Digital Strategy's goal of making government a platform, the Technology Code of Practice (TCoP), and GDS's mandate to deliver cross-government digital platforms.

### Objectives

- **O1**: Discover and catalogue all publicly available UK Government APIs into a searchable, maintained registry
- **O2**: Provide a unified API gateway with consistent authentication, error handling, and rate limiting across departments
- **O3**: Build a self-service developer portal for API discovery, registration, sandbox testing, and key management
- **O4**: Normalise response formats across departments into consistent data structures where possible
- **O5**: Track and report API usage analytics, availability, latency, and error patterns

### Expected Outcomes

- **Outcome 1**: 500+ registered developers and 50+ production applications within 12 months of public beta (supports Goal G-1, G-2)
- **Outcome 2**: 60%+ reduction in developer integration time compared to direct department API integration (supports Goal G-1)
- **Outcome 3**: 8+ government departments' APIs aggregated within 18 months (supports Goal G-2)
- **Outcome 4**: Zero security incidents involving credential leakage or unauthorised data access (supports Goal G-3)
- **Outcome 5**: 1.5:1 cost-benefit ratio within 24 months of launch (supports Goal G-4)

### Project Scope

**In Scope**:
- Automated discovery and cataloguing of UK Government APIs from api.gov.uk and department developer hubs
- Unified API gateway with request routing to upstream department APIs
- Developer portal with registration, documentation, sandbox, and key management
- Response normalisation and data transformation layer
- Usage analytics and monitoring dashboard
- Integration with at least 8 government departments in Phase 1
- Open data and non-personal-data APIs (primary focus)
- APIs returning personal data (with appropriate controls, phased approach)

**Out of Scope**:
- Replacing or modifying department APIs themselves
- Creating new APIs that don't exist at the department level
- Hosting department API infrastructure
- Processing classified data (SECRET or above)
- Mobile native applications (developer portal is web-based)
- Providing guarantees on upstream API data quality or accuracy
- Payment processing or commercial API monetisation

---

## Stakeholders

| Stakeholder | Role | Organization | Involvement Level | Ref |
|-------------|------|--------------|-------------------|-----|
| GDS Director of Technology | Executive Sponsor | GDS | Decision maker | SD-1 |
| Senior Responsible Owner (SRO) | Programme Governance | GDS | Programme accountability | SD-6 |
| GDS Service Owner | Product Owner | GDS | Requirements definition, prioritisation | — |
| Enterprise Architect | Architecture Governance | GDS | Technical oversight | — |
| Department API Owners | Upstream providers | HMRC, CH, DVLA, NHS Digital, EA, OS | Integration partners | SD-2 |
| NCSC Advisor | Security Oversight | NCSC | Security review and approval | SD-4 |
| ICO Engagement Lead | Data Protection | ICO | Compliance oversight | SD-7 |
| HM Treasury Spending Team | Financial Oversight | HM Treasury | Budget approval | SD-5 |
| Third-party Developers | End Users | Private sector, civic tech | User acceptance, feedback | SD-3 |
| Local Authority Digital Teams | End Users | Local government | User acceptance, feedback | SD-10 |
| GDS Operations / WebOps | Operations | GDS | Operational readiness | SD-8 |
| GDS User Researchers | Research | GDS | User needs evidence | SD-9 |

---

## Business Requirements

### BR-001: Cross-Government API Discovery and Cataloguing

**Description**: The platform MUST automatically discover, index, and maintain a comprehensive catalogue of UK Government APIs from all departments that publish APIs, creating a single searchable registry of government data and services.

**Rationale**: Currently api.gov.uk provides a basic catalogue but it is manually maintained and incomplete. Automated discovery ensures comprehensive, current coverage and reduces the burden on departments to register their APIs. (Addresses SD-1: Cross-government platform delivery; SD-3: Developer needs for discoverability)

**Success Criteria**:
- Catalogue covers 90%+ of APIs listed on api.gov.uk within 3 months of launch
- New APIs detected and catalogued within 48 hours of publication
- Catalogue metadata includes: department, description, endpoints, authentication method, rate limits, data format, status, version
- Catalogue searchable by department, data domain, keyword, and capability

**Priority**: MUST_HAVE

**Stakeholder**: GDS Director (SD-1), Third-party developers (SD-3)

**Traces to**: Goal G-2 (API aggregation coverage), Principle 3 (Interoperability)

---

### BR-002: Unified API Access Gateway

**Description**: The platform MUST provide a single API gateway endpoint through which developers can access multiple government department APIs with consistent authentication, request formatting, error handling, and rate limiting.

**Rationale**: Developers currently integrate with each department separately, dealing with different authentication, formats, and error handling. A unified gateway eliminates this per-department overhead. (Addresses SD-3: Simplified integration; SD-10: Affordable access for local authorities)

**Success Criteria**:
- Developers access APIs from 8+ departments through a single base URL and authentication token
- Consistent JSON error response format across all aggregated APIs
- Request/response logging with correlation IDs for troubleshooting
- Gateway adds < 50ms overhead to upstream API response time (p95)

**Priority**: MUST_HAVE

**Stakeholder**: Third-party developers (SD-3), Local authorities (SD-10)

**Traces to**: Goal G-1 (Unified onboarding), Principle 3 (Interoperability), Principle 12 (API-First Design)

---

### BR-003: Developer Self-Service Portal

**Description**: The platform MUST provide a self-service web portal where developers can discover APIs, register for access, manage API keys, access sandbox environments, read documentation, and view usage analytics.

**Rationale**: Reducing friction in the developer journey is the core value proposition. Self-service eliminates manual approval bottlenecks and enables developers to start building immediately. (Addresses SD-3, SD-10, Goal G-1)

**Success Criteria**:
- Developer registration completed in under 5 minutes
- First API call achievable within 1 hour of registration (including sandbox)
- API documentation auto-generated from upstream API specifications
- Developer dashboard showing usage, rate limit consumption, and error rates
- Portal meets WCAG 2.2 Level AA accessibility standards

**Priority**: MUST_HAVE

**Stakeholder**: Third-party developers (SD-3), GDS User Researchers (SD-9)

**Traces to**: Goal G-1 (Unified onboarding), Goal G-5 (Service Standard), Principle 6 (User-Centred Design)

---

### BR-004: Department Control and Transparency

**Description**: The platform MUST preserve department API owners' control over their APIs, including rate limiting, access policies, authentication upgrades, API versioning, and deprecation decisions, while providing them with visibility into how their APIs are consumed through the aggregator.

**Rationale**: Department buy-in is critical to success. Departments will not participate if they lose control over their APIs or cannot see what is happening. (Addresses SD-2: Protect service integrity and autonomy)

**Success Criteria**:
- Departments can set and modify rate limits for their APIs through the platform
- Departments receive real-time traffic analytics for their APIs
- Departments can block specific consumers or IP ranges
- Department authentication and access policy changes propagated within 15 minutes
- Departments can deprecate or retire API versions with configurable notice periods
- MoU framework agreed and signed with each participating department

**Priority**: MUST_HAVE

**Stakeholder**: Department API Owners (SD-2)

**Traces to**: Goal G-2 (Coverage depends on department participation), Principle 10 (Loose Coupling)

---

### BR-005: Value for Money Evidence

**Description**: The platform MUST collect and report metrics that demonstrate value for money, including developer time savings, department support cost reduction, new applications enabled, and cost per API transaction.

**Rationale**: HM Treasury requires ongoing evidence that the programme delivers benefits exceeding costs. Without this evidence, continued funding is at risk. (Addresses SD-5: Value for money; SD-6: Successful delivery)

**Success Criteria**:
- Benefits realisation dashboard available to SRO and Treasury
- Developer time savings quantified through survey and funnel analytics
- Department support ticket reduction tracked per participating department
- Quarterly benefits realisation report produced automatically
- Cost-benefit ratio tracked and reported against 1.5:1 target

**Priority**: MUST_HAVE

**Stakeholder**: HM Treasury (SD-5), SRO (SD-6)

**Traces to**: Goal G-4 (Value for money), Outcome O-3 (ROI)

---

### BR-006: Phased Delivery with Stop/Go Gates

**Description**: The platform MUST be delivered in phases (Discovery, Alpha, Private Beta, Public Beta, Live) with clear stop/go decision points at each gate, enabling incremental investment based on evidence of value.

**Rationale**: Phased delivery reduces financial risk and allows early course correction. This approach satisfies both Treasury's need for controlled spending and the SRO's need for risk management. (Addresses SD-5, SD-6, Conflict C-2)

**Success Criteria**:
- Each phase has defined entry/exit criteria and deliverables
- Stop/go decisions documented with evidence basis
- Phase costs tracked independently for incremental ROI assessment
- GDS Service Standard assessment at Alpha and Beta gates

**Priority**: MUST_HAVE

**Stakeholder**: SRO (SD-6), HM Treasury (SD-5)

**Traces to**: Goal G-5 (Service Standard compliance)

---

## Functional Requirements

### User Personas

#### Persona 1: Alex — Private Sector Developer
- **Role**: Full-stack developer at a GovTech startup
- **Goals**: Build applications that combine data from multiple government APIs (Companies House + HMRC) with minimal integration overhead
- **Pain Points**: Currently manages 4 separate API registrations, 4 sets of credentials, 4 different authentication flows, 4 different error formats
- **Technical Proficiency**: High

#### Persona 2: Sam — Local Authority Developer
- **Role**: Digital developer in a small council digital team (3 people)
- **Goals**: Access environmental, planning, and property data APIs for local services without the overhead of integrating with each department separately
- **Pain Points**: Limited time and budget; cannot justify the effort of separate registrations for each API needed; often uses screen-scraping as a workaround
- **Technical Proficiency**: Medium

#### Persona 3: Jordan — Department API Owner
- **Role**: Technical lead responsible for a department's public API estate
- **Goals**: Maintain control of their APIs while benefiting from increased adoption and reduced developer support burden
- **Pain Points**: Spends 30% of team time on developer onboarding and support; worried about unknown intermediaries accessing their APIs
- **Technical Proficiency**: High

#### Persona 4: Pat — Platform Administrator
- **Role**: GDS WebOps engineer responsible for platform operations
- **Goals**: Operate the aggregator with minimal toil, clear monitoring, and automated recovery
- **Pain Points**: Already responsible for multiple GDS platforms; cannot absorb a complex, manually-intensive system
- **Technical Proficiency**: High

---

### Use Cases

#### UC-1: Developer Discovers and Calls an API

**Actor**: Alex (Private Sector Developer)

**Preconditions**:
- Developer has internet access
- Developer portal is available
- At least one department API is integrated

**Main Flow**:
1. Developer visits the developer portal
2. Developer searches the API catalogue by keyword or browses by department
3. System displays matching APIs with descriptions, endpoints, data formats, and status
4. Developer selects an API and views detailed documentation
5. Developer registers for an account (email, organisation, intended use)
6. System provisions API key and sandbox credentials
7. Developer makes a test call in the sandbox environment
8. System returns mock response in normalised format
9. Developer upgrades to production access
10. Developer makes production API call through the gateway
11. System routes request to upstream department API, returns normalised response

**Postconditions**:
- Developer has active account with API key
- API call logged in usage analytics
- Department API owner can see the traffic in their dashboard

**Alternative Flows**:
- **Alt 3a**: No results found — system suggests related APIs or departments
- **Alt 5a**: Developer already has an account — system authenticates and skips registration
- **Alt 9a**: Production access requires approval for personal data APIs — system routes request for department review

**Exception Flows**:
- **Ex 1**: Upstream API is unavailable — system returns structured error with upstream status, cached response if available
- **Ex 2**: Rate limit exceeded — system returns 429 with retry-after header and rate limit details

**Priority**: CRITICAL

---

#### UC-2: Department Onboards Their API

**Actor**: Jordan (Department API Owner)

**Preconditions**:
- MoU signed between department and GDS
- Department API has machine-readable specification (OpenAPI preferred)

**Main Flow**:
1. Department API owner accesses department admin portal
2. Owner registers their API with specification URL or file upload
3. System validates the API specification and extracts metadata
4. System generates adapter configuration based on specification
5. Owner configures rate limits, access policies, and authentication mapping
6. System deploys adapter to staging environment
7. Owner runs integration tests against staging
8. Owner approves promotion to production
9. System adds API to public catalogue and enables routing

**Postconditions**:
- API visible in catalogue and accessible through gateway
- Department dashboard shows traffic analytics
- Alerting configured for upstream API health

**Alternative Flows**:
- **Alt 3a**: Specification invalid — system provides validation errors and guidance
- **Alt 4a**: Non-standard API without specification — manual adapter development required

**Priority**: HIGH

---

#### UC-3: Platform Administrator Responds to Incident

**Actor**: Pat (Platform Administrator)

**Preconditions**:
- Platform monitoring is active
- Alerting rules configured
- Runbooks available

**Main Flow**:
1. Monitoring system detects upstream API failure (circuit breaker opens)
2. System sends alert to on-call engineer with runbook link
3. Administrator reviews dashboard showing affected upstream API
4. System has already activated circuit breaker and is returning cached responses or graceful errors
5. Administrator confirms automated mitigation is working correctly
6. Upstream API recovers — circuit breaker closes automatically
7. Administrator documents incident and closes alert

**Postconditions**:
- Incident documented in incident management system
- Upstream API owner notified
- No manual intervention required for recovery

**Priority**: HIGH

---

### Functional Requirements Detail

#### FR-001: API Catalogue Discovery Engine

**Description**: The system MUST automatically discover UK Government APIs by crawling api.gov.uk, department developer hubs (HMRC Developer Hub, Companies House API, DVLA API, NHS Digital API Hub, Environment Agency API, Ordnance Survey Data Hub), and machine-readable API specifications.

**Relates To**: BR-001, UC-2

**Acceptance Criteria**:
- [ ] Given api.gov.uk is accessible, when the discovery engine runs, then all APIs listed on api.gov.uk are indexed with metadata
- [ ] Given a department developer hub URL, when the engine crawls it, then API endpoints and documentation links are extracted
- [ ] Given an OpenAPI/Swagger specification URL, when imported, then all endpoints, parameters, and response schemas are catalogued
- [ ] Given a previously discovered API has changed, when the engine re-crawls, then the catalogue is updated within 48 hours
- [ ] Given a department publishes a new API, when the engine next runs, then the new API appears in the catalogue

**Data Requirements**:
- **Inputs**: Department hub URLs, api.gov.uk catalogue, OpenAPI specs
- **Outputs**: Structured API metadata records
- **Validations**: URL reachability, specification format validity

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: Access to api.gov.uk data, department developer hub availability

---

#### FR-002: API Catalogue Search and Browse

**Description**: The system MUST provide full-text search and faceted browsing of the API catalogue, allowing developers to find APIs by keyword, department, data domain, status, and authentication type.

**Relates To**: BR-001, BR-003, UC-1

**Acceptance Criteria**:
- [ ] Given a search query "company information", when searched, then Companies House APIs appear in top results
- [ ] Given filter by department "HMRC", when applied, then only HMRC APIs are displayed
- [ ] Given filter by status "live", when applied, then deprecated or beta APIs are excluded
- [ ] Given a search with no results, when displayed, then system suggests related terms or departments
- [ ] Search results returned in < 500ms (p95)

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001 (catalogue must be populated)

---

#### FR-003: Developer Registration and Account Management

**Description**: The system MUST allow developers to self-register, manage their profile, and maintain their organisation details through the developer portal.

**Relates To**: BR-003, UC-1

**Acceptance Criteria**:
- [ ] Given a new developer, when they complete registration (email, name, organisation, intended use), then account is created within 30 seconds
- [ ] Given a registered developer, when they log in, then they access their dashboard with API keys, usage, and settings
- [ ] Given a developer requests account deletion, when confirmed, then all personal data is deleted within 30 days (UK GDPR compliance)
- [ ] Registration does not require manual approval for open data APIs

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: NFR-SEC-1 (authentication), DR-002 (developer account data)

---

#### FR-004: API Key Management

**Description**: The system MUST allow developers to create, rotate, revoke, and manage API keys for authenticating gateway requests.

**Relates To**: BR-003, UC-1

**Acceptance Criteria**:
- [ ] Given a registered developer, when they request an API key, then a key is generated and displayed once
- [ ] Given an active API key, when the developer rotates it, then a new key is issued and the old key expires after a configurable grace period (default 24 hours)
- [ ] Given a compromised key, when revoked, then all requests using that key are rejected immediately
- [ ] Given a developer, when they view their keys, then they see key prefix, creation date, last used date, and status (key value is never re-displayed)
- [ ] Developers can create multiple keys per application for key rotation

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: NFR-SEC-4 (secrets management)

---

#### FR-005: API Gateway Request Routing

**Description**: The system MUST route incoming API requests to the correct upstream department API based on the request path, apply consumer authentication and rate limiting, and return the response to the caller.

**Relates To**: BR-002, UC-1

**Acceptance Criteria**:
- [ ] Given a valid request to `/v1/companies-house/company/{id}`, when processed, then the request is routed to Companies House API and the response returned
- [ ] Given a request with an invalid API key, when received, then a 401 error is returned with a consistent error format
- [ ] Given a request exceeding the consumer's rate limit, when received, then a 429 response is returned with Retry-After header
- [ ] Given an upstream API timeout, when detected, then a 504 error is returned within the platform timeout threshold
- [ ] Gateway adds a correlation ID header to all responses for tracing
- [ ] Gateway overhead does not exceed 50ms added latency (p95)

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: FR-001, FR-004, INT-001 through INT-008

---

#### FR-006: Response Normalisation

**Description**: The system SHOULD normalise responses from upstream APIs into consistent data formats, including consistent date formats, error structures, pagination patterns, and envelope structures, while preserving the original response data.

**Relates To**: BR-002

**Acceptance Criteria**:
- [ ] Given responses from different departments, when normalised, then all use ISO 8601 date formats
- [ ] Given error responses from different departments, when normalised, then all follow a consistent error schema (code, message, details, upstream_error)
- [ ] Given paginated responses, when normalised, then all use consistent pagination headers/metadata
- [ ] Given a normalised response, when the developer requests it, then the original un-normalised response is also available via a header flag
- [ ] Normalisation rules are configurable per upstream API without code changes

**Priority**: SHOULD_HAVE

**Complexity**: HIGH

**Dependencies**: FR-005, knowledge of each upstream API response format

---

#### FR-007: Sandbox Environment

**Description**: The system MUST provide a sandbox environment where developers can test API calls against mock responses without hitting upstream production APIs.

**Relates To**: BR-003, UC-1

**Acceptance Criteria**:
- [ ] Given a registered developer, when they use sandbox credentials, then requests return realistic mock data
- [ ] Sandbox mock responses mirror the structure of production responses for each API
- [ ] Sandbox is available without production API key approval
- [ ] Sandbox rate limits are generous (10x production) to support experimentation
- [ ] Sandbox clearly labelled in responses to prevent confusion with production data

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001 (API specifications needed to generate mocks)

---

#### FR-008: Usage Analytics Dashboard

**Description**: The system MUST provide usage analytics dashboards for both developers (their own usage) and department API owners (traffic to their APIs through the aggregator).

**Relates To**: BR-004, BR-005

**Acceptance Criteria**:
- [ ] Given a developer, when they view their dashboard, then they see: request count, error rate, latency percentiles, rate limit consumption — per API, per time period
- [ ] Given a department API owner, when they view their dashboard, then they see: total requests via aggregator, unique consumers, error rates, latency, top consumers — per API
- [ ] Given the SRO, when they view the platform dashboard, then they see: total developers, total API calls, top APIs, overall error rate, platform availability
- [ ] Analytics data available within 5 minutes of request completion (near-real-time)
- [ ] Historical data retained for at least 2 years with monthly aggregation

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-005 (gateway must log requests)

---

#### FR-009: Department Administration Portal

**Description**: The system MUST provide a secure administration portal for department API owners to manage their APIs, configure access policies, view analytics, and manage consumer access.

**Relates To**: BR-004, UC-2

**Acceptance Criteria**:
- [ ] Given a department admin, when they log in, then they access a dashboard for their department's APIs only
- [ ] Given a department admin, when they modify rate limits, then changes take effect within 15 minutes
- [ ] Given a department admin, when they block a consumer, then requests from that consumer are rejected immediately
- [ ] Given a department admin, when they upload a new API specification, then the catalogue is updated
- [ ] MFA required for all department admin access

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-004, NFR-SEC-1

---

#### FR-010: API Health Monitoring and Status Page

**Description**: The system MUST monitor the health of all upstream APIs and display current status on a public status page.

**Relates To**: BR-002

**Acceptance Criteria**:
- [ ] Given an upstream API, when health checks run every 60 seconds, then current availability status is displayed
- [ ] Given an upstream API becomes unavailable, when detected, then status page updates within 2 minutes
- [ ] Status page shows: current status (operational/degraded/outage), uptime history (90 days), incident history
- [ ] Developers can subscribe to status notifications via email or webhook
- [ ] Status page accessible without authentication

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: FR-005

---

#### FR-011: API Documentation Rendering

**Description**: The system MUST render interactive API documentation from machine-readable specifications, allowing developers to read endpoint descriptions, view request/response examples, and try API calls from the documentation.

**Relates To**: BR-003

**Acceptance Criteria**:
- [ ] Given an OpenAPI specification, when rendered, then developers see endpoint list, parameters, response schemas, and examples
- [ ] Given a documentation page, when developer clicks "Try it", then they can make a sandbox API call from the browser
- [ ] Documentation auto-updates when upstream API specification changes
- [ ] Documentation meets WCAG 2.2 AA accessibility

**Priority**: SHOULD_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001, FR-007

---

#### FR-012: Rate Limiting and Throttling

**Description**: The system MUST implement multi-tier rate limiting: platform-level limits, per-department limits (set by department owners), and per-consumer limits.

**Relates To**: BR-002, BR-004

**Acceptance Criteria**:
- [ ] Given a consumer exceeding their rate limit, when a request is received, then a 429 response is returned with X-RateLimit-Remaining and Retry-After headers
- [ ] Given a department has set a rate limit of 100 req/min for their API, when the 101st request arrives within the window, then it is rejected
- [ ] Rate limit configuration changeable by department admins without platform redeployment
- [ ] Rate limit headers included in all responses (X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset)
- [ ] Different rate limit tiers available (free tier, standard, elevated) configurable per consumer

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-005, FR-009

---

#### FR-013: Circuit Breaker and Fault Isolation

**Description**: The system MUST implement circuit breakers for each upstream API connection, preventing cascading failures when an upstream API is degraded or unavailable.

**Relates To**: BR-002

**Acceptance Criteria**:
- [ ] Given an upstream API returning 50%+ errors, when the circuit breaker triggers, then requests to that API return a 503 with informative error message without hitting the upstream API
- [ ] Given a tripped circuit breaker, when periodic health checks detect upstream recovery, then the circuit breaker resets
- [ ] Failure of one upstream API does not affect requests to other upstream APIs
- [ ] Circuit breaker state visible in operations dashboard
- [ ] Circuit breaker thresholds configurable per upstream API

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-005

**Traces to**: Principle 2 (Resilience and Fault Tolerance)

---

#### FR-014: Webhook Notifications

**Description**: The system SHOULD allow developers to register webhooks for notifications about API status changes, deprecation notices, and usage alerts.

**Relates To**: BR-003

**Acceptance Criteria**:
- [ ] Given a developer registers a webhook URL, when an API they use goes down, then a notification is sent to their webhook within 5 minutes
- [ ] Given a department deprecates an API version, when scheduled, then all consumers of that version receive advance notification
- [ ] Given a developer's usage exceeds 80% of their rate limit, when detected, then a warning notification is sent
- [ ] Webhook delivery includes retry logic (3 attempts with exponential backoff)

**Priority**: SHOULD_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-010, FR-012

---

#### FR-015: API Versioning Support

**Description**: The system MUST support multiple versions of upstream APIs simultaneously, allowing consumers to migrate at their own pace.

**Relates To**: BR-002, BR-004

**Acceptance Criteria**:
- [ ] Given an upstream API has v1 and v2, when a consumer calls v1, then v1 response is returned
- [ ] Given a version is deprecated, when accessed, then a deprecation warning header is included in the response
- [ ] Given a version is retired, when accessed, then a 410 Gone response with migration guidance is returned
- [ ] Version lifecycle (active/deprecated/retired) visible in catalogue and documentation

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-005, FR-001

---

#### FR-016: Platform Administration and Configuration

**Description**: The system MUST provide platform administration capabilities for GDS operators to manage the platform, configure global settings, and respond to operational events.

**Relates To**: UC-3

**Acceptance Criteria**:
- [ ] Given a platform administrator, when they access the admin portal, then they see global platform health, all upstream API statuses, and system metrics
- [ ] Given a platform administrator, when they need to block a malicious consumer, then they can do so immediately
- [ ] Given a platform administrator, when they deploy a new adapter, then it can be done without full platform redeployment
- [ ] All administrative actions are audit logged

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: NFR-SEC-2, NFR-C-2

---

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-001: Gateway Response Time

**Requirement**: The API gateway MUST add no more than 50ms overhead to upstream API response times at the 95th percentile under normal load.

- Gateway-added latency: < 50ms (p95), < 100ms (p99)
- End-to-end latency determined primarily by upstream API (not aggregator)
- Response time measured from gateway request receipt to response dispatch (excluding upstream time)

**Measurement Method**: Distributed tracing measuring gateway processing time separately from upstream API time. Continuous monitoring via APM tooling.

**Load Conditions**:
- Normal load: 1,000 requests per second across all APIs
- Peak load: 5,000 requests per second (tax deadline, census, etc.)
- Data volume: 100+ upstream API endpoints

**Priority**: MUST_HAVE

**Traces to**: Principle 13 (Performance and Efficiency), SD-3 (developers want low overhead)

---

#### NFR-P-002: Catalogue Search Performance

**Requirement**: API catalogue search MUST return results in under 500ms at the 95th percentile.

**Measurement Method**: End-to-end search latency from query submission to results rendered.

**Priority**: MUST_HAVE

---

#### NFR-P-003: Developer Portal Performance

**Requirement**: Developer portal pages MUST load in under 2 seconds on a standard broadband connection (10 Mbps), meeting GDS performance guidelines.

**Measurement Method**: Synthetic monitoring and real user monitoring (RUM).

**Priority**: MUST_HAVE

**Traces to**: Principle 6 (User-Centred Design), Goal G-5 (Service Standard)

---

#### NFR-P-004: Throughput Capacity

**Requirement**: The platform MUST support sustained throughput of 5,000 requests per second at peak with the ability to scale to 15,000 req/s within 10 minutes.

**Scalability**: Must scale horizontally to support 3x growth over 2 years without architectural changes.

**Priority**: MUST_HAVE

**Traces to**: Principle 1 (Scalability and Elasticity)

---

### Availability and Resilience Requirements

#### NFR-A-001: Platform Availability Target

**Requirement**: The platform (gateway, portal, catalogue) MUST achieve 99.9% availability measured monthly, independent of upstream API availability.

- Maximum planned downtime: 4 hours/month during maintenance windows
- Maximum unplanned downtime: 43.8 minutes/month (99.9% SLA)
- Platform availability measured independently of upstream API failures

**Maintenance Windows**: Weekday 02:00-06:00 GMT with advance notice

**Priority**: MUST_HAVE

**Traces to**: Principle 14 (Availability and Reliability), Goal G-6 (Operational sustainability)

---

#### NFR-A-002: Disaster Recovery

**RPO (Recovery Point Objective)**: Maximum 1 hour of data loss for platform-owned data (developer accounts, API keys, usage analytics)

**RTO (Recovery Time Objective)**: Maximum 4 hours to full platform restoration

**Backup Requirements**:
- Backup frequency: Hourly for transactional data, daily for configuration
- Backup retention: 30 days for operational backups, 2 years for audit data
- Geographic backup location: Separate UK availability zone or region

**Failover Requirements**:
- Automatic failover to secondary availability zone: YES
- Failover time: < 5 minutes for gateway components

**Priority**: MUST_HAVE

---

#### NFR-A-003: Upstream API Fault Isolation

**Requirement**: Failure of any single upstream government API MUST NOT affect the availability of other APIs through the platform. The platform MUST gracefully degrade, returning informative errors for unavailable APIs while continuing to serve available APIs.

**Resilience Patterns Required**:
- [ ] Circuit breaker for each upstream API connection
- [ ] Timeout on all upstream API calls (configurable per API, default 30 seconds)
- [ ] Retry with exponential backoff and jitter for transient failures
- [ ] Bulkhead isolation between upstream API adapters
- [ ] Cached response serving for read-only APIs during upstream outages (where configured)

**Priority**: MUST_HAVE

**Traces to**: Principle 2 (Resilience and Fault Tolerance)

---

### Scalability Requirements

#### NFR-S-001: Horizontal Scaling

**Requirement**: All platform components MUST support horizontal scaling without code changes or downtime.

**Growth Projections**:
- Year 1: 500 developers, 1M API calls/month, 8 department APIs
- Year 2: 1,500 developers, 5M API calls/month, 15 department APIs
- Year 3: 3,000 developers, 15M API calls/month, 25+ department APIs

**Scaling Triggers**: Auto-scale when request latency p95 > 40ms or CPU > 70% or queue depth > threshold

**Priority**: MUST_HAVE

**Traces to**: Principle 1 (Scalability and Elasticity)

---

#### NFR-S-002: Adapter Extensibility

**Requirement**: Adding a new upstream API adapter MUST NOT require changes to core platform components. New adapters MUST be deployable independently.

**Priority**: MUST_HAVE

**Traces to**: Principle 10 (Loose Coupling), Principle 15 (Maintainability)

---

### Security Requirements

#### NFR-SEC-001: Consumer Authentication

**Requirement**: All API gateway requests MUST be authenticated using API keys with support for OAuth 2.0 client credentials flow for machine-to-machine access.

**Multi-Factor Authentication (MFA)**:
- Required for: Developer portal login, department admin access, platform admin access
- MFA methods: Authenticator app, hardware security key

**Session Management**:
- Portal session timeout: 30 minutes of inactivity
- Absolute session timeout: 8 hours
- Re-authentication required for: API key creation, account deletion, permission changes

**Priority**: MUST_HAVE

**Traces to**: Principle 4 (Security by Design)

---

#### NFR-SEC-002: Role-Based Access Control

**Requirement**: The platform MUST implement RBAC with least privilege across four role categories: Developer, Department Admin, Platform Admin, and Read-Only Viewer.

**Roles**:
- **Developer**: Register, manage own keys, view own usage, access sandbox and production APIs
- **Department Admin**: Manage own department's APIs, view traffic analytics, manage consumer access for own APIs
- **Platform Admin**: Global platform management, user management, configuration
- **Read-Only Viewer**: View dashboards and analytics without modification capability

**Priority**: MUST_HAVE

**Traces to**: Principle 4 (Security by Design — Least Privilege)

---

#### NFR-SEC-003: Encryption

**Requirement**:
- Data in transit: TLS 1.2+ (TLS 1.3 preferred) for all connections
- Data at rest: AES-256 encryption for all data stores
- Upstream API credentials: Encrypted with separate key per department, never accessible to consumers

**Encryption Scope**:
- [ ] All database storage encrypted at rest
- [ ] All backup storage encrypted
- [ ] All inter-service communication over TLS
- [ ] Upstream API credentials encrypted with department-specific keys
- [ ] API keys hashed (not reversibly encrypted) in storage

**Priority**: MUST_HAVE

**Traces to**: Principle 4 (Security by Design — Encryption Everywhere)

---

#### NFR-SEC-004: Secrets Management

**Requirement**: No secrets (API keys, upstream credentials, certificates, database passwords) stored in code, configuration files, or environment variables in plain text. All secrets MUST be managed through a dedicated secrets management solution.

**Secrets Rotation**: Automatic rotation every 90 days for platform secrets; per-department schedule for upstream credentials

**Priority**: MUST_HAVE

**Traces to**: Principle 4 (Security by Design)

---

#### NFR-SEC-005: Credential Isolation

**Requirement**: Upstream API credentials for each department MUST be isolated such that compromise of one department's credentials cannot lead to access to another department's APIs. No single credential or key MUST grant access to all upstream APIs.

**Priority**: MUST_HAVE

**Traces to**: Principle 4, SD-4 (NCSC concern about high-value target)

---

#### NFR-SEC-006: Vulnerability Management

**Requirement**:
- Dependency scanning in CI/CD pipeline (no critical/high vulnerabilities merged)
- Static application security testing (SAST) on every pull request
- Dynamic application security testing (DAST) in staging environment
- Penetration testing: Before each phase gate by independent external tester
- OWASP API Security Top 10 explicitly addressed

**Remediation SLA**:
- Critical vulnerabilities: 24 hours
- High vulnerabilities: 7 days
- Medium vulnerabilities: 30 days

**Priority**: MUST_HAVE

**Traces to**: Principle 4, Goal G-3 (Security assurance)

---

#### NFR-SEC-007: Input Validation and API Security

**Requirement**: All input to the gateway MUST be validated and sanitised. The gateway MUST protect against injection attacks, oversized payloads, and request smuggling.

**Controls**:
- [ ] Request size limits enforced (configurable per API, default 10MB)
- [ ] Header injection prevention
- [ ] Path traversal prevention
- [ ] SQL/NoSQL injection prevention in catalogue search
- [ ] Rate limiting to prevent brute force attacks on authentication

**Priority**: MUST_HAVE

---

### Compliance and Regulatory Requirements

#### NFR-C-001: UK GDPR and Data Protection Act 2018

**Applicable Regulations**: UK GDPR, Data Protection Act 2018

**Compliance Requirements**:
- [ ] Data subject rights supported (access, deletion, portability) for developer account data
- [ ] Privacy notice published explaining platform's data processing
- [ ] Data Protection Impact Assessment (DPIA) completed before processing personal data
- [ ] Data controller/processor agreements signed with each department for personal data APIs
- [ ] Data breach notification to ICO within 72 hours
- [ ] Article 30 records of processing maintained
- [ ] No unnecessary caching of personal data from upstream API responses

**Data Residency**: All data processed and stored within the UK

**Data Retention**: Developer accounts retained while active + 30 days after deletion request; audit logs 2 years; usage analytics 2 years with aggregation

**Priority**: MUST_HAVE

**Traces to**: Principle 7 (Data Sovereignty), Goal G-7 (Data protection compliance), SD-7

---

#### NFR-C-002: Audit Logging

**Requirement**: Comprehensive, tamper-evident audit trail for all security-relevant and administrative operations.

**Audit Log Contents**:
- Who: Authenticated user/service identity
- What: Action performed (API call, config change, key creation, etc.)
- When: Timestamp (UTC, millisecond precision)
- Where: System component and endpoint
- Why: Correlation ID, request context
- Result: Success/failure with error code

**Log Retention**: 2 years minimum for audit logs (immutable storage)

**Log Integrity**: Tamper-evident logging with write-once storage

**Priority**: MUST_HAVE

**Traces to**: Principle 5 (Observability)

---

#### NFR-C-003: Technology Code of Practice (TCoP)

**Requirement**: All technology decisions MUST comply with the UK Government Technology Code of Practice.

**Key TCoP Requirements**:
- [ ] Open source by default
- [ ] Open standards for APIs and data formats
- [ ] Cloud-first hosting
- [ ] Secure by design
- [ ] User needs validated through research
- [ ] Accessible and inclusive

**Priority**: MUST_HAVE

**Traces to**: Principle 19 (TCoP Alignment), Principle 20 (Open Standards)

---

#### NFR-C-004: GDS Service Standard

**Requirement**: The platform MUST be designed and delivered to pass GDS Service Standard assessment at Alpha and Beta gates across all 14 points.

**Priority**: MUST_HAVE

**Traces to**: Goal G-5 (Service Standard compliance)

---

### Usability Requirements

#### NFR-U-001: Developer Portal UX

**Requirement**: The developer portal MUST be intuitive for developers with varying technical proficiency (Personas Alex and Sam).

**UX Standards**:
- Follows GOV.UK Design System patterns
- WCAG 2.2 Level AA compliance
- Mobile responsive design
- Browser support: Chrome, Firefox, Safari, Edge — last 2 versions
- Progressive enhancement: core functionality works without JavaScript

**Priority**: MUST_HAVE

**Traces to**: Principle 6 (User-Centred Design), Goal G-5

---

#### NFR-U-002: Accessibility

**Requirement**: WCAG 2.2 Level AA compliance for all user-facing components.

**Accessibility Features**:
- [ ] Keyboard navigation for all functions
- [ ] Screen reader compatibility (tested with JAWS, NVDA, VoiceOver)
- [ ] Sufficient colour contrast ratios
- [ ] Focus indicators visible
- [ ] Alt text for all images
- [ ] Error messages clearly associated with form fields

**Testing**: Automated accessibility testing in CI/CD (axe-core) + manual testing with assistive technologies each sprint

**Priority**: MUST_HAVE

---

### Maintainability and Supportability Requirements

#### NFR-M-001: Observability

**Requirement**: Comprehensive instrumentation for monitoring, troubleshooting, and capacity planning.

**Telemetry Requirements**:
- **Logging**: Structured JSON logs with correlation IDs spanning consumer → gateway → upstream API
- **Metrics**: Request rate, error rate, latency percentiles per upstream API, per consumer, per endpoint
- **Tracing**: Distributed tracing across all platform components
- **Dashboards**: Real-time operational dashboards for platform health, upstream API health, and consumer activity
- **Alerts**: SLO-based alerting with actionable runbook links

**Priority**: MUST_HAVE

**Traces to**: Principle 5 (Observability), Goal G-6 (Operational sustainability), SD-8

---

#### NFR-M-002: Documentation

**Requirement**: Comprehensive documentation for operators, developers, and department API owners.

**Documentation Types**:
- [ ] Architecture documentation (C4 model diagrams)
- [ ] API documentation (OpenAPI 3.0 specs for platform's own APIs)
- [ ] Operational runbooks for all known failure scenarios
- [ ] Developer onboarding guide
- [ ] Department onboarding guide
- [ ] Troubleshooting guides

**Priority**: MUST_HAVE

---

#### NFR-M-003: Infrastructure as Code

**Requirement**: All infrastructure MUST be defined as code, version-controlled, and deployed through automated pipelines. No manual infrastructure changes in any environment.

**Priority**: MUST_HAVE

**Traces to**: Principle 16 (Infrastructure as Code)

---

### Portability and Interoperability Requirements

#### NFR-I-001: Open API Standards

**Requirement**: All platform APIs MUST be documented using OpenAPI 3.0+ specifications. API catalogue data MUST be available in machine-readable format.

**API Design Principles**:
- RESTful design with standard HTTP methods
- JSON request/response format
- URL path versioning (e.g., /v1/, /v2/)
- Consistent error response format across all platform APIs
- Standard pagination via Link headers or cursor-based pagination

**Priority**: MUST_HAVE

**Traces to**: Principle 20 (Open Standards), Principle 12 (API-First Design)

---

#### NFR-I-002: Open Source

**Requirement**: Platform source code SHOULD be published as open source under an appropriate licence (MIT or OGL), in line with TCoP open source requirements.

**Priority**: SHOULD_HAVE

**Traces to**: NFR-C-003 (TCoP)

---

---

## Integration Requirements

### External System Integrations

#### INT-001: Integration with HMRC Developer Hub APIs

**Purpose**: Aggregate HMRC APIs (VAT, Self Assessment, Corporation Tax, Customs) into the unified gateway.

**Integration Type**: Real-time API proxying via HTTPS

**Data Exchanged**:
- **From Platform to HMRC**: Consumer API requests (authenticated, rate-limited)
- **From HMRC to Platform**: API responses (JSON)

**Authentication**: OAuth 2.0 (HMRC uses server token authentication for some APIs)

**Error Handling**: Circuit breaker with 30s timeout, 3 retries with exponential backoff

**SLA**: Dependent on HMRC's API SLA; platform adds < 50ms overhead

**Priority**: MUST_HAVE (Phase 1)

---

#### INT-002: Integration with Companies House API

**Purpose**: Aggregate Companies House APIs (company search, filing history, officers, charges) into the unified gateway.

**Integration Type**: Real-time API proxying via HTTPS

**Authentication**: API key (Companies House uses API key authentication)

**Priority**: MUST_HAVE (Phase 1)

---

#### INT-003: Integration with DVLA APIs

**Purpose**: Aggregate DVLA APIs (vehicle enquiry, MOT history) into the unified gateway.

**Integration Type**: Real-time API proxying via HTTPS

**Authentication**: API key

**Priority**: MUST_HAVE (Phase 1)

---

#### INT-004: Integration with NHS Digital APIs

**Purpose**: Aggregate NHS Digital APIs (Organisation Data Service, e-Referral, etc.) into the unified gateway.

**Integration Type**: Real-time API proxying via HTTPS

**Authentication**: OAuth 2.0 / NHS Identity

**Note**: Personal health data APIs require enhanced access controls and separate DPIA. Initially focus on non-patient-data APIs (ODS, reference data).

**Priority**: SHOULD_HAVE (Phase 1 for non-patient APIs, Phase 2 for clinical APIs)

---

#### INT-005: Integration with Environment Agency APIs

**Purpose**: Aggregate Environment Agency APIs (flood monitoring, water quality, bathing water, rainfall) into the unified gateway.

**Integration Type**: Real-time API proxying via HTTPS

**Authentication**: Open data (no authentication required for most EA APIs)

**Priority**: MUST_HAVE (Phase 1)

---

#### INT-006: Integration with Ordnance Survey Data Hub

**Purpose**: Aggregate Ordnance Survey APIs (OS Places, OS Maps, OS Features) into the unified gateway.

**Integration Type**: Real-time API proxying via HTTPS

**Authentication**: API key (OS uses key-based authentication)

**Note**: Some OS APIs are commercially licensed. Platform must respect OS licensing terms.

**Priority**: SHOULD_HAVE (Phase 1)

---

#### INT-007: Integration with Land Registry APIs

**Purpose**: Aggregate HM Land Registry APIs (price paid data, title plans) into the unified gateway.

**Integration Type**: Real-time API proxying via HTTPS

**Authentication**: API key

**Priority**: SHOULD_HAVE (Phase 2)

---

#### INT-008: Integration with DWP APIs

**Purpose**: Aggregate DWP APIs (benefits status, eligibility checking) into the unified gateway.

**Integration Type**: Real-time API proxying via HTTPS

**Authentication**: OAuth 2.0 with enhanced access controls (sensitive personal data)

**Note**: DWP APIs handle highly sensitive benefit data. Enhanced DPIA and access controls required.

**Priority**: COULD_HAVE (Phase 2)

---

#### INT-009: Integration with api.gov.uk Catalogue

**Purpose**: Ingest the existing api.gov.uk catalogue data to bootstrap the platform's API directory and maintain synchronisation.

**Integration Type**: Periodic batch import (crawl/scrape or API if available)

**Data Exchanged**:
- **From api.gov.uk to Platform**: API listings, metadata, department information, documentation links

**Priority**: MUST_HAVE (Phase 1)

---

---

## Data Requirements

### Data Entities

#### Entity 1: API Catalogue Entry

**Description**: Represents a single API or API endpoint discovered and catalogued by the platform.

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| id | UUID | Yes | Unique identifier | Primary key |
| department_id | UUID | Yes | Owning department | Foreign key |
| name | String(255) | Yes | API name | Not null |
| description | Text | Yes | API description | Not null |
| base_url | String(2048) | Yes | Upstream API base URL | Valid URL |
| specification_url | String(2048) | No | OpenAPI spec URL | Valid URL |
| auth_type | Enum | Yes | Authentication method | ['api_key', 'oauth2', 'open', 'mutual_tls'] |
| status | Enum | Yes | API status | ['active', 'beta', 'deprecated', 'retired'] |
| version | String(20) | Yes | API version | Semver format |
| data_classification | Enum | Yes | Data sensitivity | ['official', 'official_sensitive'] |
| rate_limit | Integer | No | Requests per minute | > 0 |
| discovered_at | Timestamp | Yes | First discovery date | Indexed |
| last_checked | Timestamp | Yes | Last health check | Indexed |
| metadata | JSONB | No | Additional metadata | Valid JSON |

**Relationships**: Many-to-one with Department; One-to-many with API Endpoint

**Data Volume**: ~500-1000 records Year 1, ~2000 Year 3

**Data Classification**: OFFICIAL (catalogue metadata is public)

**Data Retention**: Retained while API exists; archived 1 year after retirement

---

#### Entity 2: Developer Account

**Description**: Represents a registered developer or organisation using the platform.

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| id | UUID | Yes | Unique identifier | Primary key |
| email | String(255) | Yes | Developer email | Unique, validated |
| name | String(255) | Yes | Developer name | Not null |
| organisation | String(255) | No | Organisation name | |
| organisation_type | Enum | No | Org type | ['private', 'public_sector', 'civic_tech', 'academic'] |
| intended_use | Text | Yes | Description of intended use | Not null |
| status | Enum | Yes | Account status | ['active', 'suspended', 'deleted'] |
| created_at | Timestamp | Yes | Registration date | Indexed |
| last_login | Timestamp | No | Last login timestamp | |
| mfa_enabled | Boolean | Yes | MFA status | Default true |

**Data Volume**: 500 Year 1, 1500 Year 2, 3000 Year 3

**Data Classification**: OFFICIAL (contains PII — email, name)

**Data Retention**: Active while account exists; deleted 30 days after deletion request (UK GDPR)

---

#### Entity 3: API Key

**Description**: Authentication credential issued to developers for gateway access.

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| id | UUID | Yes | Unique identifier | Primary key |
| developer_id | UUID | Yes | Owning developer | Foreign key |
| key_hash | String(64) | Yes | SHA-256 hash of key | Indexed, unique |
| key_prefix | String(8) | Yes | First 8 chars for identification | Indexed |
| name | String(100) | No | Developer-assigned label | |
| status | Enum | Yes | Key status | ['active', 'revoked', 'expired'] |
| created_at | Timestamp | Yes | Creation date | |
| last_used | Timestamp | No | Last successful use | |
| expires_at | Timestamp | No | Expiry date | |

**Data Classification**: OFFICIAL-SENSITIVE (credential material)

**Data Retention**: Revoked/expired keys retained 90 days for audit, then deleted

---

#### Entity 4: API Request Log

**Description**: Record of each API request processed through the gateway, used for analytics, billing, and troubleshooting.

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| id | UUID | Yes | Unique identifier | Primary key |
| correlation_id | UUID | Yes | Request trace ID | Indexed |
| developer_id | UUID | Yes | Requesting developer | Indexed |
| api_id | UUID | Yes | Target API | Indexed |
| endpoint | String(2048) | Yes | Request path | |
| method | String(10) | Yes | HTTP method | |
| status_code | Integer | Yes | Response status code | |
| gateway_latency_ms | Integer | Yes | Gateway processing time | |
| upstream_latency_ms | Integer | No | Upstream API response time | |
| request_size_bytes | Integer | No | Request body size | |
| response_size_bytes | Integer | No | Response body size | |
| timestamp | Timestamp | Yes | Request time (UTC) | Partitioned |

**Data Volume**: 1M records/month Year 1, 15M records/month Year 3

**Data Classification**: OFFICIAL (no personal data in request logs; personal data in request/response bodies is NOT logged)

**Data Retention**: Raw logs 90 days; aggregated analytics 2 years

---

#### Entity 5: Department

**Description**: UK Government department that publishes APIs through the platform.

**Attributes**:
| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| id | UUID | Yes | Unique identifier | Primary key |
| name | String(255) | Yes | Department name | Unique |
| abbreviation | String(20) | Yes | Short name (e.g., HMRC) | Unique |
| admin_contact | String(255) | Yes | Primary admin email | |
| mou_signed | Boolean | Yes | MoU status | |
| mou_date | Date | No | MoU signature date | |
| onboarded_at | Timestamp | No | Integration date | |
| status | Enum | Yes | Department status | ['active', 'onboarding', 'suspended'] |

**Data Volume**: 8 Year 1, 25+ Year 3

**Data Classification**: OFFICIAL

**Data Retention**: Retained while department participates; archived after departure

---

### Data Quality Requirements

**Data Accuracy**: API catalogue entries must be verified against upstream sources at least daily; stale entries flagged automatically

**Data Completeness**: All required fields in catalogue entries populated; incomplete entries visible but marked as "incomplete"

**Data Consistency**: API status in catalogue must match actual upstream availability (checked via health monitoring)

**Data Timeliness**: Catalogue refreshed at least daily; usage analytics available within 5 minutes; status page within 2 minutes

**Data Lineage**: Each catalogue entry tracks source (api.gov.uk, department hub, manual), discovery date, and last verification

---

### Data Migration Requirements

**Migration Scope**: Import existing api.gov.uk catalogue data as initial seed for the platform catalogue.

**Migration Strategy**: One-time bulk import followed by ongoing synchronisation.

**Data Transformation**: Map api.gov.uk metadata fields to platform catalogue schema; enrich with additional metadata from department developer hubs.

**Data Validation**: Verify all imported URLs are reachable; validate specification links return valid OpenAPI documents.

---

## Constraints and Assumptions

### Technical Constraints

**TC-1**: Platform MUST be hosted within UK-approved cloud infrastructure (UK data residency requirement)

**TC-2**: Platform MUST integrate with upstream APIs as-is — cannot require departments to modify their APIs

**TC-3**: Platform MUST not store or cache personal data from upstream API responses unless explicitly required and lawfully based

**TC-4**: Platform MUST use open standards and avoid vendor lock-in for core components (TCoP requirement)

**TC-5**: Platform MUST be deployable and operable by existing GDS WebOps team capabilities

---

### Business Constraints

**BC-1**: Programme MUST operate within spending controls approved by HM Treasury

**BC-2**: Programme MUST pass GDS Service Standard assessment at Alpha and Beta gates

**BC-3**: Each department integration requires a signed MoU before production traffic

**BC-4**: Platform MUST NOT become the sole access path — departments must be able to continue offering direct API access

---

### Assumptions

**A-1**: Department API owners will agree to participate once value is demonstrated through early adopter success

**A-2**: Upstream government APIs will maintain reasonable backward compatibility for at least 6 months after version publication

**A-3**: api.gov.uk data will continue to be publicly available for catalogue seeding

**A-4**: GDS WebOps has capacity to absorb one additional platform into their operational portfolio

**A-5**: Developer demand exists — validated through user research during Discovery phase

**A-6**: Departments will provide (or already have) machine-readable API specifications for their APIs

**Validation Plan**: Assumptions A-1, A-5, and A-6 validated during Discovery/Alpha through department engagement and user research. A-4 validated through ops capacity assessment before Beta.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline | Measurement Method |
|--------|----------|--------|----------|-------------------|
| Registered developers | 0 | 500 | 12 months post-beta | Portal analytics |
| Production applications | 0 | 50 | 12 months post-beta | API key usage analysis |
| Departments integrated | 0 | 8 | 18 months | Platform catalogue |
| Developer integration time | 5-10 days | < 1 hour | Beta launch | Funnel analytics + survey |
| Cost-benefit ratio | N/A | 1.5:1 | 24 months | Benefits realisation tracker |
| Developer satisfaction (NPS) | N/A | > 40 | Ongoing | Quarterly survey |

### Technical Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Platform availability | 99.9% | Uptime monitoring |
| Gateway overhead (p95) | < 50ms | Distributed tracing |
| API call error rate (platform-caused) | < 0.1% | Log analysis |
| Mean time to detect (MTTD) | < 5 minutes | Monitoring |
| Mean time to recover (MTTR) | < 30 minutes | Incident tracking |
| Security incidents | 0 | Security monitoring |
| Deployment frequency | Multiple per week | CI/CD metrics |

---

## Dependencies and Risks

### Dependencies

| Dependency | Description | Owner | Target Date | Status | Impact if Delayed |
|------------|-------------|-------|-------------|--------|-------------------|
| Department MoUs | Signed agreements with 8+ departments | GDS Director | Month 6 | Not started | HIGH — no APIs to aggregate |
| api.gov.uk data access | Access to catalogue data for seeding | GDS | Month 1 | On Track | MEDIUM — can use web crawling |
| NCSC security review | Threat model and architecture approval | NCSC Advisor | Month 3 | Not started | HIGH — blocks development |
| DPIA completion | Data protection assessment before personal data processing | DPO | Month 4 | Not started | HIGH — blocks personal data APIs |
| Penetration testing | External pen test before public beta | Security Lead | Month 9 | Not started | HIGH — blocks public beta |
| GDS WebOps capacity | Ops team capacity for additional platform | Ops Lead | Month 6 | At Risk | MEDIUM — delays operational handover |

### Risks

| Risk ID | Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|-------------|-------------|--------|---------------------|-------|
| R-1 | Key departments refuse to participate | MEDIUM | HIGH | Start with willing departments; demonstrate value; ministerial support | GDS Director |
| R-2 | Security incident compromises upstream credentials | LOW | CRITICAL | Credential isolation; defence in depth; pen testing; monitoring | NCSC Advisor |
| R-3 | Programme costs exceed budget | MEDIUM | HIGH | Phased delivery with stop/go gates; descope if needed | SRO |
| R-4 | Low developer adoption | MEDIUM | MEDIUM | User research-driven design; developer relations; feedback loops | Service Owner |
| R-5 | ICO raises fundamental concerns about processing model | LOW | HIGH | Early DPIA; proactive ICO engagement; conservative personal data approach | DPO |
| R-6 | Upstream API changes break integrations | HIGH | MEDIUM | Contract testing; monitoring; adapter versioning; department notification | Architect |

---

## Requirement Conflicts & Resolutions

### Conflict C-1: Delivery Speed vs Department Onboarding Pace

**Conflicting Requirements**:
- **BR-002/G-2**: Aggregate 8+ departments within 18 months (GDS Director wants visible cross-government impact quickly)
- **BR-004**: Departments must retain control and sign MoUs before integration (Department API Owners need careful, consensual process)

**Stakeholders Involved**:
- **GDS Director (SD-1)**: Needs visible platform adoption to justify GDS investment and mandate
- **Department API Owners (SD-2)**: Need careful integration that doesn't threaten their services

**Nature of Conflict**: Rapid onboarding requires departments to move faster than their governance processes typically allow. Forced participation would undermine trust and quality.

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Mandate participation | Fast coverage | Departments resist, poor quality | GDS Director happy short-term; departments alienated |
| **Option 2**: Wait for full consensus | Full buy-in | Slow, may never reach critical mass | Departments happy; GDS Director frustrated |
| **Option 3**: Phase with willing first | Quick wins build momentum | Coverage initially limited | Both partially satisfied |

**Resolution Strategy**: PHASE

**Decision**: Option 3 — Start with willing "early adopter" departments (Companies House, Environment Agency, Ordnance Survey are historically cooperative). Use early success to build peer pressure and demonstrate the model before approaching cautious departments.

**Decision Authority**: GDS Director with SRO approval (per RACI)

**Impact on Requirements**: BR-002 target adjusted: "at least 3 departments by Month 6, 8+ by Month 18" to reflect phased approach.

**Stakeholder Management**:
- **GDS Director**: Presented evidence that phased approach achieves same 18-month target while building sustainable relationships
- **Department API Owners**: Reassured that participation is opt-in with clear MoU preserving their control

---

### Conflict C-2: Open Access vs Personal Data Protection

**Conflicting Requirements**:
- **FR-003/BR-003**: Frictionless developer registration and immediate API access (developers want minimal barriers)
- **NFR-C-001/G-7**: Strict data protection controls for personal data APIs (ICO requires lawful basis, purpose limitation, access controls)

**Stakeholders Involved**:
- **Third-party developers (SD-3)**: Want single registration, immediate access to all APIs
- **ICO (SD-7)**: Require appropriate controls proportional to data sensitivity

**Nature of Conflict**: Cannot provide frictionless access to personal data APIs (DVLA vehicle keeper data, HMRC tax data) without appropriate access controls and purpose verification.

**Resolution Strategy**: INNOVATE (tiered access)

**Decision**: Implement tiered access model:
- **Tier 1 (Open)**: Open data and non-personal APIs — lightweight registration, immediate access
- **Tier 2 (Standard)**: APIs with aggregated/anonymised data — registration + terms acceptance
- **Tier 3 (Controlled)**: Personal data APIs — enhanced verification, purpose declaration, department approval

**Impact on Requirements**:
- FR-003 modified: "Registration provides immediate Tier 1 and Tier 2 access; Tier 3 requires additional verification"
- New requirement: FR-003a: "System MUST support tiered access levels with different onboarding requirements per tier"

**Stakeholder Management**:
- **Developers**: Most APIs (open data, reference data) available immediately; only sensitive APIs require additional steps
- **ICO**: Controls proportional to risk; personal data APIs properly protected

---

### Conflict C-3: Security Review Cycles vs Delivery Pace

**Conflicting Requirements**:
- **BR-006**: Deliver through agile phases with frequent releases
- **NFR-SEC-006/G-3**: Thorough security review and penetration testing before each phase gate

**Stakeholders Involved**:
- **SRO (SD-6)**: Wants to demonstrate progress through frequent deliverables
- **NCSC Advisor (SD-4)**: Requires thorough security review which takes time

**Resolution Strategy**: INNOVATE

**Decision**: Embed security in every sprint rather than treating it as a gate:
- Security engineer embedded in delivery team from Day 1
- Automated security testing (SAST, DAST, dependency scanning) in CI/CD pipeline
- Threat model created and updated continuously, not just at gates
- NCSC advisor attends fortnightly review rather than single gate review
- Penetration testing at phase gates is confirmatory, not discovery-focused (because continuous testing catches issues earlier)

**Impact on Requirements**: NFR-SEC-006 updated to include continuous security testing requirements alongside phase-gate pen tests.

---

### Conflict C-4: Platform Overhead vs Developer Expectations

**Conflicting Requirements**:
- **NFR-P-001**: Gateway adds < 50ms overhead (developers expect near-zero overhead)
- **FR-006/FR-012/FR-013**: Gateway performs authentication, rate limiting, normalisation, circuit breaking (each adds latency)

**Stakeholders Involved**:
- **Third-party developers (SD-3)**: Want aggregator to be faster than direct access, or at least not noticeably slower
- **GDS Operations (SD-8)**: Need robust gateway features for operability

**Resolution Strategy**: COMPROMISE

**Decision**: Target 50ms p95 overhead as achievable with efficient implementation. Normalisation (FR-006) marked SHOULD_HAVE rather than MUST_HAVE, allowing it to be disabled if it pushes latency beyond target. Optional normalisation via request header flag.

---

## Timeline and Milestones

### High-Level Milestones

| Milestone | Description | Target Date | Dependencies |
|-----------|-------------|-------------|--------------|
| Discovery Complete | User research, department engagement, technical feasibility | Month 3 | Funding approval |
| Alpha Assessment | GDS Service Standard Alpha assessment | Month 5 | Discovery findings |
| Private Beta Launch | 3 departments, 20 invited developers | Month 8 | Alpha pass, 3 MoUs signed, pen test |
| Beta Assessment | GDS Service Standard Beta assessment | Month 10 | Private beta feedback |
| Public Beta Launch | 5+ departments, open registration | Month 12 | Beta pass, DPIA complete |
| Live Service | Full production service, 8+ departments | Month 18 | Operational readiness |

---

## Budget

### Cost Estimate

| Category | Estimated Cost | Notes |
|----------|----------------|-------|
| Discovery & Alpha | £500K-£800K | Team of 8-10, 5 months |
| Beta Development | £1.2M-£1.8M | Team of 12-15, 7 months |
| Live Transition | £300K-£500K | Operational handover, 3 months |
| Security Testing | £100K-£200K | External pen testing, 3 rounds |
| **Total Programme** | **£2.1M-£3.3M** | 18 months |

### Ongoing Operational Costs

| Category | Annual Cost | Notes |
|----------|-------------|-------|
| Cloud Infrastructure | £200K-£400K/year | Scales with usage |
| Operations Team | £300K-£500K/year | 2-3 FTE WebOps |
| Security & Compliance | £100K-£150K/year | Annual pen test, monitoring |
| **Total Annual** | **£600K-£1.05M/year** | |

---

## Approval

### Requirements Review

| Reviewer | Role | Status | Date | Comments |
|----------|------|--------|------|----------|
| GDS Director of Technology | Executive Sponsor | [ ] Approved | [PENDING] | |
| GDS Service Owner | Product Owner | [ ] Approved | [PENDING] | |
| Enterprise Architect | Architecture | [ ] Approved | [PENDING] | |
| NCSC Advisor | Security | [ ] Approved | [PENDING] | |
| ICO Engagement Lead | Data Protection | [ ] Approved | [PENDING] | |
| Department API Owner Rep | Integration Partner | [ ] Approved | [PENDING] | |

### Sign-Off

By signing below, stakeholders confirm that requirements are complete, understood, and approved to proceed to design phase.

| Stakeholder | Signature | Date |
|-------------|-----------|------|
| GDS Director of Technology | _________ | [PENDING] |
| Senior Responsible Owner | _________ | [PENDING] |
| Enterprise Architect | _________ | [PENDING] |

---

## Appendices

### Appendix A: Glossary

| Term | Definition |
|------|-----------|
| API | Application Programming Interface — a set of protocols for building and integrating software |
| Aggregator | A platform that provides unified access to multiple APIs from different sources |
| Adapter | A component that translates between the platform's internal interface and a specific upstream API |
| Circuit Breaker | A resilience pattern that stops requests to a failing service to prevent cascade failures |
| GDS | Government Digital Service — the UK Government's digital transformation unit |
| MoU | Memorandum of Understanding — a bilateral agreement between GDS and a department |
| NCSC | National Cyber Security Centre — the UK's technical authority for cyber security |
| TCoP | Technology Code of Practice — UK Government standards for technology decisions |
| Upstream API | A government department API that the aggregator routes requests to |
| DPIA | Data Protection Impact Assessment — required under UK GDPR Article 35 |

### Appendix B: Reference Documents

- ARC-000-PRIN-v1.0 — Architecture Principles
- ARC-001-STKE-v1.0 — Stakeholder Drivers & Goals Analysis
- UK Government Technology Code of Practice
- GDS Service Standard (14 points)
- NCSC Cloud Security Principles
- api.gov.uk — existing UK Government API catalogue
- OWASP API Security Top 10

---

**Generated by**: ArcKit `/arckit.requirements` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.1.0
**Project**: UK Government API Aggregator (Project 001)
**AI Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
**Generation Context**: Generated from stakeholder analysis (ARC-001-STKE-v1.0), architecture principles (ARC-000-PRIN-v1.0), and user input describing API aggregation across UK Government departments.
