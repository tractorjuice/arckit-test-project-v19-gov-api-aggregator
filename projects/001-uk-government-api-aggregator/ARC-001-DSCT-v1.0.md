# Data Source Discovery: UK Government API Aggregator

> **Template Status**: Alpha | **Version**: 1.0.0 | **Command**: `/arckit.datascout`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-DSCT-v1.0 |
| **Document Type** | Data Source Discovery |
| **Project** | UK Government API Aggregator (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-02-01 |
| **Last Modified** | 2026-02-01 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-01 |
| **Owner** | Platform Architecture Team |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project Team, GDS Leadership, Department API Owners |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-01 | ArcKit AI | Initial creation from `/arckit.datascout` command | PENDING | PENDING |
| 1.1 | 2026-02-01 | ArcKit AI | Added Appendix C: Government APIs not listed on api.gov.uk (border, fuel, legislation, police, carbon, ONS, DfE, TfL, devolved) | PENDING | PENDING |

---

## Executive Summary

### Data Needs Overview

This document presents data source discovery findings for the **UK Government API Aggregator** project, identifying government APIs, datasets, and data portals across UK Government departments that can fulfil the data and integration requirements documented in `ARC-001-REQ-v1.0.md`.

**Requirements Analyzed**: 5 data requirements (DR-xxx), 16 functional requirements (FR-xxx), 9 integration requirements (INT-xxx), 22 non-functional requirements (NFR-xxx)

**Data Source Categories Identified**: 9 categories based on department API ecosystems

**Discovery Approach**: UK Government API catalogue (api.gov.uk), department developer hubs, WebSearch-powered research across all 34 departments listed in the cross-government API catalogue

### Key Findings

- **240 APIs identified** across 34 departments in the official api.gov.uk catalogue, maintained by the Central Digital and Data Office (CDDO) on GitHub
- **NHS Digital dominates** with 93 APIs (39% of all catalogued APIs), followed by HMRC (31), HM Land Registry (13), MHCLG (12), Environment Agency (10), and DWP (10)
- **Authentication varies widely**: from open data (no auth) for Environment Agency, to API keys (Companies House, DVLA, OS), to OAuth 2.0 (HMRC, NHS Digital, DWP), requiring the gateway to support multiple auth patterns
- **Phase 1 integration targets are well-supported**: HMRC, Companies House, DVLA, Environment Agency, and Ordnance Survey all have mature developer hubs with REST APIs and comprehensive documentation
- **Clinical NHS APIs require enhanced governance**: 93 NHS APIs include both open reference data and controlled patient-data APIs requiring NHS Identity, IG Model compliance, and DPIA

### Data Source Summary

| Source Type | Count | Cost Range | Key Providers |
|-------------|-------|------------|---------------|
| **UK Government Open Data** | ~120 | Free (OGL v3.0) | Environment Agency, GDS, NHS (reference data), MHCLG, data.gov.uk |
| **Government APIs (Free, Auth Required)** | ~90 | Free (registration) | HMRC, Companies House, DVLA, DWP, HM Land Registry, MOJ |
| **Government APIs (Commercial/Controlled)** | ~25 | £0–£12,000/year | Ordnance Survey (premium tiers), NHS Digital (clinical APIs) |
| **Cross-Government Metadata** | 1 | Free (GitHub) | CDDO api.gov.uk catalogue (CSV on GitHub) |
| **TOTAL** | **~240** | **£0–£12,000/year** | **34 departments** |

### Top Recommended Sources

**Shortlist for Phase 1 integration**:

1. **api.gov.uk Catalogue (CDDO)** for API Discovery: Open CSV on GitHub, 240 API listings, 87/100
2. **HMRC Developer Hub** for Tax & Revenue APIs: 31 APIs, OAuth 2.0, excellent documentation, 85/100
3. **Companies House Developer Hub** for Company Data: REST + Streaming APIs, free API key, 84/100
4. **Environment Agency APIs** for Environmental Data: 10 APIs, fully open (no auth), OGL licence, 82/100
5. **DVLA Developer Portal** for Vehicle & Driver Data: VES API + Driver View, API key auth, 80/100

### Requirements Coverage

- ✅ **7 integration requirements (78%)** fully matched to external data sources with mature APIs
- ⚠️ **1 integration requirement (11%)** partially matched (DWP — APIs exist but access is controlled)
- ✅ **1 integration requirement (11%)** matched (api.gov.uk catalogue — CSV data on GitHub)

---

## Data Needs Analysis

> **Note**: Data needs are extracted from requirements, categorised by type, with criticality and volume/freshness expectations.

### Extracted Data Needs

| # | Requirement ID | Data Need | Type | Criticality | Volume | Freshness | Source Category |
|---|----------------|-----------|------|-------------|--------|-----------|-----------------|
| 1 | INT-001 | HMRC Tax APIs (VAT, SA, CT, Customs) | Integration | MUST | 200 req/s peak | Real-time proxy | Tax & Revenue |
| 2 | INT-002 | Companies House (company search, filings, officers) | Integration | MUST | 100 req/s peak | Real-time proxy + streaming | Company Data |
| 3 | INT-003 | DVLA (vehicle enquiry, MOT, driving licence) | Integration | MUST | 50 req/s peak | Real-time proxy | Vehicle & Driver |
| 4 | INT-004 | NHS Digital (ODS, reference data, clinical APIs) | Integration | SHOULD | 100 req/s peak | Real-time proxy | Health |
| 5 | INT-005 | Environment Agency (flood, water quality, rainfall) | Integration | MUST | 50 req/s peak | Real-time (15-min updates) | Environmental |
| 6 | INT-006 | Ordnance Survey (Places, Maps, Features, NGD) | Integration | SHOULD | 100 req/s peak | Real-time proxy | Geospatial |
| 7 | INT-007 | HM Land Registry (property, title, price paid) | Integration | SHOULD | 30 req/s peak | Real-time proxy | Property |
| 8 | INT-008 | DWP (benefits status, eligibility) | Integration | COULD | 20 req/s peak | Real-time proxy | Benefits |
| 9 | INT-009 | api.gov.uk catalogue metadata | Integration | MUST | Batch import | Daily sync | Catalogue |
| 10 | FR-001 | API catalogue discovery & crawling | Functional | MUST | ~500 records | Daily refresh | All departments |
| 11 | FR-005 | Gateway routing to upstream APIs | Functional | MUST | 5,000 req/s peak | Real-time | All departments |
| 12 | FR-006 | Response normalisation across departments | Functional | MUST | Per-request | Real-time | All departments |

### Data Needs by Category

**Category 1: Tax & Revenue (HMRC)**
- Requirements: INT-001, FR-005, FR-006
- Data fields needed: VAT returns, Self Assessment submissions, Corporation Tax, Customs declarations, National Insurance
- Volume: 200 req/s peak during tax deadlines
- Freshness: Real-time API proxy
- Quality threshold: 100% accuracy (financial/legal data)

**Category 2: Company Data (Companies House)**
- Requirements: INT-002, FR-005, FR-006
- Data fields needed: Company search, filing history, officers, charges, PSC, insolvency
- Volume: 100 req/s peak; streaming for real-time updates
- Freshness: Real-time + streaming API for filings
- Quality threshold: 99.9% accuracy

**Category 3: Vehicle & Driver (DVLA/DVSA)**
- Requirements: INT-003, FR-005, FR-006
- Data fields needed: Vehicle registration lookup, tax/MOT status, driver licence verification
- Volume: 50 req/s peak
- Freshness: Real-time proxy
- Quality threshold: 100% accuracy (safety-critical)

**Category 4: Health (NHS Digital)**
- Requirements: INT-004, FR-005, FR-006
- Data fields needed: Organisation Data Service, reference data (Phase 1); PDS, EPS, GP Connect (Phase 2)
- Volume: 100 req/s peak
- Freshness: Real-time proxy
- Quality threshold: 100% accuracy for clinical; 99% for reference

**Category 5: Environmental (Environment Agency)**
- Requirements: INT-005, FR-005, FR-006
- Data fields needed: Flood warnings, river levels, water quality, bathing water, rainfall
- Volume: 50 req/s peak
- Freshness: Data updated every 15 minutes by EA
- Quality threshold: 95% (sensor data with known limitations)

**Category 6: Geospatial (Ordnance Survey)**
- Requirements: INT-006, FR-005, FR-006
- Data fields needed: Address lookup, map tiles, features, NGD data
- Volume: 100 req/s peak
- Freshness: Real-time proxy; data updated periodically by OS
- Quality threshold: 99.9% positional accuracy

**Category 7: Property (HM Land Registry)**
- Requirements: INT-007, FR-005, FR-006
- Data fields needed: Title searches, price paid, local land charges, official copies
- Volume: 30 req/s peak
- Freshness: Real-time proxy
- Quality threshold: 100% (legal records)

**Category 8: Benefits (DWP)**
- Requirements: INT-008, FR-005, FR-006
- Data fields needed: Benefits status, eligibility checking, address lookup
- Volume: 20 req/s peak
- Freshness: Real-time proxy
- Quality threshold: 100% (personal benefit data)

**Category 9: API Catalogue Metadata (CDDO)**
- Requirements: INT-009, FR-001
- Data fields needed: API names, departments, descriptions, URLs, status
- Volume: ~240 records, batch
- Freshness: Daily sync from GitHub CSV
- Quality threshold: 95% (community-maintained)

---

## Data Source Discovery

> **Note**: Categories are dynamically identified from project requirements and the UK Government department landscape.

---

## Category 1: Tax & Revenue — HMRC

**Requirements Addressed**: INT-001, FR-005, FR-006, FR-012, FR-013

**Why This Category**: HMRC manages the UK's tax system and provides the most critical government APIs for businesses and tax software providers. The Making Tax Digital programme has driven extensive API development.

**Data Fields Needed**: VAT obligations/returns, Self Assessment submissions/calculations, Corporation Tax, Customs declarations, National Insurance records, Fraud Prevention Headers

---

### Source 1A: HMRC Developer Hub APIs

**Provider**: HM Revenue & Customs, https://developer.service.hmrc.gov.uk/api-documentation

**Description**: HMRC's Developer Hub provides access to 31 REST APIs covering tax, customs, and national insurance services. The hub supports sandbox and production environments, with OAuth 2.0 authentication for user-restricted APIs and server token auth for application-restricted endpoints.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 (API access); data subject to HMRC terms |
| **Pricing** | Free (registration required) |
| **Format** | JSON (REST APIs) |
| **API Endpoint** | https://api.service.hmrc.gov.uk |
| **Authentication** | OAuth 2.0 (user-restricted), Server Token (application-restricted) |
| **Rate Limits** | Per-application limits; burst protection |
| **Update Frequency** | Real-time (API responses reflect current state) |
| **Coverage** | UK-wide (HMRC jurisdiction) |
| **Temporal Coverage** | Varies by API; tax years from 2017-18 onwards for MTD |
| **Data Quality** | Excellent — authoritative source for tax data |
| **Documentation** | https://developer.service.hmrc.gov.uk/api-documentation/docs/api — Excellent |
| **SLA** | Published HMRC service levels; no explicit API SLA |
| **GDPR Status** | Contains PII (taxpayer data) — access controlled per consumer |
| **UK Data Residency** | Yes — HMRC data held in UK |

**Key APIs (31 total)**:
- **VAT (MTD) API** — Submit/view VAT returns, obligations, payments, liabilities
- **Self Assessment APIs (MTD)** — Income, expenses, tax calculations, submissions (multiple APIs)
- **Corporation Tax API** — Company tax submissions and calculations
- **Customs Declarations API** — Import/export declarations via CDS
- **National Insurance API** — NI contributions and liability
- **GOV.UK Trade Tariff API** — Commodity code lookups
- **Fraud Prevention Headers API** — Required header validation for all MTD-connected software
- **Business Details API** — Business income source details
- **Individual Calculations API** — Tax calculation trigger and retrieval

**Requirements Fit**:
- ✅ Covers: VAT, Self Assessment, Corporation Tax, Customs, NI — all core HMRC integrations
- ✅ OAuth 2.0 and server token patterns well-documented
- ⚠️ Partial: Some older APIs still use XML; majority now JSON/REST
- ❌ Missing: No single "list all HMRC APIs" endpoint — must be catalogued manually

**Integration Approach**:
- **Pattern**: Real-time API proxying via gateway adapter
- **Estimated Effort**: 15 person-days (adapter + OAuth flow + sandbox testing)
- **Dependencies**: HMRC Developer Hub registration, OAuth 2.0 client credentials, Fraud Prevention Headers compliance

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 9/10 | 22.5/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 9/10 | 13.5/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 9/10 | 13.5/15 |
| Reliability | 10% | 7/10 | 7/10 |
| **Total** | **100%** | | **88.5/100** |

---

## Category 2: Company Data — Companies House

**Requirements Addressed**: INT-002, FR-005, FR-006

**Why This Category**: Companies House is the UK's registrar of companies, providing essential company data used by financial services, legal, and public sector organisations.

**Data Fields Needed**: Company search, registered details, filing history, officers, persons with significant control (PSC), charges, insolvency

---

### Source 2A: Companies House API & Streaming API

**Provider**: Companies House, https://developer.company-information.service.gov.uk/

**Description**: Companies House provides a REST API for on-demand company data queries and a Streaming API for real-time change notifications. The streaming API pushes data changes as they happen through long-running HTTP connections, covering companies, filings, officers, PSCs, charges, insolvency cases, and disqualified officers.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | Free (API key registration required) |
| **Format** | JSON (REST API); JSON streaming (Streaming API) |
| **API Endpoint** | https://api.company-information.service.gov.uk (REST); https://stream.companieshouse.gov.uk (Streaming) |
| **Authentication** | API Key (HTTP Basic with key as username) |
| **Rate Limits** | 600 requests per 5 minutes per API key |
| **Update Frequency** | REST: real-time queries; Streaming: real-time push on data change |
| **Coverage** | UK-wide (England, Wales, Scotland, Northern Ireland companies) |
| **Temporal Coverage** | Companies registered from 1844 to present |
| **Data Quality** | Excellent — authoritative register of UK companies |
| **Documentation** | https://developer-specs.company-information.service.gov.uk/ — Good |
| **SLA** | Beta service; no formal SLA published |
| **GDPR Status** | Contains director/PSC names and addresses (public register data) |
| **UK Data Residency** | Yes |

**Streaming API Endpoints**:
- `/companies` — Real-time company profile changes
- `/filings` — New filing events
- `/officers` — Officer appointment/resignation events
- `/persons-with-significant-control` — PSC changes
- `/charges` — Charge creation/satisfaction events
- `/insolvency-cases` — Insolvency proceedings
- `/disqualified-officers` — Disqualification events

**Requirements Fit**:
- ✅ Covers: Company search, filing history, officers, PSC, charges, insolvency
- ✅ Streaming API enables real-time catalogue updates for company-related APIs
- ⚠️ Partial: Shareholder information not available via API (only from filed documents)
- ❌ Missing: Bulk data downloads require separate process

**Integration Approach**:
- **Pattern**: REST API proxy + Streaming API consumer for real-time updates
- **Estimated Effort**: 10 person-days (REST adapter + streaming consumer)
- **Dependencies**: API key registration (self-service, instant)

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 9/10 | 22.5/25 |
| Data Quality | 20% | 9/10 | 18/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 9/10 | 13.5/15 |
| Reliability | 10% | 7/10 | 7/10 |
| **Total** | **100%** | | **88/100** |

---

## Category 3: Vehicle & Driver — DVLA / DVSA

**Requirements Addressed**: INT-003, FR-005, FR-006

**Why This Category**: DVLA and DVSA provide vehicle registration, tax/MOT status, and driving licence data critical for transport, insurance, and logistics sectors.

**Data Fields Needed**: Vehicle registration details, tax status, MOT status, CO2 emissions, driver licence verification

---

### Source 3A: DVLA Vehicle Enquiry Service (VES) API

**Provider**: Driver and Vehicle Licensing Agency (DVLA), https://developer-portal.driver-vehicle-licensing.api.gov.uk/

**Description**: The Vehicle Enquiry Service API returns vehicle details for a given registration number, including make, model, colour, tax status, MOT status, CO2 emissions, fuel type, and engine capacity.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Crown Copyright; DVLA terms of use |
| **Pricing** | Free (API key required; one key per organisation) |
| **Format** | JSON (REST API) |
| **API Endpoint** | https://driver-vehicle-licensing.api.gov.uk/vehicle-enquiry/v1/vehicles |
| **Authentication** | API Key (x-api-key header) |
| **Rate Limits** | Per-plan basis; rate limited per second and per day |
| **Update Frequency** | Real-time (reflects current DVLA records) |
| **Coverage** | UK-wide (GB and NI registered vehicles) |
| **Temporal Coverage** | Current vehicle data |
| **Data Quality** | Excellent — authoritative vehicle register |
| **Documentation** | https://developer-portal.driver-vehicle-licensing.api.gov.uk/ — Good |
| **SLA** | No published SLA; high availability observed |
| **GDPR Status** | Vehicle registration numbers are ICO-sensitive |
| **UK Data Residency** | Yes |

**Requirements Fit**:
- ✅ Covers: Vehicle details, tax status, MOT status, emissions data
- ⚠️ Partial: Only one API key per organisation — limits multi-tenant gateway model
- ❌ Missing: Full MOT history (separate DVSA API, see below)

---

### Source 3B: DVSA MOT History API

**Provider**: Driver and Vehicle Standards Agency (DVSA), https://dvsa.github.io/mot-history-api-documentation/

**Description**: Provides access to MOT test history for vehicles, including pass/fail results, advisory notices, and defects. Note: The original API was deprecated 1 September 2025; a new version is available.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | Free (registration required) |
| **Format** | JSON |
| **Authentication** | API Key |
| **Coverage** | UK-wide |

---

### Source 3C: DVLA Driver View API

**Provider**: DVLA, https://developer-portal.driver-vehicle-licensing.api.gov.uk/

**Description**: Retrieves driving licence details, optionally including CPC and tachograph data. Requires enhanced authentication (JWT + API Key).

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Crown Copyright; DVLA Secure API terms |
| **Pricing** | Free (enhanced onboarding required) |
| **Format** | JSON |
| **API Endpoint** | https://driver-vehicle-licensing.api.gov.uk/full-driver-enquiry |
| **Authentication** | JWT Token + API Key (Secure API) |
| **Rate Limits** | Per-plan basis |
| **GDPR Status** | Contains PII (driving licence holder data) — Secure API |

**Combined DVLA/DVSA Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 8/10 | 20/25 |
| Data Quality | 20% | 9/10 | 18/20 |
| License & Cost | 15% | 9/10 | 13.5/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 8/10 | 12/15 |
| Reliability | 10% | 7/10 | 7/10 |
| **Total** | **100%** | | **81/100** |

---

## Category 4: Health — NHS Digital

**Requirements Addressed**: INT-004, FR-005, FR-006

**Why This Category**: NHS Digital (now part of NHS England) provides the largest number of government APIs (93), spanning clinical, reference, and administrative health data.

**Data Fields Needed**: Organisation Data Service (ODS), reference data, electronic prescriptions, GP Connect, Personal Demographics Service

---

### Source 4A: NHS Digital API Catalogue (93 APIs)

**Provider**: NHS England Digital, https://digital.nhs.uk/developer/api-catalogue

**Description**: The largest single collection of UK Government APIs, covering health and care data. APIs range from open reference data to controlled clinical APIs requiring NHS Identity and IG Model compliance.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Mixed: OGL v3.0 (reference data), NHS-specific terms (clinical APIs) |
| **Pricing** | Free (registration and IG compliance required for controlled APIs) |
| **Format** | JSON/FHIR (HL7 FHIR R4 for newer APIs); HL7 V3 (legacy); EDIFACT (some) |
| **API Endpoint** | Various: https://api.service.nhs.uk (newer APIs), Spine (legacy) |
| **Authentication** | Open (some reference), API Key, OAuth 2.0, NHS CIS2 Identity |
| **Rate Limits** | Per-API basis |
| **Update Frequency** | Real-time for clinical; periodic for reference data |
| **Coverage** | England (primary); some UK-wide |
| **Data Quality** | Excellent — authoritative NHS records |
| **Documentation** | https://digital.nhs.uk/developer — Excellent |
| **SLA** | Tiered: Bronze, Silver, Gold, Platinum (24/7 for EPS) |
| **GDPR Status** | Many APIs contain patient PII — strict IG controls |
| **UK Data Residency** | Yes — NHS data sovereignty |

**Key API Groups**:

**Open/Reference APIs (Phase 1 candidates)**:
- Organisation Data Service (ODS) — NHS organisation lookups
- NHS Service Search — Find NHS services
- Cyber Alerts API — Security advisories
- Data Registers Service — Reference data

**Clinical APIs (Phase 2, controlled access)**:
- Personal Demographics Service (PDS) FHIR API — Patient demographics
- Electronic Prescription Service (EPS) FHIR API — E-prescriptions
- GP Connect APIs — Appointment management, access records
- Summary Care Record — Patient clinical summaries
- e-Referral Service — Clinical referrals
- Digital Medicine FHIR — Medicine dispensing notifications
- Booking and Referral FHIR — 111/UTC booking

**Requirements Fit**:
- ✅ Covers: 93 APIs across all NHS data domains
- ✅ Modern FHIR R4 standard for newer APIs
- ⚠️ Partial: Clinical APIs require NHS IG Model compliance and DPIA
- ⚠️ Partial: Legacy HL7 V3 APIs being migrated to FHIR (e.g., EPS HL7v3 retiring March 2027)
- ❌ Missing: Some APIs England-only; Scotland/Wales/NI have separate systems

**Integration Approach**:
- **Pattern**: Phased — Phase 1: open/reference APIs; Phase 2: clinical with IG compliance
- **Estimated Effort**: 8 person-days (Phase 1 reference APIs); 25 person-days (Phase 2 clinical)
- **Dependencies**: NHS Identity onboarding, IG Model compliance, DPIA for clinical APIs

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 9/10 | 22.5/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 7/10 | 10.5/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 6/10 | 9/15 |
| Reliability | 10% | 8/10 | 8/10 |
| **Total** | **100%** | | **82/100** |

---

## Category 5: Environmental — Environment Agency

**Requirements Addressed**: INT-005, FR-005, FR-006

**Why This Category**: The Environment Agency provides open environmental data including real-time flood monitoring, water quality, bathing water quality, and rainfall data — all freely available without authentication.

**Data Fields Needed**: Flood warnings/alerts, river levels, water quality, bathing water, rainfall measurements

---

### Source 5A: Environment Agency Real-Time Flood Monitoring API

**Provider**: Environment Agency, https://environment.data.gov.uk/flood-monitoring/doc/reference

**Description**: Provides near real-time flood monitoring data including water levels (updated every 15 minutes), flood warnings and alerts, monitoring station information, and 3-day flood risk forecasts. Fully open data with no authentication required.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | Free — no registration required |
| **Format** | JSON (default), RDF/XML, Turtle, CSV |
| **API Endpoint** | https://environment.data.gov.uk/flood-monitoring |
| **Authentication** | None (fully open) |
| **Rate Limits** | Fair use; recommended max 4 calls/hour for latest readings |
| **Update Frequency** | Every 15 minutes (water levels), near real-time (warnings) |
| **Coverage** | England (EA jurisdiction) |
| **Temporal Coverage** | Real-time data; historical archive via Hydrology API |
| **Data Quality** | Good — sensor data with known limitations (beta API) |
| **Documentation** | https://environment.data.gov.uk/flood-monitoring/doc/reference — Good |
| **SLA** | No guarantee of service level; not for safety-critical use |
| **GDPR Status** | No personal data |
| **UK Data Residency** | Yes |

**Additional EA APIs (10 total on api.gov.uk)**:
- Flood Monitoring API (warnings, levels, stations)
- Water Quality Archive API
- Bathing Water Quality API
- Rainfall API
- Ecology & Fish Data API
- Hydrology Archive API (newer — billions of historical readings)

**Requirements Fit**:
- ✅ Covers: Flood warnings, river levels, rainfall, water quality, bathing water
- ✅ Fully open — simplest integration of all department APIs
- ⚠️ Partial: England-only coverage (SEPA covers Scotland, NRW covers Wales)
- ⚠️ Partial: Beta API — no SLA, not for safety-critical applications

**Integration Approach**:
- **Pattern**: Direct REST API proxy; optional caching with 15-min TTL
- **Estimated Effort**: 5 person-days (simplest adapter — no auth)
- **Dependencies**: None (open access)

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 8/10 | 20/25 |
| Data Quality | 20% | 7/10 | 14/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 6/10 | 6/10 |
| **Total** | **100%** | | **80.5/100** |

---

## Category 6: Geospatial — Ordnance Survey

**Requirements Addressed**: INT-006, FR-005, FR-006

**Why This Category**: Ordnance Survey is the UK's national mapping agency, providing authoritative geospatial data essential for address lookup, mapping, and location-based services.

**Data Fields Needed**: Address lookup/geocoding, map tiles, building/road features, National Geographic Database

---

### Source 6A: Ordnance Survey Data Hub APIs

**Provider**: Ordnance Survey, https://osdatahub.os.uk/

**Description**: The OS Data Hub provides access to OS datasets through a suite of APIs and data downloads. Offers both free (OpenData) and premium tiers, with public sector organisations eligible for free premium access via the PSMA (Public Sector Mapping Agreement).

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL v3.0 (OpenData); OS commercial licence (Premium); PSMA (public sector) |
| **Pricing** | Free: OpenData plan + £1,000/month free premium transactions; Premium: commercial pricing |
| **Format** | JSON, GeoJSON, Vector Tiles, Raster Tiles |
| **API Endpoint** | https://api.os.uk |
| **Authentication** | API Key (OS Data Hub project key) |
| **Rate Limits** | Transaction-based; OpenData unlimited; Premium metered |
| **Update Frequency** | Varies: OS MasterMap updated 6-weekly; OS OpenData updated periodically |
| **Coverage** | Great Britain (England, Scotland, Wales); Northern Ireland via LPS |
| **Data Quality** | Excellent — sub-metre positional accuracy |
| **Documentation** | https://docs.os.uk — Excellent |
| **SLA** | 99.9% uptime for premium plans |
| **GDPR Status** | No personal data |
| **UK Data Residency** | Yes |

**Key APIs**:
- **OS Places API** — Address geocoding/reverse geocoding (UPRN-based)
- **OS Maps API** — Raster map tiles for web/mobile
- **OS Vector Tile API** — Customisable vector basemaps
- **OS NGD API** — Next-generation features API (OGC-compliant GeoJSON)
- **OS Features API** — Buildings, roads, rivers, greenspaces (being superseded by NGD)

**Developer Tools**: Python SDK (`osdatahub`), JavaScript SDK (`osdatahub-js`)

**Requirements Fit**:
- ✅ Covers: Address lookup, map tiles, features, NGD data
- ✅ Public sector organisations get free premium access via PSMA
- ⚠️ Partial: Commercial licensing for premium data may limit third-party passthrough
- ⚠️ Partial: GB only — Northern Ireland requires separate data source

**Integration Approach**:
- **Pattern**: API proxy with caching for map tiles (long TTL); direct proxy for Places
- **Estimated Effort**: 10 person-days (adapter + PSMA licence negotiation)
- **Dependencies**: OS Data Hub registration, PSMA agreement for public sector access

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 8/10 | 20/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 7/10 | 10.5/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 9/10 | 13.5/15 |
| Reliability | 10% | 8/10 | 8/10 |
| **Total** | **100%** | | **85.5/100** |

---

## Category 7: Property — HM Land Registry

**Requirements Addressed**: INT-007, FR-005, FR-006

**Why This Category**: HM Land Registry holds the definitive register of property ownership in England and Wales, providing data critical for conveyancing, financial services, and property-related services.

**Data Fields Needed**: Title searches, price paid data, local land charges, official copies, ownership verification

---

### Source 7A: HM Land Registry Business Gateway APIs

**Provider**: HM Land Registry, https://landregistry.github.io/bg-dev-pack-redesign/

**Description**: HMLR provides 13 APIs through its Business Gateway, supporting property searches, title enquiries, official copies, and the new Digital Registration Service (DRS). In November 2025, HMLR launched new RESTful APIs replacing legacy SOAP services.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Crown Copyright; HMLR terms of use |
| **Pricing** | Per-transaction fees for searches (£2-£7 per search); some open data free |
| **Format** | JSON (new REST APIs), XML (legacy SOAP) |
| **API Endpoint** | Business Gateway (requires registration and contract) |
| **Authentication** | API Key + Certificate (mutual TLS for some services) |
| **Rate Limits** | Per-agreement basis |
| **Update Frequency** | Real-time (register reflects current state) |
| **Coverage** | England and Wales (Scotland: Registers of Scotland; NI: LPS) |
| **Data Quality** | Authoritative — definitive property register |
| **Documentation** | https://landregistry.github.io/bg-dev-pack-redesign/ — Good |
| **SLA** | Business hours support; high availability |
| **GDPR Status** | Contains property owner PII |
| **UK Data Residency** | Yes |

**Key Services**:
- Title Number Search (by address)
- Official Copy of Register
- Official Search of Whole (with priority)
- Local Land Charges Search
- Digital Registration Service (DRS) — new REST API
- Ownership Verification

**Requirements Fit**:
- ✅ Covers: Property search, title enquiry, price paid, local land charges
- ✅ New REST APIs (Nov 2025) modernise the integration experience
- ⚠️ Partial: Per-transaction fees add cost at scale
- ⚠️ Partial: Business Gateway onboarding requires contract negotiation

**Integration Approach**:
- **Pattern**: REST API proxy for new APIs; legacy SOAP adapter for older services
- **Estimated Effort**: 12 person-days (REST adapter + SOAP adapter + contract negotiation)
- **Dependencies**: Business Gateway registration, commercial agreement, certificate provisioning

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 8/10 | 20/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 5/10 | 7.5/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 8/10 | 12/15 |
| Reliability | 10% | 8/10 | 8/10 |
| **Total** | **100%** | | **78/100** |

---

## Category 8: Benefits — DWP

**Requirements Addressed**: INT-008, FR-005, FR-006

**Why This Category**: DWP manages welfare and pension services, transacting £212 billion annually. APIs handle sensitive benefit and eligibility data.

**Data Fields Needed**: Benefits status, eligibility checking, address lookup

---

### Source 8A: DWP APIs

**Provider**: Department for Work and Pensions, https://www.api.gov.uk/dwp/

**Description**: DWP has 10 APIs in the government catalogue, primarily internal/cross-government. These handle highly sensitive personal benefit data and require enhanced access controls. DWP is undergoing significant modernisation with cloud migration (Oracle Cloud Infrastructure) and contact centre transformation.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Restricted — cross-government access only for most APIs |
| **Pricing** | Free (but access restricted to authorised consumers) |
| **Format** | JSON |
| **Authentication** | OAuth 2.0 with enhanced access controls |
| **Rate Limits** | Per-agreement basis |
| **Coverage** | UK-wide |
| **Data Quality** | Authoritative — official benefit records |
| **Documentation** | Limited public documentation |
| **GDPR Status** | Highly sensitive PII — benefit records, eligibility, personal circumstances |

**Available APIs (10 listed)**:
- Address Lookup (Location Service)
- Care Homes Information Service
- Citizen API
- Citizen Benefit Relationships
- FINDr Matching Service
- GOV.UK Notify
- Get Interest Details
- Maintain Interest Details
- Organisations
- Subscription Service API

**Requirements Fit**:
- ✅ Covers: Address lookup, benefit relationships, citizen data
- ⚠️ Partial: Most APIs are cross-government only — not for public developer consumption
- ❌ Missing: No public developer hub; access requires formal data-sharing agreements
- ❌ Missing: Benefit status and eligibility checking APIs not publicly available

**Integration Approach**:
- **Pattern**: Cross-government API integration with formal data-sharing agreement
- **Estimated Effort**: 20 person-days (negotiation + IG compliance + adapter)
- **Dependencies**: Formal data-sharing agreement with DWP, DPIA, IG compliance

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 5/10 | 12.5/25 |
| Data Quality | 20% | 9/10 | 18/20 |
| License & Cost | 15% | 5/10 | 7.5/15 |
| API Quality | 15% | 5/10 | 7.5/15 |
| Compliance | 15% | 4/10 | 6/15 |
| Reliability | 10% | 6/10 | 6/10 |
| **Total** | **100%** | | **57.5/100** |

---

## Category 9: API Catalogue Metadata — CDDO

**Requirements Addressed**: INT-009, FR-001

**Why This Category**: The cross-government API catalogue at api.gov.uk, maintained by the Central Digital and Data Office (CDDO), is the canonical source for bootstrapping the platform's API directory.

**Data Fields Needed**: API names, descriptions, department names, URLs, documentation links, status

---

### Source 9A: CDDO api.gov.uk Catalogue (GitHub CSV)

**Provider**: Central Digital and Data Office (CDDO), https://github.com/co-cddo/api-catalogue

**Description**: The official cross-government API catalogue, maintained as a CSV file on GitHub. Contains metadata for 240 APIs across 34 departments. The CSV at `data/catalogue.csv` is the authoritative data source for the api.gov.uk website.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | Free (open on GitHub) |
| **Format** | CSV (structured data); GitHub API for programmatic access |
| **API Endpoint** | https://raw.githubusercontent.com/co-cddo/api-catalogue/main/data/catalogue.csv |
| **Authentication** | None (public GitHub repo) |
| **Rate Limits** | GitHub API rate limits (60/hour unauthenticated, 5000/hour authenticated) |
| **Update Frequency** | Community-maintained; updated via GitHub Issues/PRs |
| **Coverage** | UK-wide — all public sector organisations |
| **Data Quality** | Good — community-maintained with CDDO oversight |
| **Documentation** | GitHub README — Fair |
| **GDPR Status** | No personal data |

**Requirements Fit**:
- ✅ Covers: API names, departments, descriptions, URLs — bootstrap the platform catalogue
- ⚠️ Partial: Not all government APIs are listed (e.g., Home Office shows 0 APIs)
- ⚠️ Partial: Metadata may not include all fields needed (rate limits, auth methods, etc.)

**Integration Approach**:
- **Pattern**: Periodic batch import (daily cron job fetching CSV from GitHub)
- **Estimated Effort**: 3 person-days (CSV parser + data mapping + scheduled import)
- **Dependencies**: None (open access)

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 8/10 | 20/25 |
| Data Quality | 20% | 7/10 | 14/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 6/10 | 9/15 |
| Compliance | 15% | 10/10 | 15/15 |
| Reliability | 10% | 7/10 | 7/10 |
| **Total** | **100%** | | **80/100** |

---

## Additional Departments Discovered

Beyond the 9 integration requirements, the api.gov.uk catalogue reveals additional departments with APIs:

| Department | APIs | Key APIs | Phase |
|-----------|------|----------|-------|
| **Government Digital Service (GDS)** | 7 | Bank Holidays, GOV.UK Content, GOV.UK Notify, GOV.UK Pay, GOV.UK Search | Phase 1 |
| **Ministry of Housing, Communities & Local Government (MHCLG)** | 12 | Energy Performance Certificates (EPC), Open Data Communities | Phase 2 |
| **Historic England** | 6 | Heritage at Risk, Listed Buildings, Heritage Gateway | Phase 2 |
| **Ministry of Justice (MOJ)** | 4 | Courts & Tribunals, Prison API, HMPPS Auth | Phase 3 |
| **Department for Education (DfE)** | 4 | Get Information About Schools, Academies data | Phase 2 |
| **Department for Business and Trade (DBT)** | 6 | Trade tariffs, export data | Phase 2 |
| **Department for Transport (DfT)** | 1 | Transport data | Phase 3 |
| **Natural England** | 4 | MAGIC Map, designated sites | Phase 2 |
| **Food Standards Agency** | 3 | Food hygiene ratings | Phase 2 |
| **Office for National Statistics (ONS)** | 2 | Census, statistical data | Phase 2 |
| **Home Office** | 0 | None publicly listed | Future |

---

## Evaluation Matrix

### Overall Scoring Summary

| Category | Recommended Source | Type | Score | Annual Cost | Integration Effort |
|----------|-------------------|------|-------|-------------|-------------------|
| Tax & Revenue | HMRC Developer Hub | Gov API (Free) | 88.5/100 | £0 | 15 days |
| Company Data | Companies House API | Gov API (Free/OGL) | 88/100 | £0 | 10 days |
| Geospatial | Ordnance Survey Data Hub | Gov API (Free/Commercial) | 85.5/100 | £0–£12,000 | 10 days |
| Health | NHS Digital APIs | Gov API (Free/Controlled) | 82/100 | £0 | 8–33 days |
| Vehicle & Driver | DVLA/DVSA APIs | Gov API (Free) | 81/100 | £0 | 8 days |
| Environmental | Environment Agency APIs | Open Data | 80.5/100 | £0 | 5 days |
| API Catalogue | CDDO api.gov.uk | Open Data (GitHub) | 80/100 | £0 | 3 days |
| Property | HM Land Registry | Gov API (Paid) | 78/100 | £500–£5,000 | 12 days |
| Benefits | DWP APIs | Gov API (Restricted) | 57.5/100 | £0 | 20 days |
| **TOTAL** | | | **Avg: 80/100** | **£500–£17,000/year** | **91–116 days** |

### Evaluation Criteria Explained

| Criterion | Weight | What It Measures |
|-----------|--------|-----------------|
| **Requirements Fit** | 25% | Does the source cover the required data fields, scope, granularity, and volume? |
| **Data Quality** | 20% | Accuracy, completeness, consistency, timeliness, and known quality issues |
| **License & Cost** | 15% | License terms (OGL, CC, proprietary), pricing sustainability, total cost |
| **API Quality** | 15% | REST/GraphQL, documentation quality, SDKs, versioning, error handling, pagination |
| **Compliance** | 15% | GDPR, UK data residency, data classification, terms of use, DPA 2018 |
| **Reliability** | 10% | SLA, uptime history, vendor stability, community/support, track record |

---

## Data Integration Architecture

### Integration Patterns by Source

| Source | Pattern | Auth | Caching | Error Handling | Monitoring |
|--------|---------|------|---------|----------------|------------|
| HMRC | REST proxy | OAuth 2.0 / Server Token | No cache (financial data) | Circuit breaker (30s timeout, 3 retries) | Health check + latency |
| Companies House | REST proxy + Streaming consumer | API Key | 5-min TTL for search | Circuit breaker | Health check + stream status |
| DVLA | REST proxy | API Key (x-api-key) | 1-hour TTL (vehicle data) | Circuit breaker | Health check |
| NHS Digital | REST proxy (FHIR) | OAuth 2.0 / NHS CIS2 | No cache (clinical) | Circuit breaker | Health check + SLA monitoring |
| Environment Agency | REST proxy | None | 15-min TTL | Retry 3x | Health check + data freshness |
| Ordnance Survey | REST proxy | API Key | 24-hour TTL (map tiles) | Circuit breaker | Transaction metering |
| HM Land Registry | REST proxy | API Key + mTLS | No cache (legal data) | Circuit breaker | Health check + cost tracking |
| DWP | REST proxy | OAuth 2.0 (enhanced) | No cache (personal data) | Circuit breaker | Health check + audit logging |
| CDDO Catalogue | Batch import (daily) | None | Full dataset cached | Retry daily | Freshness check |

### Recommended Integration Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    API Gateway Layer                         │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐      │
│  │ Auth     │ │ Rate     │ │ Response │ │ Circuit  │      │
│  │ Manager  │ │ Limiter  │ │ Normalise│ │ Breaker  │      │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘      │
├─────────────────────────────────────────────────────────────┤
│                 Department Adapter Layer                     │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐  │
│  │ HMRC   │ │ CH     │ │ DVLA   │ │ NHS    │ │ EA     │  │
│  │Adapter │ │Adapter │ │Adapter │ │Adapter │ │Adapter │  │
│  └───┬────┘ └───┬────┘ └───┬────┘ └───┬────┘ └───┬────┘  │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐             │
│  │ OS     │ │ HMLR   │ │ DWP    │ │ CDDO   │             │
│  │Adapter │ │Adapter │ │Adapter │ │Importer│             │
│  └───┬────┘ └───┬────┘ └───┬────┘ └───┬────┘             │
├─────────────────────────────────────────────────────────────┤
│                    Cache Layer                               │
│  ┌────────────────────────────────────────────────────┐    │
│  │ Response cache (per-source TTL), Map tile cache,   │    │
│  │ Catalogue cache, Health status cache               │    │
│  └────────────────────────────────────────────────────┘    │
├─────────────────────────────────────────────────────────────┤
│                 Monitoring & Observability                   │
│  Health checks, Latency metrics, Error rates,              │
│  Data freshness, Transaction metering, Audit logs          │
└─────────────────────────────────────────────────────────────┘
```

### Authentication and Access

| Source | Auth Method | Credentials Required | Registration Process | Lead Time |
|--------|-----------|---------------------|---------------------|-----------|
| HMRC | OAuth 2.0 + Server Token | Client ID, Client Secret | Developer Hub self-service | 1-2 days (sandbox), 2-4 weeks (production) |
| Companies House | API Key | API Key | Self-service portal | Instant |
| DVLA VES | API Key | x-api-key | Email application | 1-2 weeks |
| DVLA Driver View | JWT + API Key | JWT credentials + API key | Formal onboarding | 4-8 weeks |
| NHS Digital (open) | API Key | API Key | Developer portal | 1-2 days |
| NHS Digital (clinical) | OAuth 2.0 + NHS CIS2 | NHS Identity credentials | Formal IG process | 8-16 weeks |
| Environment Agency | None | None | None required | Instant |
| Ordnance Survey | API Key | OS Data Hub project key | Self-service | Instant |
| HM Land Registry | API Key + mTLS | Business Gateway credentials | Contract application | 4-8 weeks |
| DWP | OAuth 2.0 (enhanced) | Cross-government credentials | Formal DSA | 12-24 weeks |
| CDDO Catalogue | None | None (optional GitHub token) | None required | Instant |

### Rate Limits and Capacity Planning

| Source | Rate Limit | Projected Usage (Year 1) | Headroom | Upgrade Option |
|--------|-----------|--------------------------|----------|---------------|
| HMRC | Per-app limits | 100 req/s peak | ~50% | Contact HMRC for elevation |
| Companies House | 600 req/5 min | 50 req/s peak | ~80% | N/A (fair use) |
| DVLA VES | Per-plan | 30 req/s peak | ~60% | Upgrade plan via DVLA |
| NHS Digital | Per-API | 50 req/s peak | ~50% | SLA tier upgrade |
| Environment Agency | Fair use | 20 req/s peak | ~90% | N/A (4 calls/hour for latest) |
| Ordnance Survey | Transaction-based | 50 req/s peak | ~70% | Premium plan |
| HM Land Registry | Per-agreement | 10 req/s peak | ~70% | Contract renegotiation |
| DWP | Per-agreement | 5 req/s peak | ~75% | DSA renegotiation |

---

## Data Utility Analysis

> **Note**: Most data sources have alternative and secondary uses beyond their primary requirement. Identifying these latent uses increases the strategic value of data investments.

### Utility by Source

| Source | Primary Use (Requirement) | Secondary Uses | Strategic Value | Combination Opportunities |
|--------|--------------------------|----------------|-----------------|--------------------------|
| HMRC APIs | INT-001: Tax API proxy | 1. Trade data analytics 2. Tax compliance dashboards | HIGH | Combines with CH for business compliance views |
| Companies House | INT-002: Company data proxy | 1. Due diligence tools 2. Corporate structure analysis 3. Real-time filing alerts | HIGH | Combines with HMRC for full business profile |
| DVLA/DVSA | INT-003: Vehicle data proxy | 1. Fleet management 2. Insurance risk assessment 3. Environmental analysis (emissions) | MEDIUM | Combines with OS for location-based vehicle data |
| NHS Digital | INT-004: Health data proxy | 1. Service finder apps 2. Healthcare workforce planning 3. Pharmacy locator | HIGH | Combines with OS Places for NHS service mapping |
| Environment Agency | INT-005: Environmental proxy | 1. Property flood risk assessment 2. Agricultural monitoring 3. Climate data | HIGH | Combines with HMLR + OS for property risk profiles |
| Ordnance Survey | INT-006: Geospatial proxy | 1. Location enrichment for all other datasets 2. Journey planning 3. Site analysis | HIGH | Cross-cuts all other sources for location context |
| HM Land Registry | INT-007: Property data proxy | 1. Property market analytics 2. Conveyancing automation 3. Planning applications | HIGH | Combines with EA + OS for full property intelligence |
| DWP | INT-008: Benefits proxy | 1. Local authority service integration 2. Eligibility pre-screening | MEDIUM | Combines with HMRC for full citizen financial picture |
| CDDO Catalogue | INT-009: API discovery | 1. Platform catalogue bootstrapping 2. API landscape analytics | MEDIUM | Foundation for all other integrations |

### Data Combination Opportunities

1. **Property Intelligence Platform**: Environment Agency (flood risk) + HM Land Registry (ownership, price paid) + Ordnance Survey (mapping, UPRN) → Comprehensive property risk and value assessment
2. **Business Compliance Dashboard**: HMRC (tax compliance) + Companies House (corporate structure, officers) + DWP (employer obligations) → Full business compliance picture
3. **Healthcare Service Finder**: NHS Digital (ODS, service search) + Ordnance Survey (OS Places, mapping) → Location-aware healthcare service discovery
4. **Environmental Monitoring Hub**: Environment Agency (flood, water quality, rainfall) + Ordnance Survey (mapping) + Natural England (designated sites) → Comprehensive environmental intelligence

---

## Gap Analysis

### Requirements Without Suitable Data Sources

**GAP-1**: INT-008 (DWP Benefits APIs) — Restricted Access
- **Data Need**: Real-time benefits status and eligibility checking for public developer consumption
- **Why No Source**: DWP APIs are restricted to cross-government use only; no public developer hub
- **Impact**: Cannot offer DWP benefit data through the public developer portal; limits local authority integration scenarios
- **Severity**: MEDIUM (COULD_HAVE requirement)
- **Recommended Action**: Negotiate formal data-sharing agreement with DWP Digital; explore GOV.UK One Login as auth bridge; defer to Phase 2/3
- **Estimated Effort**: 20 person-days (negotiation + compliance)
- **Cost Estimate**: £0 (staff time only)

**GAP-2**: Home Office APIs — No Public APIs Listed
- **Data Need**: Immigration, passport, and policing data APIs
- **Why No Source**: Home Office lists 0 APIs in the public catalogue despite being a major department
- **Impact**: Cannot aggregate Home Office services; gap in government-wide coverage
- **Severity**: LOW (not in current requirements)
- **Recommended Action**: Engage Home Office Digital directly; monitor future API publication
- **Estimated Effort**: 5 person-days (engagement)
- **Cost Estimate**: £0

**GAP-3**: Devolved Administration APIs — Scotland, Wales, Northern Ireland
- **Data Need**: Equivalent APIs for devolved services (SEPA for Scotland flooding, NRW for Wales)
- **Why No Source**: api.gov.uk primarily covers UK central government; devolved administrations have separate digital services
- **Impact**: Environmental data England-only (EA); some services not UK-wide
- **Severity**: MEDIUM (affects UK-wide coverage claims)
- **Recommended Action**: Engage Scottish Government, Welsh Government, and NI Digital Services for devolved API discovery
- **Estimated Effort**: 15 person-days
- **Cost Estimate**: £0

**GAP-4**: NHS Digital Clinical API Governance
- **Data Need**: Streamlined access to clinical APIs (PDS, EPS, GP Connect) for approved consumers
- **Why No Source**: Clinical APIs exist but require extensive IG compliance, NHS Identity onboarding, and per-API DPIA
- **Impact**: Phase 2 clinical API integration delayed by governance lead time (8-16 weeks)
- **Severity**: MEDIUM (Phase 2 scope)
- **Recommended Action**: Begin NHS IG onboarding process early; engage NHS England API team for bulk onboarding pathway
- **Estimated Effort**: 25 person-days (compliance + integration)
- **Cost Estimate**: £0

### Gap Summary

| Gap | Requirement | Severity | Recommended Action | Effort | Cost |
|-----|-------------|----------|-------------------|--------|------|
| GAP-1 | INT-008 (DWP) | MEDIUM | Negotiate DSA with DWP Digital | 20 days | £0 |
| GAP-2 | — (Home Office) | LOW | Engage HO Digital directly | 5 days | £0 |
| GAP-3 | — (Devolved) | MEDIUM | Engage devolved administrations | 15 days | £0 |
| GAP-4 | INT-004 (NHS clinical) | MEDIUM | Begin NHS IG onboarding early | 25 days | £0 |

---

## Recommendations & Shortlist

### Top 5 Recommended Sources

#### 1. HMRC Developer Hub for Tax & Revenue

**Overall Score**: 88.5/100

**Rationale**: HMRC provides the most comprehensive and mature developer hub across UK Government, with 31 APIs supporting Making Tax Digital. OAuth 2.0 authentication is well-documented, and sandbox environments enable thorough testing before production.

**Key Strengths**:
- ✅ 31 APIs covering VAT, Self Assessment, Corporation Tax, Customs, NI
- ✅ Excellent documentation with end-to-end service guides
- ✅ Sandbox environment for integration testing

**Key Concerns**:
- ⚠️ OAuth 2.0 flows require careful implementation (user-restricted vs application-restricted)
- ⚠️ Fraud Prevention Headers mandatory for all MTD-connected software

**Cost**: Free
**Integration Effort**: 15 person-days
**Risk Level**: LOW

**Next Steps**:
- [ ] Register for HMRC Developer Hub account
- [ ] Create sandbox application for gateway integration POC
- [ ] Implement OAuth 2.0 client credentials + user-auth flows
- [ ] Validate Fraud Prevention Headers compliance

#### 2. Companies House API for Company Data

**Overall Score**: 88/100

**Rationale**: Companies House offers both REST and Streaming APIs, providing real-time company data with the simplest authentication model (API key). The Streaming API is a unique capability that enables real-time filing notifications — valuable for the platform's event-driven architecture.

**Key Strengths**:
- ✅ REST + Streaming API for real-time data changes
- ✅ Free, open data under OGL v3.0
- ✅ Simple API key authentication (instant registration)

**Key Concerns**:
- ⚠️ Beta service — no formal SLA
- ⚠️ Rate limit of 600 req/5 min may need monitoring at scale

**Cost**: Free
**Integration Effort**: 10 person-days
**Risk Level**: LOW

**Next Steps**:
- [ ] Register for Companies House API key
- [ ] Build REST adapter and Streaming consumer POC
- [ ] Validate data fields against catalogue requirements
- [ ] Load test rate limits

#### 3. Ordnance Survey Data Hub for Geospatial

**Overall Score**: 85.5/100

**Rationale**: OS provides the authoritative UK geospatial data through well-designed APIs with excellent documentation and SDKs. The PSMA agreement provides free premium access for public sector use, and the OS NGD API represents the next-generation approach.

**Key Strengths**:
- ✅ Authoritative UK mapping and address data (sub-metre accuracy)
- ✅ Excellent documentation with Python and JavaScript SDKs
- ✅ Free premium access for public sector via PSMA

**Key Concerns**:
- ⚠️ Commercial licensing may restrict passthrough to third-party developers
- ⚠️ GB coverage only — Northern Ireland requires separate source

**Cost**: £0 (PSMA) to £12,000/year (commercial)
**Integration Effort**: 10 person-days
**Risk Level**: MEDIUM

**Next Steps**:
- [ ] Register OS Data Hub account
- [ ] Confirm PSMA eligibility for platform
- [ ] Conduct POC with OS Places API (address lookup)
- [ ] Review licensing terms for third-party passthrough

#### 4. NHS Digital APIs for Health

**Overall Score**: 82/100

**Rationale**: The largest API portfolio in UK Government with 93 APIs. Phase 1 can start with open/reference APIs (ODS, service search) without heavy governance, while Phase 2 clinical API integration is planned in parallel with IG compliance process.

**Key Strengths**:
- ✅ 93 APIs — largest government API portfolio
- ✅ Modern FHIR R4 standard for newer APIs
- ✅ Tiered SLA with Platinum support for critical services (EPS)

**Key Concerns**:
- ⚠️ Clinical APIs require extensive IG compliance (8-16 week lead time)
- ⚠️ Legacy HL7 V3 APIs being migrated — transition risk
- ⚠️ England-only for most services

**Cost**: Free
**Integration Effort**: 8 person-days (Phase 1) + 25 person-days (Phase 2)
**Risk Level**: MEDIUM (governance complexity)

**Next Steps**:
- [ ] Register for NHS Developer portal
- [ ] Begin with ODS and reference data APIs (Phase 1)
- [ ] Initiate NHS IG compliance process for clinical APIs (Phase 2)
- [ ] Review FHIR adapter requirements

#### 5. Environment Agency APIs for Environmental Data

**Overall Score**: 80.5/100

**Rationale**: The simplest integration target — fully open data with no authentication required. Provides valuable real-time environmental monitoring data (flood warnings, river levels, rainfall) updated every 15 minutes under OGL licence.

**Key Strengths**:
- ✅ Fully open — no authentication or registration required
- ✅ Real-time data (15-min updates)
- ✅ OGL v3.0 — maximum licence flexibility

**Key Concerns**:
- ⚠️ Beta API — no SLA or service guarantee
- ⚠️ England-only (SEPA for Scotland, NRW for Wales)
- ⚠️ Not for safety-critical applications

**Cost**: Free
**Integration Effort**: 5 person-days
**Risk Level**: LOW

**Next Steps**:
- [ ] Build adapter POC (no registration needed)
- [ ] Implement 15-minute cache for latest readings
- [ ] Validate data formats and response normalisation
- [ ] Test flood warning and river level endpoints

---

## Impact on Data Model

### New Entities from External Sources

| Entity | Source | Description | Key Attributes | Sync Strategy |
|--------|--------|-------------|---------------|---------------|
| Government Department | CDDO Catalogue | UK Government department or agency | id, name, abbreviation, api_count, developer_hub_url | Daily batch import |
| Upstream API Definition | CDDO + Department hubs | API endpoint discovered from departments | id, department_id, name, base_url, auth_type, format, rate_limit | Daily sync + manual enrichment |
| API Health Status | Platform monitoring | Real-time health of upstream APIs | api_id, status, latency_p50, latency_p95, error_rate, last_checked | Real-time (every 30s) |
| Upstream Credential | Platform config | Stored credentials for upstream API access | api_id, auth_type, encrypted_credentials, rotation_date | Managed, rotated per schedule |

### New Attributes on Existing Entities

| Existing Entity | New Attribute | Source | Type | Update Frequency |
|----------------|---------------|--------|------|-----------------|
| API Catalogue Entry | upstream_auth_type | Department hub | Enum | On discovery |
| API Catalogue Entry | upstream_rate_limit | Department hub | Integer | On discovery |
| API Catalogue Entry | upstream_sla_tier | Department hub | String | On discovery |
| API Catalogue Entry | data_classification | Department hub | Enum | On discovery |
| API Catalogue Entry | coverage_geography | Department hub | String | On discovery |

### Sync Strategy

| Source | Pattern | Frequency | Staleness Tolerance | Fallback |
|--------|---------|-----------|--------------------|---------|
| CDDO Catalogue | Batch CSV import | Daily | 7 days | Serve cached catalogue |
| HMRC APIs | Real-time proxy | Per-request | 0 (no caching financial data) | Circuit breaker → 503 |
| Companies House | Real-time proxy + streaming | Per-request + continuous | 5 minutes (search cache) | Serve stale cache for search |
| DVLA | Real-time proxy | Per-request | 1 hour (vehicle data cache) | Serve stale cache |
| NHS Digital | Real-time proxy | Per-request | 0 (no caching clinical) | Circuit breaker → 503 |
| Environment Agency | Real-time proxy with cache | 15 minutes | 30 minutes | Serve stale cache |
| Ordnance Survey | Real-time proxy with cache | Per-request | 24 hours (map tiles) | Serve stale tiles |
| HM Land Registry | Real-time proxy | Per-request | 0 (no caching legal data) | Circuit breaker → 503 |
| DWP | Real-time proxy | Per-request | 0 (no caching personal data) | Circuit breaker → 503 |

---

## UK Government Open Data Opportunities

### TCoP Point 10: Make Better Use of Data

**Open Data Consumed**:

| Source | Dataset | License | Requirement | Status |
|--------|---------|---------|-------------|--------|
| CDDO | api.gov.uk catalogue | OGL v3.0 | INT-009 | ✅ Recommended |
| Environment Agency | Flood monitoring | OGL v3.0 | INT-005 | ✅ Recommended |
| Environment Agency | Water quality | OGL v3.0 | INT-005 | ✅ Recommended |
| Environment Agency | Rainfall | OGL v3.0 | INT-005 | ✅ Recommended |
| Companies House | Company data | OGL v3.0 | INT-002 | ✅ Recommended |
| Ordnance Survey | OS OpenData | OGL v3.0 | INT-006 | ✅ Recommended |
| GDS | Bank Holidays API | OGL v3.0 | FR-001 | ✅ Bonus |
| GDS | GOV.UK Content API | OGL v3.0 | FR-001 | ✅ Bonus |

**Open Data Publishing Opportunities**:
- API usage analytics (aggregated, anonymised) — valuable for government digital strategy
- API health and availability dashboards — transparency for consumers
- Cross-government API landscape analysis — inform digital transformation strategy

**Common Data Standards Used**:
- UPRN (Unique Property Reference Number) for property addresses — via OS Places API
- Company Number for business entities — via Companies House
- NHS Number for patient identification — via NHS PDS (Phase 2, controlled access)
- VAT Registration Number — via HMRC APIs
- Vehicle Registration Mark — via DVLA VES API
- INSPIRE identifier — via HM Land Registry

**Data Ethics Framework Compliance**:
- [x] Clear user need for data collection (aggregation reduces integration burden)
- [x] Proportionate to the need (only proxy existing public APIs)
- [x] Lawful basis established (OGL for open data; formal agreements for controlled)
- [x] Data minimisation applied (platform does not store upstream data, only proxies)
- [x] Transparency about data use (developer portal documents all data sources)
- [x] Data quality maintained (real-time proxy preserves source quality)

---

## Requirements Traceability

### Full Mapping Table

| Requirement ID | Requirement Description | Data Source | Score | Status | Notes |
|----------------|------------------------|-------------|-------|--------|-------|
| INT-001 | HMRC API aggregation | HMRC Developer Hub (31 APIs) | 88.5/100 | ✅ Matched | Phase 1; OAuth 2.0 + server token |
| INT-002 | Companies House API aggregation | Companies House REST + Streaming | 88/100 | ✅ Matched | Phase 1; API key auth |
| INT-003 | DVLA API aggregation | DVLA VES + Driver View + DVSA MOT | 81/100 | ✅ Matched | Phase 1; API key + JWT |
| INT-004 | NHS Digital API aggregation | NHS Digital (93 APIs) | 82/100 | ✅ Matched | Phase 1 (reference) + Phase 2 (clinical) |
| INT-005 | Environment Agency API aggregation | EA Flood Monitoring + 9 others | 80.5/100 | ✅ Matched | Phase 1; no auth needed |
| INT-006 | Ordnance Survey API aggregation | OS Data Hub (5 APIs) | 85.5/100 | ✅ Matched | Phase 1; API key + PSMA |
| INT-007 | Land Registry API aggregation | HMLR Business Gateway (13 APIs) | 78/100 | ✅ Matched | Phase 2; contract required |
| INT-008 | DWP API aggregation | DWP APIs (10 listed) | 57.5/100 | ⚠️ Partial | Phase 2/3; restricted access (GAP-1) |
| INT-009 | api.gov.uk catalogue import | CDDO GitHub CSV | 80/100 | ✅ Matched | Phase 1; batch import |
| FR-001 | API catalogue discovery | CDDO catalogue + department hubs | — | ✅ Matched | Composite source |
| FR-005 | Gateway routing | All 9 department sources | — | ✅ Matched | Per-adapter implementation |
| FR-006 | Response normalisation | All 9 department sources | — | ✅ Matched | JSON normalisation layer |
| FR-010 | Health monitoring | All upstream APIs | — | ✅ Constraint | Health check per adapter |
| FR-013 | Circuit breaker | All upstream APIs | — | ✅ Constraint | Per-adapter circuit breaker |

### Coverage Summary

**Requirements with Identified Sources**:
- ✅ **8 integration requirements (89%)** have recommended data sources with mature APIs
- ⚠️ **1 integration requirement (11%)** partially covered — DWP APIs exist but access is restricted
- ✅ **All functional requirements** related to gateway, normalisation, and monitoring are addressable through the identified sources
- ❌ **0 requirements** without any viable source

---

## Next Steps

### Immediate Actions (0-2 weeks)

1. **Register for API access** at HMRC Developer Hub, Companies House, DVLA, OS Data Hub, and NHS Digital developer portal
2. **Fetch CDDO catalogue CSV** from GitHub and build initial import pipeline
3. **Build Environment Agency adapter POC** (simplest — no auth, quick validation of gateway pattern)
4. **Review HMRC Fraud Prevention Headers** requirements for gateway compliance

### Data Model Updates (2-4 weeks)

5. **Update data model** with upstream API definition entity and health status tracking (`/arckit.data-model`)
6. **Create ADRs** for auth strategy (multi-auth gateway), caching strategy, and circuit breaker patterns (`/arckit.adr`)
7. **Begin DPIA** for NHS clinical APIs and DWP benefit data access (`/arckit.dpia`)

### Gap Resolution (4-8 weeks)

8. **Initiate NHS IG compliance process** for Phase 2 clinical API access
9. **Engage DWP Digital** for formal data-sharing agreement discussion
10. **Negotiate HM Land Registry Business Gateway contract** for property API access
11. **Confirm OS PSMA eligibility** and licensing terms for third-party passthrough
12. **Engage devolved administrations** (Scottish Government, Welsh Government, NI) for equivalent API discovery

### Integration (Ongoing)

13. **Build department adapters** in priority order: EA → Companies House → HMRC → DVLA → OS → NHS (ref) → HMLR → NHS (clinical) → DWP
14. **Implement multi-auth gateway** supporting: no auth, API key, OAuth 2.0, JWT, and mutual TLS
15. **Set up health monitoring** and circuit breakers for all upstream APIs
16. **Build response normalisation layer** for consistent JSON output across departments

---

## Appendices

### Appendix A: Research Methodology

**Data Sources Searched**:
- UK Government API catalogue (api.gov.uk) — 240 APIs across 34 departments
- HMRC Developer Hub (developer.service.hmrc.gov.uk)
- Companies House Developer Hub (developer.company-information.service.gov.uk)
- DVLA Developer Portal (developer-portal.driver-vehicle-licensing.api.gov.uk)
- NHS Digital Developer Hub (digital.nhs.uk/developer)
- Environment Agency Data Platform (environment.data.gov.uk)
- Ordnance Survey Data Hub (osdatahub.os.uk)
- HM Land Registry Developer Pack (landregistry.github.io)
- DWP Digital Blog (dwpdigital.blog.gov.uk)
- CDDO API Catalogue GitHub repository (github.com/co-cddo/api-catalogue)

**Evaluation Methodology**:
- Weighted scoring across 6 criteria (Requirements Fit 25%, Data Quality 20%, License & Cost 15%, API Quality 15%, Compliance 15%, Reliability 10%)
- All scores based on verified information from official department sources
- Pricing verified from official documentation and developer portals
- API quality assessed from documentation review and endpoint analysis

**Limitations**:
- Pricing based on published rates (volume discounts may be available via PSMA, framework agreements)
- API quality assessed from documentation, not hands-on testing (POC needed to validate)
- Data quality indicators from provider documentation (validate during integration POC)
- Some departments may have internal APIs not listed in the public catalogue
- Market evolves — discovery valid for approximately 6 months

### Appendix B: Full Department API Count (api.gov.uk)

| Department | Abbreviation | API Count |
|-----------|-------------|-----------|
| NHS Digital | ND | 93 |
| HM Revenue & Customs | HMRC | 31 |
| HM Land Registry | HMLR | 13 |
| Ministry of Housing, Communities & Local Government | MHCLG | 12 |
| Environment Agency | EA | 10 |
| Department for Work and Pensions | DWP | 10 |
| Ordnance Survey | OS | 8 |
| Government Digital Service | GDS | 7 |
| Historic England | HE | 6 |
| Driver and Vehicle Licensing Agency | DVLA | 6 |
| Department for Business and Trade | DBT | 6 |
| Companies House | CH | 5 |
| Natural England | NE | 4 |
| Ministry of Justice | MOJ | 4 |
| Department for Education | DfE | 4 |
| Food Standards Agency | FSA | 3 |
| National Records of Scotland | NRS | 2 |
| Office for National Statistics | ONS | 2 |
| The National Archives | TNA | 2 |
| Valuation Office Agency | VOA | 2 |
| Planning Inspectorate | PINS | 2 |
| UK Hydrographic Office | UKHO | 2 |
| Department for Transport | DfT | 1 |
| DEFRA | DEFRA | 1 |
| Office of the Public Guardian | OPG | 1 |
| Intellectual Property Office | IPO | 1 |
| Scottish Environment Protection Agency | SEPA | 1 |
| Met Office | MO | 1 |
| Other departments | Various | ~3 |
| **TOTAL** | | **~240** |

### Appendix C: Government APIs NOT Listed on api.gov.uk

The api.gov.uk catalogue (240 APIs, 34 departments) is **not exhaustive**. The catalogue relies on departments voluntarily submitting their APIs via GitHub Issues. CDDO acknowledges this gap and is exploring a federated discovery model. The following significant APIs exist outside the central catalogue:

#### C.1 Border & Customs APIs (HMRC)

Published on GOV.UK separately from api.gov.uk, these APIs support UK border trade:

| API | Description | Auth | Status |
|-----|-------------|------|--------|
| **CDS (Customs Declaration Service)** | Import/export declarations replacing CHIEF | OAuth 2.0 | Active |
| **NCTS (New Computerised Transit System)** | Transit declarations for goods moving through UK | OAuth 2.0 | Active |
| **GVMS (Goods Vehicle Movement Service)** | Goods Movement Records for cross-border haulage | OAuth 2.0 | Active |
| **Safety & Security Import Declarations** | Pre-arrival safety declarations | OAuth 2.0 | Active |

**Reference**: https://www.gov.uk/government/publications/apis

#### C.2 Fuel Finder Open Data API (DESNZ / CMA)

A **brand new** statutory open data scheme launching **2 February 2026** under the Motor Fuel Price (Open Data) Regulations 2025:

| Attribute | Value |
|-----------|-------|
| **Provider** | Department for Energy Security and Net Zero (DESNZ); aggregated by VE3 Global Ltd |
| **Description** | Real-time fuel prices from every UK petrol station, updated within 30 minutes of any price change |
| **Legal Basis** | Data (Use and Access) Act 2025; Motor Fuel Price (Open Data) Regulations 2025 |
| **Data Available** | Per-station prices by fuel grade, station name, address, lat/long, trading hours, amenities |
| **Update Frequency** | Near real-time (within 30 minutes of price change at pump) |
| **Coverage** | UK-wide (all forecourts, mandatory) |
| **Authentication** | To be confirmed (open data scheme — expected to be freely accessible to developers) |
| **Enforcement** | CMA enforcement; penalties up to 1% worldwide turnover for non-compliance |
| **Launch Date** | 2 February 2026 (stations registering from December 2025) |
| **Access Point** | https://www.gov.uk/guidance/access-fuel-price-data |

**Significance for the aggregator**: This is a major new government open data API launching imminently. It represents exactly the type of cross-department data that the API Aggregator should surface.

#### C.3 Legislation API (The National Archives)

| Attribute | Value |
|-----------|-------|
| **Provider** | The National Archives |
| **API Endpoint** | https://www.legislation.gov.uk/developer |
| **Description** | Consolidated UK legislation in XML, RDF, and Atom formats |
| **Auth** | None (fully open) |
| **License** | Open Government Licence v3.0 |
| **Format** | XML (Legislation Schema), RDF, Atom, PDF |
| **Status** | Active (since 2010) |

#### C.4 UK Police Data API (Home Office)

| Attribute | Value |
|-----------|-------|
| **Provider** | Home Office / data.police.uk |
| **API Endpoint** | https://data.police.uk/docs/ |
| **Description** | Street-level crime data, outcomes, stop and search, force/neighbourhood info |
| **Auth** | None (15 req/s, 30 burst) |
| **License** | Open Government Licence v3.0 |
| **Coverage** | England, Wales, Northern Ireland police forces |
| **Status** | Active |

**Note**: Despite the Home Office showing 0 APIs on api.gov.uk, the Police Data API is one of the most used government open data services.

#### C.5 Carbon Intensity API (National Energy System Operator)

| Attribute | Value |
|-----------|-------|
| **Provider** | NESO (formerly National Grid ESO) |
| **API Endpoint** | https://api.carbonintensity.org.uk |
| **Description** | Regional carbon intensity of GB electricity system, 48-hour forecasts |
| **Auth** | None (fully open) |
| **License** | CC BY 4.0 |
| **Status** | Active |

#### C.6 ONS Developer Hub (Beta)

| Attribute | Value |
|-----------|-------|
| **Provider** | Office for National Statistics |
| **API Endpoint** | https://api.beta.ons.gov.uk/v1 |
| **Description** | Programmatic access to ONS datasets (census, labour market, CPI, GDP) |
| **Auth** | None (fully open, beta) |
| **Documentation** | https://developer.ons.gov.uk |
| **Status** | Beta |

**Note**: api.gov.uk lists only 2 ONS APIs but the developer hub provides access to 275+ datasets.

#### C.7 DfE Find and Use an API (Beta)

| Attribute | Value |
|-----------|-------|
| **Provider** | Department for Education |
| **API Endpoint** | https://find-and-use-an-api.education.gov.uk |
| **Description** | DfE's own API catalogue — schools, finance, corporate data |
| **Auth** | API Key (subscription) |
| **Status** | Beta |

**Note**: api.gov.uk lists only 4 DfE APIs; the DfE's own catalogue contains additional APIs with sandbox environments.

#### C.8 GOV.UK Platform APIs (GDS)

Published separately from api.gov.uk, these power the GOV.UK platform:

| API | Description | Listed on api.gov.uk? |
|-----|-------------|----------------------|
| GOV.UK Content API | Published content in JSON | Yes |
| GOV.UK Notify API | Email, SMS, letters to users | Yes |
| GOV.UK Pay API | Payment processing | Yes |
| GOV.UK Search API | Site search | Yes |
| GOV.UK Publishing APIs (~40) | Internal publishing platform APIs | **No** |
| GOV.UK Chat API | AI-powered Q&A (launching 2026) | **No** |

**Reference**: https://docs.publishing.service.gov.uk/apis.html

#### C.9 NHS Website APIs (developer.api.nhs.uk)

| Attribute | Value |
|-----------|-------|
| **Provider** | NHS England |
| **API Endpoint** | https://developer.api.nhs.uk |
| **Description** | NHS website content syndication, service finder |
| **Status** | Being migrated to digital.nhs.uk (retiring Spring 2026) |

**Note**: Separate from the 93 NHS Digital APIs on api.gov.uk — these are NHS website-specific APIs.

#### C.10 Transport for London Unified API

| Attribute | Value |
|-----------|-------|
| **Provider** | Transport for London |
| **API Endpoint** | https://api.tfl.gov.uk |
| **Description** | Bus arrivals, Tube data, journey planner, station locations, accessibility, road disruptions |
| **Auth** | API Key (free registration) |
| **License** | OGL v3.0 |
| **Documentation** | Swagger: https://api.tfl.gov.uk/swagger/ui/index.html |
| **Status** | Active |

**Note**: Listed on api.gov.uk (1 entry) but the Unified API contains dozens of sub-APIs.

#### C.11 Devolved Administration APIs

Equivalent services not covered by api.gov.uk:

| Region | Service | API/Portal | Equivalent to |
|--------|---------|-----------|---------------|
| **Scotland** | SEPA Time Series API | https://timeseriesdoc.sepa.org.uk | Environment Agency flood monitoring |
| **Scotland** | SEPA Rainfall API | https://www2.sepa.org.uk/rainfall | EA rainfall data |
| **Scotland** | statistics.gov.scot | https://statistics.gov.scot | ONS statistics |
| **Wales** | NRW Flood & River Levels API | https://api-portal.naturalresources.wales | EA flood monitoring |
| **Wales** | NRW Bathing Water API | https://environment.data.gov.uk/wales/bathing-waters/ | EA bathing water |
| **N. Ireland** | OpenDataNI Portal | https://www.opendatani.gov.uk | data.gov.uk |

#### C.12 Met Office Weather DataHub (Replacement for DataPoint)

| Attribute | Value |
|-----------|-------|
| **Provider** | Met Office |
| **Description** | Weather forecasts, observations, map imagery |
| **Note** | DataPoint API was **retired** in 2025; replaced by Weather DataHub (commercial, tiered pricing) |
| **Auth** | API Key |
| **Status** | Active (commercial) |

#### Summary: Estimated Total UK Government APIs

| Source | API Count |
|--------|-----------|
| api.gov.uk catalogue | ~240 |
| Border/Customs APIs (HMRC) | ~8 |
| Fuel Finder (DESNZ, launching Feb 2026) | 1 |
| Legislation API (TNA) | 1 |
| Police Data API (Home Office) | 1 |
| Carbon Intensity (NESO) | 1 |
| ONS Developer Hub (uncatalogued datasets) | ~275 datasets |
| DfE Find and Use an API (additional) | ~10+ |
| GOV.UK Publishing Platform (internal) | ~40 |
| NHS Website APIs | ~5 |
| TfL sub-APIs | ~15 |
| Devolved administration APIs | ~10 |
| Met Office Weather DataHub | ~5 |
| **Estimated total UK public sector APIs** | **~400+ unique APIs** |

The api.gov.uk catalogue captures roughly **60%** of publicly accessible UK Government APIs. The remainder are discoverable only through department-specific developer hubs, GOV.UK publications, or open data portals.

---

### Appendix D: Glossary

- **API**: Application Programming Interface
- **CDDO**: Central Digital and Data Office
- **CIS2**: Care Identity Service 2 (NHS authentication)
- **DPA 2018**: Data Protection Act 2018
- **DPIA**: Data Protection Impact Assessment
- **DSA**: Data Sharing Agreement
- **EA**: Environment Agency
- **EPS**: Electronic Prescription Service
- **ETL**: Extract, Transform, Load
- **FHIR**: Fast Healthcare Interoperability Resources
- **GDPR**: General Data Protection Regulation (UK GDPR)
- **GDS**: Government Digital Service
- **HMLR**: HM Land Registry
- **IG**: Information Governance
- **MTD**: Making Tax Digital
- **mTLS**: Mutual Transport Layer Security
- **ODS**: Organisation Data Service (NHS)
- **OGL**: Open Government Licence
- **PDS**: Personal Demographics Service (NHS)
- **PII**: Personally Identifiable Information
- **PSC**: Persons with Significant Control
- **PSMA**: Public Sector Mapping Agreement
- **SLA**: Service Level Agreement
- **TCoP**: Technology Code of Practice (UK Government)
- **TTL**: Time To Live (cache expiry)
- **UPRN**: Unique Property Reference Number
- **VES**: Vehicle Enquiry Service (DVLA)

---

**Generated by**: ArcKit `/arckit.datascout` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.1.0
**Project**: UK Government API Aggregator
**Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
