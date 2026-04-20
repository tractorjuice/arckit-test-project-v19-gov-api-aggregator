# UK Government API Aggregator

A platform that aggregates, indexes, and provides unified access to UK Government APIs from across departments and public sector organisations.

Built with [ArcKit](https://tractorjuice.github.io/arc-kit/) v4.7.2 -- AI-driven slash commands for architecture governance across Claude Code, Gemini CLI, and Codex CLI.

## Problem Statement

The UK Government maintains **240+ APIs** across **34+ departments** (catalogued at [api.gov.uk](https://www.api.gov.uk/)). Developers building government digital services must:

- Discover APIs across multiple department developer hubs
- Register separately with each department
- Handle inconsistent authentication, formats, and error responses
- Monitor multiple API health dashboards independently
- Navigate different versioning and deprecation policies

This creates friction for both internal government teams and external developers building on government data.

## Vision

A unified API aggregation platform that:

1. **Discovers** -- Automatically catalogues UK Government APIs from api.gov.uk and department hubs
2. **Normalises** -- Provides consistent request/response formats across departments
3. **Secures** -- Unified authentication, rate limiting, and access control
4. **Monitors** -- Centralised health, latency, and usage analytics
5. **Documents** -- Single developer portal with sandbox environments

## Compliance

- UK Government [Technology Code of Practice](https://www.gov.uk/guidance/the-technology-code-of-practice) (TCoP)
- [GDS Service Standard](https://www.gov.uk/service-manual/service-standard)
- [NCSC Cloud Security Principles](https://www.ncsc.gov.uk/collection/cloud-security)
- [API Technical and Data Standards](https://www.gov.uk/guidance/gds-api-technical-and-data-standards)

## Current Status

Architecture-first project — no application code yet. Governance artifacts produced so far for project `001-uk-government-api-aggregator`:

- Architecture Principles (global)
- Requirements, Stakeholder Drivers, Product Backlog
- Secure by Design assessment
- Data Source Discovery, AWS research (v1.1), Azure research (v1.2)
- Architecture Diagrams
- Wardley Mapping suite: Value Chain, Doctrine, Gameplay, Climate
- Analysis Report, Traceability Matrix (v1.1), Project Story

Live documentation site: generated via `/arckit.pages` — see [`docs/index.html`](docs/index.html).

## Getting Started

1. Start your AI assistant (Claude Code, Gemini CLI, or Codex CLI)
2. Run `/arckit.start` for guided onboarding, or jump straight in:
3. `/arckit.principles` → `/arckit.stakeholders` → `/arckit.requirements`
4. Run `/arckit.health` any time to surface stale artifacts and governance gaps

Full dependency ordering is documented in [`DEPENDENCY-MATRIX.md`](DEPENDENCY-MATRIX.md).

## Available Commands

Once you start your AI assistant, you'll have access to the full ArcKit command set:

#### Project Planning
- `/arckit.plan` - Create project plan with timeline, phases, and gates

#### Core Workflow
- `/arckit.principles` - Create or update architecture principles
- `/arckit.stakeholders` - Analyze stakeholder drivers, goals, and outcomes
- `/arckit.risk` - Create comprehensive risk register (Orange Book)
- `/arckit.sobc` - Create Strategic Outline Business Case (Green Book 5-case)
- `/arckit.requirements` - Define comprehensive requirements
- `/arckit.data-model` - Create data model with ERD, GDPR compliance, data governance
- `/arckit.research` - Research technology, services, and products with build vs buy analysis
- `/arckit.datascout` - Discover external data sources, APIs, and open data portals
- `/arckit.adr` - Document architectural decisions with options analysis
- `/arckit.strategy` - Synthesise strategic artifacts into executive Architecture Strategy

#### Wardley Mapping
- `/arckit.wardley` - Create strategic Wardley Maps for build vs buy and procurement strategy
- `/arckit.wardley.value-chain` - Decompose user needs into value chains
- `/arckit.wardley.doctrine` - Assess organisational doctrine maturity
- `/arckit.wardley.gameplay` - Analyse strategic play options using 60+ gameplay patterns
- `/arckit.wardley.climate` - Assess climatic patterns affecting map components

#### Cloud Research
- `/arckit.aws-research` - Research AWS services using AWS Knowledge MCP
- `/arckit.azure-research` - Research Azure services using Microsoft Learn MCP
- `/arckit.gcp-research` - Research Google Cloud services using Google Developer MCP

#### Government Code Reuse
- `/arckit.gov-code-search` - Search 24,500+ UK government repositories
- `/arckit.gov-landscape` - Map the UK government code landscape for a domain
- `/arckit.gov-reuse` - Discover reusable UK government code before building
- `/arckit.grants` - Research UK government grants and funding opportunities

#### Vendor Procurement
- `/arckit.sow` - Generate Statement of Work (RFP)
- `/arckit.dos` - Digital Outcomes and Specialists (DOS) procurement
- `/arckit.gcloud-search` - Search G-Cloud services on UK Digital Marketplace
- `/arckit.gcloud-clarify` - Validate G-Cloud services and generate clarification questions
- `/arckit.evaluate` - Create vendor evaluation framework and score vendors

#### Design & Delivery
- `/arckit.diagram` - Generate visual architecture diagrams using Mermaid
- `/arckit.hld-review` - Review High-Level Design
- `/arckit.dld-review` - Review Detailed Design
- `/arckit.backlog` - Generate prioritised product backlog with GDS user stories
- `/arckit.devops` - Create DevOps strategy with CI/CD pipelines
- `/arckit.finops` - Create FinOps strategy for cloud cost management
- `/arckit.mlops` - Create MLOps strategy with model lifecycle and governance
- `/arckit.operationalize` - Create operational readiness pack with runbooks and DR/BCP
- `/arckit.roadmap` - Create strategic architecture roadmap
- `/arckit.platform-design` - Create platform strategy using Platform Design Toolkit

#### Governance & Quality
- `/arckit.traceability` - Generate requirements traceability matrix
- `/arckit.analyze` - Comprehensive governance quality analysis
- `/arckit.principles-compliance` - Architecture principles compliance scorecard
- `/arckit.conformance` - Assess architecture conformance and drift
- `/arckit.health` - Diagnostic health check across all artifacts
- `/arckit.impact` - Analyse blast radius of a requirement or decision change
- `/arckit.search` - Search across all project artifacts
- `/arckit.glossary` - Consolidate terms, acronyms, and definitions

#### Service Management
- `/arckit.servicenow` - Generate ServiceNow service design
- `/arckit.data-mesh-contract` - Federated data product contracts
- `/arckit.dfd` - Generate Yourdon-DeMarco Data Flow Diagrams
- `/arckit.maturity-model` - Generate capability maturity models

#### UK Government Compliance
- `/arckit.service-assessment` - GDS Service Standard assessment preparation
- `/arckit.tcop` - Technology Code of Practice assessment
- `/arckit.ai-playbook` - AI Playbook compliance for responsible AI
- `/arckit.dpia` - Data Protection Impact Assessment (UK GDPR Article 35)
- `/arckit.atrs` - Algorithmic Transparency Recording Standard (ATRS) record

#### Security Assessment
- `/arckit.secure` - UK Government Secure by Design
- `/arckit.mod-secure` - MOD Secure by Design
- `/arckit.jsp-936` - MOD JSP 936 AI assurance documentation

#### Reporting
- `/arckit.story` - Generate project story with timeline and governance achievements
- `/arckit.pages` - Generate GitHub Pages site for project documentation
- `/arckit.presentation` - Generate MARP presentation slides from artifacts
- `/arckit.trello` - Export product backlog to a Trello board
- `/arckit.framework` - Transform artifacts into a phased framework

#### Setup & Extension
- `/arckit.start` - Guided onboarding and workflow selection
- `/arckit.init` - Initialize ArcKit project structure
- `/arckit.customize` - Copy plugin templates to project for customization
- `/arckit.template-builder` - Create new document templates

## Project Structure

```
gov-api-aggregator/
├── docs/
│   ├── index.html          # Generated documentation site (/arckit.pages)
│   ├── manifest.json       # Document index for the site
│   ├── health.json         # Latest /arckit.health scan
│   ├── llms.txt            # LLM/agent discovery index
│   └── guides/             # Command usage guides
├── projects/
│   ├── 000-global/
│   │   ├── policies/                # Organisation-wide policies
│   │   ├── external/                # Enterprise reference documents
│   │   └── ARC-000-PRIN-v1.0.md     # Architecture Principles
│   └── 001-uk-government-api-aggregator/
│       ├── ARC-001-REQ-v1.0.md      # Requirements
│       ├── ARC-001-STKE-v1.0.md     # Stakeholder Drivers
│       ├── ARC-001-BKLG-v1.0.md     # Product Backlog
│       ├── ARC-001-SECD-v1.0.md     # Secure by Design
│       ├── ARC-001-DSCT-v1.0.md     # Data Source Discovery
│       ├── ARC-001-ANAL-v1.0.md     # Analysis Report
│       ├── ARC-001-TRAC-v1.1.md     # Traceability Matrix
│       ├── ARC-001-STORY-v1.0.md    # Project Story
│       ├── diagrams/                # Architecture Diagrams
│       ├── wardley-maps/            # Value chain, doctrine, gameplay, climate
│       ├── research/                # AWS & Azure research
│       ├── decisions/               # ADRs
│       ├── reviews/                 # HLD / DLD reviews
│       └── external/                # PDFs, specs, vendor docs
├── CLAUDE.md               # Project instructions for Claude Code
└── README.md
```

## Documentation

- [ArcKit Documentation](https://tractorjuice.github.io/arc-kit/)
- [Project Documentation Site](docs/index.html) — generated by `/arckit.pages`
- [Command Guides](docs/guides/)
- [API Technical and Data Standards](https://www.gov.uk/guidance/gds-api-technical-and-data-standards)
- [api.gov.uk](https://www.api.gov.uk/)

## License

MIT
