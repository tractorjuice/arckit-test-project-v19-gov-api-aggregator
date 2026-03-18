# Wardley Gameplay Analysis: UK Government API Aggregator

> **Template Origin**: Official | **ArcKit Version**: 4.3.1 | **Command**: `/arckit.wardley.gameplay`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-WGAM-001-v1.0 |
| **Document Type** | Wardley Gameplay Analysis |
| **Project** | UK Government API Aggregator (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-03-18 |
| **Last Modified** | 2026-03-18 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-04-17 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Programme Board, Architecture Team, Leadership |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-18 | ArcKit AI | Initial creation from `/arckit:wardley.gameplay` command | [PENDING] | [PENDING] |

---

## Executive Summary

The UK Government API Aggregator occupies a unique strategic position: it is a Custom-Built aggregation platform in a growing but fragmented government API market with no direct competitors. The dominant strategic posture is **opportunistic with ecosystem building** -- the opportunity window is open but department inertia is the primary constraint. The platform's core value comes from two genesis/custom-built differentiators (Discovery Engine, Response Normalisation) surrounded by product-stage and commodity components that should be bought or outsourced.

Seven plays are recommended across three strategic thrusts: (1) **Market creation** through Aggregation, Education, and Market Enablement; (2) **Ecosystem building** through Open Approaches and Co-creation with departments; (3) **Execution enablement** through Managing Inertia and Experimentation. All recommended plays are Lawful Good or Neutral, consistent with UK Government values and TCoP requirements. No LE or CE plays are recommended for deployment.

**Selected Plays Summary**:

| Play | Alignment | Category | Recommendation | Priority | Time Horizon |
|------|-----------|----------|----------------|----------|--------------|
| Aggregation | N | J: Positional | Apply | High | Immediate |
| Education | LG | A: User Perception | Apply | High | Immediate |
| Open Approaches | LG | B: Accelerators | Apply | High | Short-term |
| Industrial Policy | N | B: Accelerators | Apply | High | Immediate |
| Co-creation | LG | H: Ecosystem | Apply | Medium | Short-term |
| Managing Inertia | N | F: Defensive | Apply | High | Immediate |
| Experimentation | LG | G: Attacking | Apply | Medium | Immediate |

---

## Map Reference

This gameplay analysis is derived from the following artifact:

| Field | Value |
|-------|-------|
| **Source Document ID** | ARC-001-WVCH-001-v1.0 |
| **Document Type** | Wardley Value Chain (used as map proxy; no full WARD artifact yet exists) |
| **Map Date** | 2026-03-18 |
| **Key Components** | Discovery Engine [0.42, 0.30], Response Normalisation [0.48, 0.35], API Gateway [0.78, 0.70], Developer Portal [0.90, 0.55], API Catalogue [0.85, 0.40] |

> **Note**: A full Wardley Map (`/arckit:wardley`) would strengthen this analysis with inertia annotations, pipeline positions, and movement arrows. This analysis uses the value chain component positions as the basis for gameplay selection. Consider running `/arckit:wardley` to create the full WARD artifact.

---

## Situational Assessment

### Position Analysis

- **Anchor (User Need)**: "Developer can build applications using UK Government data through a single integration point" [0.95, 0.35] -- Custom-Built evolution, indicating a novel need that the market has not yet standardised
- **Differentiating Components**: Discovery Engine [0.42, 0.30] and Response Normalisation [0.48, 0.35] are genesis/custom-built -- unique to this platform, no off-the-shelf alternatives exist. API Catalogue [0.85, 0.40] is custom-built at high visibility
- **Product-Stage Components**: API Gateway [0.78, 0.70], Developer Registration [0.70, 0.72], API Documentation [0.80, 0.65], Usage Analytics [0.65, 0.60] -- multiple vendor options available; buy or configure rather than build
- **Commodity Dependencies**: Rate Limiting [0.52, 0.75], Secrets Management [0.18, 0.80], Cloud Hosting [0.08, 0.90], DNS/CDN [0.05, 0.92] -- outsource to utility providers
- **External Dependency**: Upstream Govt APIs [0.30, 0.45] -- not under platform control; each department operates independently

**Dominant Position Type**: **Custom-Built strength in a growing market**. The Play-Position Matrix recommends: Centre of Gravity, Differentiation, Co-creation.

### Capability Assessment

- **Core Strengths**: GDS's existing platform delivery track record (GOV.UK Pay, Notify, Verify), cross-government mandate, ministerial support, existing api.gov.uk catalogue data
- **Critical Weaknesses**: Doctrine assessment (ARC-001-WDOC-v1.0) scores 2.5/5.0 overall; Bias Towards Action at 2/5; no team structure designed; ownership unassigned. Execution capability is untested
- **Unique Assets**: GDS's existing relationships with department CTOs via CTO Council; api.gov.uk catalogue providing baseline data; TCoP mandate creating regulatory pull
- **Constraints**: Treasury spending review gates limit investment speed; department MoU negotiations required before API onboarding; GDS Service Standard assessment gates at Alpha/Beta; overall doctrine maturity at Developing (2.5/5)

### Market Context

- **Competitor Positions**: No direct competitor currently aggregates UK Government APIs. api.gov.uk exists as a manual catalogue but not a gateway. Each department operates independently. The absence of competition creates a window but also means there is no proven market demand for aggregation
- **Market Signals**: Growing developer community around gov.uk APIs; increasing department API publication; GDS "government as a platform" strategy. EU is developing similar API catalogues. Private-sector API aggregators (RapidAPI) demonstrate the model works commercially
- **Regulatory Environment**: TCoP mandates open source, open standards, cloud-first. GDS Service Standard requires user research evidence. NCSC security guidance constrains architecture. These are enabling constraints -- they push toward LG plays
- **Partnership Opportunities**: Department API owners (HMRC, Companies House, DVLA, NHS Digital, Environment Agency, OS) as co-creation partners. GOV.UK One Login as identity partner. Existing GDS platforms (Pay, Notify) as integration examples

### Peace/War/Wonder Phase

**Assessment**: Early **Peace** transitioning toward **Wonder**

- The government API space is in **Peace** -- departments publish APIs independently, no commoditisation pressure, feature competition is absent because there is no competition
- **Wonder** signals: the aggregation concept itself is a higher-order system that combines existing APIs into something new. The Discovery Engine and Response Normalisation represent new capabilities that could create a fundamentally different developer experience
- **Implication**: Peace favours Education, Differentiation, and Sensing Engines. Wonder favours Experimentation, Co-creation, and Weak Signal/Horizon

---

## Play Evaluation by Category

### Category A: User Perception

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Education | LG | High | **Apply** | Discovery Engine and unified gateway are novel concepts. Developers need to understand what unified govt API access means and why it is better than direct integration. Market understanding is low -- education creates demand |
| Bundling | N | Medium | Monitor | The platform naturally bundles APIs, but the bundling play is premature until multiple APIs are onboarded. Revisit at Beta |
| Creating Artificial Needs | LE | Low | Skip | The developer need is genuine (validated by personas and stakeholder analysis). No need to manufacture demand |
| Confusion of Choice | LE | Low | Skip | Inappropriate for UK Government; contradicts TCoP transparency requirements |
| Brand and Marketing | N | Medium | Monitor | GDS brand has value but the platform must prove utility before marketing. Revisit post-Beta |
| FUD | LE | Low | Skip | Inappropriate for UK Government. No competitors to direct FUD toward |
| Artificial Competition | CE | None | Skip | CE -- recognise only. Not applicable |
| Lobbying/Counterplay | CE | None | Skip | CE -- recognise only. The project already has ministerial support; further lobbying unnecessary |

### Category B: Accelerators

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Market Enablement | LG | High | **Apply** | The platform IS market enablement -- it lowers barriers for developers to access govt APIs. Standards, sandbox, and documentation reduce friction. Directly aligned with GDS mandate |
| Open Approaches | LG | High | **Apply** | TCoP mandates open source (Point 3). Open-sourcing the gateway and adapters accelerates adoption, builds department trust, and invites community contribution. Reduces "GDS is taking over" perception |
| Exploiting Network Effects | N | Medium | Monitor | Platform becomes more valuable as more APIs and developers join. But network effects require critical mass (8+ APIs, 100+ developers) not yet achieved |
| Co-operation | N | Medium | Monitor | Cross-government co-operation via CTO Council exists but not formalised for this project. Could evolve into formal co-operation play with EU API catalogue initiatives |
| Industrial Policy | N | High | **Apply** | This project IS industrial policy -- GDS mandate, TCoP requirements, and ministerial support create regulatory pull that market forces alone cannot generate. Leverage the mandate to drive department adoption |

### Category C: De-accelerators

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Exploiting Constraint | LE | Low | Skip | No resource constraint to exploit. Government context makes this inappropriate |
| IPR | LE | Low | Skip | TCoP mandates open source. IPR protection contradicts the platform's values and mandate |
| Creating Constraints | CE | None | Skip | CE -- recognise only. Actively harmful to government transparency goals |

### Category D: Dealing with Toxicity

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Pig in a Poke | CE | None | Skip | CE -- recognise only |
| Disposal of Liability | N | Low | Skip | No toxic components to dispose of -- the platform is greenfield |
| Sweat and Dump | LE | None | Skip | Not applicable to a new platform |
| Refactoring | LG | Low | Skip | No legacy to refactor. The existing api.gov.uk catalogue could be refactored into the new platform, but this is more accurately described as Aggregation |

### Category E: Market

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Differentiation | N | Medium | Monitor | The platform differentiates through unified access, but there is no competitor to differentiate against yet. Differentiation becomes relevant if departments build their own aggregation or if EU catalogues emerge as alternatives |
| Pricing Policy | N | Low | Skip | Government platform -- free at point of use. No pricing lever |
| Buyer/Supplier Power | LE | Low | Skip | Inappropriate for government context. Departments are partners, not suppliers to be squeezed |
| Harvesting | LE | None | Skip | Platform is pre-launch; harvesting is irrelevant |
| Standards Game | LE | Low | Skip | The platform should adopt standards, not create proprietary ones. TCoP mandates open standards |
| Last Man Standing | LE | None | Skip | No competitors to outlast |
| Signal Distortion | CE | None | Skip | CE -- recognise only |
| Trading | N | Low | Skip | No components to trade at this stage |

### Category F: Defensive

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Threat Acquisition | N | Low | Skip | No emerging threats to acquire. Departments are partners, not threats |
| Raising Barriers to Entry | N | Low | Skip | Premature -- the platform must first establish value before worrying about defence |
| Procrastination | N | Low | Skip | The doctrine assessment flags insufficient action already; procrastination would be counterproductive |
| Defensive Regulation | LE | Low | Skip | TCoP already provides favourable regulatory context |
| Limitation of Competition | CE | None | Skip | CE -- recognise only |
| Managing Inertia | N | High | **Apply** | Department resistance (SD-2 in stakeholder analysis) is the primary risk to the platform. Departments fear loss of autonomy. Inertia must be actively managed through trust-building, MoUs, and co-design. Doctrine assessment scores this at 3/5 -- partially addressed but needs execution |

### Category G: Attacking

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Directed Investment | LG | Medium | Monitor | Government spending review gates constrain directed investment. The phased approach (BR-006) is a controlled investment model. Revisit if phase gates approve acceleration |
| Experimentation | LG | High | **Apply** | Discovery Engine [0.42, 0.30] is genesis-stage. Rapid experimentation on crawling strategies, API detection methods, and normalisation approaches is essential. Doctrine assessment flags Bias Towards Action at 2/5 -- experimentation directly addresses this gap |
| Centre of Gravity | N | Medium | Monitor | The centre of gravity for department API access is currently the department developer hubs themselves. The aggregator aims to become the new centre of gravity, but this requires execution, not a directed attack |
| Undermining Barriers to Entry | N | Medium | Monitor | The platform inherently undermines barriers to govt API access (reducing per-department registration overhead). This is a natural consequence of aggregation, not a separate play |
| Fool's Mate | LE | Low | Skip | Requires secrecy and surprise. Government projects operate in the open. Inappropriate |
| Press Release Process | LE | Low | Skip | Premature; announcing before building risks credibility |
| Playing Both Sides | N | Low | Skip | The platform serves developers and departments -- but this is N-sided Markets, not Playing Both Sides |

### Category H: Ecosystem

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Alliances | LG | Medium | Monitor | Formalising alliances with department API owners is part of Co-creation (below). Separate Alliances play becomes relevant for cross-government or international partnerships |
| Co-creation | LG | High | **Apply** | Departments should co-create API adapters for their services rather than GDS building them unilaterally. Co-design workshops (identified in STKE analysis) turn departments from resistant stakeholders into co-owners. Reduces "GDS is taking over" perception |
| Sensing Engines / ILC | N | Medium | Monitor | The platform will generate usage data that can inform which APIs to prioritise. But this requires live traffic -- too early for deployment. Build the data infrastructure now; activate sensing at Beta |
| Tower and Moat | N | Medium | Monitor | The aggregation layer plus developer portal plus sandbox creates a natural moat over time. But building the moat is premature -- first, build the tower (prove the value). Revisit at Live phase |
| N-sided Markets | N | Medium | Monitor | Platform connects developers (demand side) and departments (supply side). But the N-sided market play requires critical mass on both sides. Currently at zero on both. Revisit when 3+ departments and 50+ developers are active |
| Co-opting and Intercession | LE | Medium | Skip | The platform IS an intermediary between developers and department APIs. But framing this as co-option risks triggering department resistance. Position as enablement, not intercession |
| Embrace and Extend | LE | Low | Skip | Contradicts TCoP open standards mandate. Community backlash risk |
| Channel Disintermediation | N | Low | Skip | Not disintermediating -- adding a new channel alongside existing direct department access |

### Category I: Competitor

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Ambush | N | Low | Skip | No competitors to ambush |
| Fragmentation Play | LE | Low | Skip | No dominant player to fragment against |
| Reinforcing Competitor Inertia | LE | Low | Skip | No competitors with inertia to reinforce |
| Sapping | LE | None | Skip | No competitors |
| Misdirection | CE | None | Skip | CE -- recognise only |
| Restriction of Movement | CE | None | Skip | CE -- recognise only |
| Talent Raid | CE | None | Skip | CE -- recognise only |
| Circling and Probing | N | Low | Skip | No competitors to probe |

### Category J: Positional

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Land Grab | N | Medium | Monitor | The opportunity to establish the definitive UK Government API aggregation platform is time-limited. If departments build their own aggregation or a third party fills the gap, the window closes. But Land Grab requires aggressive investment that Treasury gates constrain. Monitor for window closure signals |
| First Mover / Fast Follower | N | Medium | Monitor | GDS is first mover in UK govt API aggregation. First-mover advantage exists but the risk is building without proven demand. The phased approach mitigates this. Monitor EU and other govt aggregation efforts to determine if fast follower is safer |
| Aggregation | N | High | **Apply** | The ENTIRE PLATFORM is an aggregation play -- consolidating fragmented department APIs into a unified offering. This is not a secondary play; it is the core strategic move. Aggregation creates value by reducing developer integration costs. The value chain is designed around this play |
| Weak Signal / Horizon | N | Medium | Monitor | Watch for: federation standards that could make aggregation unnecessary, department-led improvements that reduce the need for centralisation, EU API catalogue developments. These signals could shift the strategic landscape |

### Category K: Poison

| Play | Alignment | Applicability | Recommendation | Rationale |
|------|-----------|---------------|----------------|-----------|
| Licensing Play | LE | None | Skip | TCoP mandates open source. Licensing play contradicts mandate |
| Insertion | CE | None | Skip | CE -- recognise only. Departments should be aware of insertion risk (the aggregator becoming a dependency they cannot remove). Mitigate by ensuring departments retain direct API access alongside aggregated access |
| Designed to Fail | CE | None | Skip | CE -- recognise only |

---

## Play Compatibility Analysis

### Reinforcing Combinations

| Primary Play | Compatible Play | Why They Reinforce |
|-------------|----------------|-------------------|
| Aggregation | Education | Education explains the value of aggregation to developers and departments; aggregation gives education a concrete product to demonstrate |
| Open Approaches | Co-creation | Openness invites department contribution; co-creation ensures contributions are structured and valued |
| Education | Market Enablement | Education builds understanding; enablement removes practical barriers. Together they create both demand and supply |
| Managing Inertia | Co-creation | Co-creation reduces inertia by giving departments ownership; inertia management ensures co-creation is not blocked by institutional resistance |
| Experimentation | Open Approaches | Open experiments invite community feedback and contribution; openness validates experiments faster |
| Industrial Policy | Managing Inertia | Policy mandate provides authority to overcome inertia; inertia management provides the practical mechanisms |

**High-Value Combination 1**: **Aggregation + Education + Market Enablement** -- Create the aggregated platform, educate developers on its value, and remove practical barriers to adoption. This is the core market-creation thrust.

**High-Value Combination 2**: **Open Approaches + Co-creation + Managing Inertia** -- Open-source the platform to build trust, invite departments to co-create adapters, and actively manage the resistance that will emerge. This is the ecosystem-building thrust.

**High-Value Combination 3**: **Industrial Policy + Experimentation** -- Use the GDS mandate to secure resources and political support for rapid experimentation on the Discovery Engine and normalisation approaches. This is the execution-enablement thrust.

### Conflicting Plays

No conflicts identified among the 7 recommended plays. All are LG or N alignment and reinforce each other. The closest tension is between Industrial Policy (top-down mandate) and Co-creation (bottom-up collaboration) -- but these are complementary when the mandate creates the space for co-creation rather than imposing solutions.

**Resolution**: Ensure Industrial Policy is used to open doors, not to dictate solutions. The GDS mandate should require department participation in co-design, not compliance with a pre-determined architecture.

### Overall Play Coherence

- **Strategic coherence**: All 7 plays tell a consistent story -- create a new market (Aggregation, Education, Market Enablement), build an ecosystem (Open Approaches, Co-creation), and execute effectively (Managing Inertia, Experimentation)
- **Offensive/Defensive balance**: 5 offensive plays (Aggregation, Education, Open Approaches, Experimentation, Market Enablement), 1 defensive play (Managing Inertia), 1 policy play (Industrial Policy). Appropriate for a first-mover with no competitors
- **Alignment profile**: All plays are LG (4) or N (3). No LE or CE plays recommended. Consistent with UK Government values, TCoP, and GDS Service Standard

---

## Selected Plays -- Detailed Execution Plans

### Play 1: Aggregation (N) -- Category J

**Description**: Consolidate fragmented UK Government department APIs into a unified platform that is more valuable than the sum of its parts, reducing developer integration costs by 60%+.

**Why it applies here**: The value chain (ARC-001-WVCH-001-v1.0) is designed around this play. 18 components serve the anchor need of unified API access. The fragmented landscape (8+ departments, each with separate registration, auth, and formats) creates genuine aggregation value.

**Prerequisites**:

- At least one department API onboarded with a working adapter
- API Gateway capable of routing requests to upstream APIs
- Developer Portal with catalogue search and documentation

**Execution Steps**:

1. Build a proof-of-concept aggregating one department API (Companies House recommended -- well-documented REST API, responsive team, high developer demand)
2. Validate the aggregation value proposition with 10 invited developers: does unified access genuinely reduce integration time?
3. If validated, onboard second and third departments (Environment Agency, Ordnance Survey) to prove multi-department aggregation
4. Measure integration time reduction against the 60% target
5. Scale to 8+ departments using the adapter pattern and co-creation model

**Expected Outcomes**:

- **Short-term (0-3 months)**: Working proof-of-concept with one department API accessible through the gateway. Quantified integration time for direct vs. aggregated access
- **Long-term (6-18 months)**: 8+ department APIs aggregated. 100+ developers using the platform. Measurable evidence of integration time reduction

**Risks and Mitigations**:

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Gateway overhead exceeds 50ms target (p95) | Medium | Performance test early with real upstream APIs; select proven API Gateway product |
| Aggregated access adds no meaningful value over direct department access | Low | Validate with real developers at PoC stage before scaling |
| Departments refuse to participate | High | Combine with Managing Inertia and Co-creation plays |

**Success Criteria**:

- [ ] 1 department API accessible through aggregated gateway within 3 months
- [ ] Integration time measured as < 40% of direct department integration
- [ ] 3+ departments onboarded within 9 months
- [ ] 50+ active developers within 12 months

**Review Points**: After PoC (month 3) -- stop/go decision based on developer feedback and performance data

---

### Play 2: Education (LG) -- Category A

**Description**: Inform developers and department API owners about the genuine value of unified government API access, building market understanding before scaling the platform.

**Why it applies here**: The concept of a unified government API gateway is novel (anchor at evolution 0.35). Developers do not know this platform exists. Department API owners may not understand how it benefits them. Education must precede adoption.

**Prerequisites**:

- Working demonstration or prototype (even minimal)
- Clear articulation of developer pain points and how the platform addresses them
- Department benefits case documented (reduced support burden, increased adoption)

**Execution Steps**:

1. Publish a GDS blog post explaining the vision: "One gateway to UK Government APIs"
2. Present at GDS Sprint (the cross-government show-and-tell) with a live demo
3. Create a "Getting Started in 5 Minutes" guide for the Developer Portal
4. Run workshops with 3 target developer communities: GovTech startups, civic tech groups, local authority digital teams
5. Produce a department benefits briefing showing how aggregation reduces support costs
6. Present to the CTO Council to educate department CTOs

**Expected Outcomes**:

- **Short-term (0-3 months)**: 200+ developers aware of the platform through blog and events. 5+ department CTOs briefed
- **Long-term (6-18 months)**: Developer registration growing 20%+ month-on-month. Inbound department interest (departments requesting to join rather than being recruited)

**Risks and Mitigations**:

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Education creates expectations the platform cannot yet deliver | Medium | Clearly communicate current capabilities and roadmap. Label as Alpha/Beta |
| Department CTOs perceive education as GDS self-promotion | Medium | Focus education on developer pain points and department benefits, not GDS mandate |

**Success Criteria**:

- [ ] Blog post published within 1 month; 500+ page views
- [ ] 3+ developer community workshops completed within 6 months
- [ ] Developer awareness survey shows > 30% recognition among target audience within 12 months

**Review Points**: Month 6 -- assess whether education is converting to registrations

---

### Play 3: Open Approaches (LG) -- Category B

**Description**: Open-source the platform code, API specifications, and adapter framework to accelerate adoption, build trust with departments, and invite community contribution.

**Why it applies here**: TCoP Point 3 mandates "be open and use open source." Architecture Principle 20 requires open standards. Open-sourcing directly addresses department concerns about GDS control (stakeholder SD-2) by making the platform transparent and forkable. It also accelerates the Discovery Engine and adapter development through community contribution.

**Prerequisites**:

- Code must be in a publishable state (security review completed, no embedded secrets)
- Clear contribution guidelines and governance model
- Architecture principles document (ARC-000-PRIN-v1.0) already mandates open source

**Execution Steps**:

1. Publish all platform code on GitHub under a permissive licence (MIT or Apache 2.0)
2. Publish the adapter framework as a standalone open-source project that departments can use to create their own adapters
3. Create contribution guidelines following GDS open-source conventions
4. Invite department development teams to contribute adapters for their own APIs
5. Engage the civic tech community (mySociety, Open Data Institute) as contributors and advocates
6. Publish OpenAPI specifications for the platform's own APIs

**Expected Outcomes**:

- **Short-term (0-3 months)**: Code published on GitHub. Initial community engagement (stars, forks, issues)
- **Long-term (6-18 months)**: 3+ external contributors. 2+ department-authored adapters. Community-driven adapter coverage accelerating beyond GDS's internal capacity

**Risks and Mitigations**:

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Publishing reveals security vulnerabilities before they are fixed | Medium | Security review and penetration testing before initial publication |
| Community contributions are low quality or misaligned | Low | Clear contribution guidelines, code review process, and named maintainers |
| Open source reduces GDS's ability to control platform direction | Low | GDS retains project governance; open source does not mean open governance |

**Success Criteria**:

- [ ] Platform code published on GitHub within 3 months of first working code
- [ ] 10+ GitHub stars and 3+ forks within 6 months
- [ ] At least 1 external contribution merged within 12 months

**Review Points**: Month 6 -- assess community engagement metrics

---

### Play 4: Industrial Policy (N) -- Category B

**Description**: Leverage the GDS mandate, TCoP requirements, and ministerial support to drive department adoption of the aggregation platform, using policy authority where market pull alone is insufficient.

**Why it applies here**: Department inertia (stakeholder SD-2) is the primary barrier. Market pull from developers alone will not overcome institutional resistance. The GDS mandate from ministerial authority and TCoP compliance requirements create policy levers that can compel or strongly encourage department participation.

**Prerequisites**:

- Ministerial support confirmed and documented
- TCoP compliance assessment demonstrating the platform meets government standards
- Working prototype demonstrating value (credibility before mandate)

**Execution Steps**:

1. Secure formal endorsement from the GDS Director of Technology as a priority cross-government platform
2. Present the platform to the CTO Council with a request for department participation commitments
3. Include API aggregation readiness in the GDS Service Standard assessment for new government services
4. Frame department participation as TCoP Point 8 compliance ("share, reuse, and collaborate")
5. Use the SRO's programme governance authority to formalise MoU agreements with departments

**Expected Outcomes**:

- **Short-term (0-3 months)**: Formal GDS endorsement secured. CTO Council briefing completed
- **Long-term (6-18 months)**: 5+ departments with signed MoUs. API aggregation referenced in TCoP guidance

**Risks and Mitigations**:

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Heavy-handed mandate triggers department pushback and political resistance | High | Lead with value demonstration, not mandate. Use policy authority as a backstop, not a first move. Combine with Co-creation |
| Political environment changes -- new minister deprioritises the platform | Medium | Build department-level support that survives ministerial changes. Demonstrate value quickly |

**Success Criteria**:

- [ ] GDS Director formal endorsement within 2 months
- [ ] CTO Council briefing within 3 months
- [ ] 3+ department MoUs signed within 9 months

**Review Points**: Month 3 -- assess CTO Council response. If hostile, pivot to Co-creation-first approach

---

### Play 5: Co-creation (LG) -- Category H

**Description**: Collaborate with department API owners to co-develop API adapters, normalisation rules, and governance frameworks, turning potential resistors into co-owners.

**Why it applies here**: Stakeholder analysis (ARC-001-STKE-v1.0) identifies department resistance (SD-2) as the primary risk. Departments fear loss of autonomy and control. Co-creation transforms the relationship from "GDS builds, departments comply" to "we build this together." It also leverages department domain expertise that GDS lacks (each department understands their own APIs better than GDS ever will).

**Prerequisites**:

- Adapter framework designed and documented (so departments can build their own)
- At least one GDS-built adapter as a reference implementation
- Department engagement strategy from stakeholder analysis activated

**Execution Steps**:

1. Identify the most willing department (likely Companies House or Environment Agency based on existing API maturity and community engagement)
2. Run a 2-day co-design workshop with the pilot department: jointly define the adapter interface, normalisation rules, and operational model
3. Department builds their own adapter with GDS providing the framework and guidance
4. Jointly test and deploy the adapter -- both teams share operational responsibility during Beta
5. Document the co-creation process as a playbook for subsequent departments
6. Present the co-creation success story at GDS Sprint to attract further department participation

**Expected Outcomes**:

- **Short-term (0-3 months)**: 1 co-design workshop completed. Pilot department actively contributing to adapter development
- **Long-term (6-18 months)**: 3+ departments building and maintaining their own adapters. Adapter development pace exceeds what GDS alone could deliver

**Risks and Mitigations**:

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Departments lack capacity to contribute to adapter development | High | Provide templates, documentation, and GDS engineering support. Keep department effort minimal |
| Co-created adapters have inconsistent quality | Medium | Define adapter quality standards and automated testing. All adapters pass the same CI/CD pipeline |
| Co-creation slows initial delivery vs. GDS building unilaterally | Medium | Accept slower initial pace as investment in sustainable ecosystem. Build the first adapter alone as proof-of-concept |

**Success Criteria**:

- [ ] 1 co-design workshop completed within 4 months
- [ ] 1 department-authored adapter deployed within 9 months
- [ ] Co-creation playbook published for subsequent departments

**Review Points**: After first workshop -- assess department engagement and willingness to invest time

---

### Play 6: Managing Inertia (N) -- Category F

**Description**: Actively identify and address organisational resistance to change across GDS internal teams and department API owners, ensuring that a strategically sound platform is not defeated by institutional friction.

**Why it applies here**: Doctrine assessment (ARC-001-WDOC-v1.0) identifies inertia management at 3/5 -- partially addressed but not proven. Stakeholder analysis identifies department resistance (SD-2) as the primary barrier, with secondary inertia from Treasury spending gates (SD-5) and NCSC security review processes (SD-4). Internal GDS inertia includes over-documentation without action (14+ artifacts, zero code).

**Prerequisites**:

- Inertia sources mapped (already done in stakeholder analysis)
- Named change champion within GDS
- Working prototype demonstrating value (evidence-based change, not theoretical)

**Execution Steps**:

1. Map all inertia sources in a structured register: department resistance, Treasury gates, NCSC review timelines, GDS internal process overhead
2. For each inertia source, identify the specific concern and the specific evidence that would address it (e.g., departments need to see that the aggregator does not mask abuse patterns)
3. Build evidence proactively: deploy a pilot that generates the data departments need to see
4. Address GDS internal inertia by shifting from documentation to action (doctrine recommendation #1)
5. Assign a named change champion responsible for department engagement
6. Create a quarterly inertia review -- reassess which barriers have been removed and which persist

**Expected Outcomes**:

- **Short-term (0-3 months)**: Inertia register created. Top 3 barriers have specific mitigation plans
- **Long-term (6-18 months)**: Department participation achieved despite initial resistance. Internal GDS delivery pace accelerated

**Risks and Mitigations**:

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Inertia management is itself deprioritised ("we'll deal with resistance when we encounter it") | High | Make inertia management a standing agenda item at programme board. Track it like a risk register |
| Department resistance is deeper than expected -- political, not technical | Medium | Escalate to ministerial level if CTO Council engagement fails. But this is the last resort |

**Success Criteria**:

- [ ] Inertia register created within 1 month
- [ ] 2+ inertia sources resolved within 6 months
- [ ] No department refusal to participate caused by addressable concerns

**Review Points**: Monthly at programme board -- inertia register reviewed alongside risk register

---

### Play 7: Experimentation (LG) -- Category G

**Description**: Rapidly test and iterate on the Discovery Engine and Response Normalisation approaches -- the two custom-built differentiators -- to find the best technical strategies before committing to full implementation.

**Why it applies here**: Discovery Engine [0.42, 0.30] and Response Normalisation [0.48, 0.35] are both in the genesis/custom-built zone. No off-the-shelf solutions exist. The right approach is unknown and must be discovered through experimentation, not analysis. The doctrine assessment flags Bias Towards Action at 2/5 -- experimentation directly addresses this gap.

**Prerequisites**:

- Small, autonomous team (3-5 people) with authority to experiment
- Access to api.gov.uk catalogue data and at least 2 department developer hubs
- Failure budget defined: how many experiments can fail before the approach is abandoned?

**Execution Steps**:

1. Define 3 competing approaches for the Discovery Engine: (a) structured crawling of known department hub URLs, (b) API specification auto-detection via web scanning, (c) department self-registration via admin portal
2. Build a time-boxed spike for each approach (1 week per spike)
3. Measure each approach against: API detection rate, metadata quality, maintenance burden, department effort required
4. Select the winning approach (or hybrid) based on evidence
5. Repeat for Response Normalisation: test rules-based normalisation, schema-mapping normalisation, and AI-assisted normalisation against real department API responses
6. Document findings as ADRs (Architecture Decision Records)

**Expected Outcomes**:

- **Short-term (0-3 months)**: 3+ experiments completed for Discovery Engine. Evidence-based selection of approach. First ADRs published
- **Long-term (6-18 months)**: Validated technical approach for both differentiating components. Confidence to scale implementation

**Risks and Mitigations**:

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Experiments are treated as production development rather than learning exercises | Medium | Define clear experiment boundaries: time-boxed, throw-away code, learning objective stated upfront |
| All approaches fail to achieve acceptable quality | Low | If all Discovery Engine approaches fail, pivot to department self-registration only (admin portal) as the primary catalogue input |

**Success Criteria**:

- [ ] 3+ Discovery Engine experiments completed within 2 months
- [ ] 1 ADR published documenting the selected approach
- [ ] Response Normalisation approach validated against 3+ department API response formats

**Review Points**: Month 2 -- review experiment results. If no viable approach found, escalate to architecture review

---

## Anti-Pattern Check

**Playing in the wrong evolution stage**: No violations identified. Experimentation is applied to genesis-stage Discovery Engine (correct). Aggregation is applied to the overall custom-built platform (correct). No commodity-stage plays are applied to genesis components, and no genesis plays are applied to commodity components.
Status: PASS

**Ignoring inertia**: Addressed via the Managing Inertia play (Play 6). Department resistance is the primary inertia source and has a dedicated play with specific execution steps. GDS internal inertia (over-documentation) is addressed through the Experimentation play.
Status: PASS

**Single-play dependence**: Portfolio of 7 plays across 3 strategic thrusts provides redundancy. If Co-creation fails (departments unwilling), Industrial Policy provides a backstop. If Experimentation on Discovery Engine fails, department self-registration (admin portal) provides a fallback for catalogue population.
Status: PASS

**Misreading evolution pace**: Evolution positions from the WVCH have not been validated against live market data. No WCLM (Climate Assessment) exists to verify evolution velocity. Key risk: API Gateway may be more commoditised than positioned (0.70) -- cloud-native API gateways (AWS API Gateway, Azure API Management) are utility services. This would shift the buy vs. build decision even more firmly toward buy.
Status: WARNING -- API Gateway evolution position should be validated. Consider running `/arckit:wardley.climate` for evolution velocity analysis.

**Ecosystem hubris**: Not yet applicable -- the ecosystem does not exist yet. The Co-creation and Open Approaches plays include mechanisms for generating genuine ecosystem value (department-authored adapters, open-source contributions). No assumption of self-sustaining ecosystem without continued investment.
Status: PASS

**Open washing**: Open Approaches is recommended alongside no conflicting plays. No Licensing Play, Standards Game, or Embrace and Extend plays selected. The open approach is genuine and consistent with TCoP mandate.
Status: PASS

**Anti-Pattern Summary**: 5/6 passed. 1 warning (evolution pace validation for API Gateway).

---

## Case Study Cross-References

| Case Study | Plays Used | Relevance to This Strategy |
|------------|-----------|---------------------------|
| **Ubuntu** | Open Approaches + Alliances + Market Enablement | Most closely parallels the recommended strategy. Ubuntu open-sourced to lower barriers, built alliances with cloud providers, and enabled a market. The API Aggregator should open-source to build trust, ally with departments, and enable the developer market |
| **AWS** | Land Grab + Tower and Moat + Sensing Engines (ILC) | Demonstrates the long-term potential of an aggregation/platform play. AWS aggregated cloud infrastructure components into a unified platform. The API Aggregator aggregates government APIs. AWS's sensing engine (marketplace data) parallels the future Usage Analytics capability |
| **Airbnb** | N-sided Markets + Market Enablement + Defensive Regulation | Demonstrates a two-sided platform connecting supply (departments/APIs) and demand (developers/apps). Airbnb's proactive regulatory engagement parallels the Industrial Policy and Managing Inertia plays needed for department adoption |
| **Google Android** | Open Approaches + Alliances + Insertion | Demonstrates the power of openness to drive adoption against resistant incumbents. Android's open-source model attracted device manufacturers despite their inertia. Caution: Android's Insertion play (embedding Google services) is a CE pattern to avoid |

---

## Recommended Play Portfolio

| Priority | Play | Alignment | Category | Time Horizon | Strategic Thrust |
|----------|------|-----------|----------|--------------|-----------------|
| 1 | Aggregation | N | J: Positional | Immediate (0-3m) | Market Creation |
| 2 | Managing Inertia | N | F: Defensive | Immediate (0-3m) | Execution Enablement |
| 3 | Education | LG | A: User Perception | Immediate (0-3m) | Market Creation |
| 4 | Experimentation | LG | G: Attacking | Immediate (0-3m) | Execution Enablement |
| 5 | Industrial Policy | N | B: Accelerators | Immediate (0-3m) | Market Creation |
| 6 | Open Approaches | LG | B: Accelerators | Short-term (3-12m) | Ecosystem Building |
| 7 | Co-creation | LG | H: Ecosystem | Short-term (3-12m) | Ecosystem Building |

**Plays to Monitor** (revisit at Beta):

| Play | Trigger to Activate |
|------|-------------------|
| N-sided Markets | 3+ departments and 50+ developers active |
| Tower and Moat | Platform proven valuable; need to protect position |
| Sensing Engines / ILC | Live traffic data available to mine |
| Land Grab | Window closing signal detected (competitor or federation standard emerging) |
| Exploiting Network Effects | Critical mass of APIs and developers achieved |

---

## Traceability

| Artifact | Document ID | Relationship |
|----------|-------------|--------------|
| Wardley Value Chain | ARC-001-WVCH-001-v1.0 | Source map providing component positions and evolution stages for play selection |
| Doctrine Assessment | ARC-001-WDOC-v1.0 | Doctrine maturity (2.5/5) constrains play execution; gaps (Bias Towards Action, Be the Owner) directly informed play selection |
| Stakeholder Analysis | ARC-001-STKE-v1.0 | Department inertia (SD-2) and political context informed Managing Inertia and Industrial Policy plays |
| Requirements | ARC-001-REQ-v1.0 | User personas and outcomes validated play applicability |
| Architecture Principles | ARC-000-PRIN-v1.0 | TCoP, open source, and open standards mandates confirmed alignment of LG plays; ruled out LE/CE plays |

---

**Generated by**: ArcKit `/arckit:wardley.gameplay` command
**Generated on**: 2026-03-18 16:00 GMT
**ArcKit Version**: 4.3.1
**Project**: UK Government API Aggregator (Project 001)
**AI Model**: claude-opus-4-6
**Generation Context**: Derived from WVCH (value chain with component positions), WDOC (doctrine maturity), STKE (stakeholder inertia), REQ (personas and outcomes), PRIN (TCoP and open standards constraints)
