# UK Government API Aggregator

A platform that aggregates, indexes, and provides unified access to UK Government APIs from across departments and public sector organisations.

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

1. **Discovers** — Automatically catalogues UK Government APIs from api.gov.uk and department hubs
2. **Normalises** — Provides consistent request/response formats across departments
3. **Secures** — Unified authentication, rate limiting, and access control
4. **Monitors** — Centralised health, latency, and usage analytics
5. **Documents** — Single developer portal with sandbox environments

## Architecture

This project uses [ArcKit](https://github.com/tractorjuice/arc-kit) for architecture governance. All architecture artifacts are generated using ArcKit slash commands.

### Getting Started

```bash
# Install ArcKit
pip install arckit-cli

# Start your AI assistant
claude  # or gemini or codex

# Begin with principles
/arckit.principles

# Define requirements
/arckit.requirements Government API Aggregator

# Discover data sources
/arckit.datascout Discover UK Government APIs for aggregation
```

### Project Structure

```
projects/
  000-global/              # Cross-project architecture principles
  001-gov-api-aggregator/  # Project artifacts
docs/
  guides/                  # ArcKit command guides
```

## Compliance

- UK Government [Technology Code of Practice](https://www.gov.uk/guidance/the-technology-code-of-practice) (TCoP)
- [GDS Service Standard](https://www.gov.uk/service-manual/service-standard)
- [NCSC Cloud Security Principles](https://www.ncsc.gov.uk/collection/cloud-security)
- [API Technical and Data Standards](https://www.gov.uk/guidance/gds-api-technical-and-data-standards)

## License

MIT
