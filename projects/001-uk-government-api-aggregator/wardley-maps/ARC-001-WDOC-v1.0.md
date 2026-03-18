# Wardley Doctrine Assessment: UK Government API Aggregator

> **Template Origin**: Official | **ArcKit Version**: 4.3.1 | **Command**: `/arckit.wardley.doctrine`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-WDOC-v1.0 |
| **Document Type** | Wardley Doctrine Assessment |
| **Project** | UK Government API Aggregator (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-03-18 |
| **Last Modified** | 2026-03-18 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-06-16 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Programme Board, Architecture Team, Leadership |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-18 | ArcKit AI | Initial doctrine assessment from `/arckit:wardley.doctrine` command | [PENDING] | [PENDING] |

---

## Executive Summary

**Overall Maturity Score**: 2.5 / 5.0 -- Developing

**Phase Positioning**:

| Phase | Name | Score | Status |
|-------|------|-------|--------|
| Phase I | Stop Self-Harm | 3.0 / 5.0 | In Progress |
| Phase II | Becoming More Context Aware | 2.5 / 5.0 | In Progress |
| Phase III | Better for Less | 2.3 / 5.0 | Not Started |
| Phase IV | Continuously Evolving | 1.6 / 5.0 | Not Started |

**Critical Findings**:

1. Strong user-needs foundation (personas, stakeholder analysis, requirements traceability) but no learning-by-doing -- 14+ architecture artifacts exist with zero code, prototypes, or experiments
2. Decision-making authority is heavily centralised (GDS Director, SRO, Architecture Review Board, Treasury gates) creating bottlenecks that conflict with the speed needed for a platform in a competitive government landscape
3. Document ownership is entirely unassigned -- every artifact has `[OWNER_NAME_AND_ROLE]` in the owner field, indicating accountability has not been embedded despite thorough governance documentation

The organisation has invested heavily in understanding users and documenting requirements (Phase I strengths) but has not yet translated this understanding into action, learning, or distributed execution capability. The gap between documentation quality and execution readiness is the primary risk to this programme.

---

## Strategy Cycle Context

| Element | Summary |
|---------|---------|
| **Purpose** | Deliver a unified aggregation platform for UK Government APIs, reducing developer integration friction across departments and demonstrating GDS's mandate for cross-government digital platforms. Purpose is clearly stated in requirements (ARC-001-REQ-v1.0) and stakeholder analysis. |
| **Landscape** | Value chain (ARC-001-WVCH-001-v1.0) identifies 18 components. Two custom-built differentiators (Discovery Engine at evolution 0.30, Response Normalisation at 0.35) sit alongside product-stage components (API Gateway at 0.70, Developer Registration at 0.72) and commodity infrastructure (Cloud Hosting at 0.90). The strategic challenge is building the novel components while leveraging commodities -- but the organisation has not yet started building anything. |
| **Climate** | UK Government regulatory environment imposes significant constraints: TCoP compliance, GDS Service Standard assessment gates, NCSC security guidance, Treasury spending reviews, and DPIA requirements. Department resistance to centralisation (stakeholder SD-2) creates political friction. The API landscape is evolving -- departments are publishing new APIs independently, and the window of opportunity for a centralised aggregator may close if departments adopt federation or industry standards render bespoke aggregation unnecessary. |
| **Leadership** | Decision-making is centralised. The GDS Director of Technology is executive sponsor with HIGH power/HIGH interest. Programme governance runs through an SRO with monthly board reviews. Architecture decisions require Architecture Review Board approval. Treasury controls budget through phase gates. This governance model prioritises control and accountability but risks slow execution in a domain where the landscape is evolving. |

---

## Doctrine Assessment Matrix

Score key: **1** = Not practised | **2** = Ad hoc | **3** = Developing | **4** = Mature | **5** = Cultural norm

### Phase I: Stop Self-Harm

| Category | Principle | Score (1-5) | Evidence | Improvement Action |
|----------|-----------|:-----------:|----------|--------------------|
| Communication | Common Language | 3 | Consistent document naming conventions (ARC-001-xxx). Architecture principles use defined terminology. Stakeholder analysis uses shared vocabulary. But no formal glossary published. | Create a project glossary (`/arckit:glossary`) and mandate its use in all communications. |
| Communication | Challenge Assumptions | 3 | Stakeholder analysis explicitly identifies conflicts (C-1: speed vs. control, C-2: openness vs. security). Value chain documents 6 assumptions and 4 open questions. But no formal assumption-challenge process or devil's advocate role. | Institute assumption reviews at phase gates. Assign a named challenger for each architecture decision. |
| Communication | Understand Context | 3 | Stakeholder power-interest grid created. Value chain maps visibility and evolution. Strategy cycle context established. But context is captured in documents -- no evidence it flows into day-to-day decisions. | Use Wardley Maps in sprint planning and decision meetings, not just governance documents. |
| Development | Know Your Users | 4 | Four well-defined personas (Alex, Sam, Jordan, Pat) with pain points, goals, and proficiency levels. 15+ stakeholders mapped with engagement strategies. Requirements trace to user research. | Validate personas with real user research. Confirm pain points through interviews, not assumption. |
| Development | Focus on User Needs | 4 | Value chain anchor is a genuine user need ("Developer can build applications using UK Government data through a single integration point"). All 6 business requirements trace to stakeholder drivers. Use cases start from user perspective. | Maintain user-need anchoring through implementation. Create a "needs wall" visible to the team. |
| Development | Remove Bias & Duplication | 2 | Architecture principles mention open standards (reducing vendor bias). But no formal process for identifying duplication across government (e.g., does a similar aggregator already exist within GDS or departments?). No diverse review panel documented. | Conduct a cross-government landscape scan for existing API aggregation efforts. Establish diverse review for architecture decisions. |
| Development | Use Appropriate Methods | 3 | Phased delivery (Discovery/Alpha/Beta/Live) aligned with GDS Service Standard. Architecture principles mention agile. But no explicit mapping of methodology to component evolution stage -- the same document-heavy approach is applied to custom-built differentiators and commodity components alike. | Map methodologies to component evolution: use rapid prototyping for Discovery Engine (genesis), product evaluation for API Gateway (product stage), procurement for Cloud Hosting (commodity). |
| Operation | Know the Details | 3 | Requirements include detailed acceptance criteria (42+ criteria across FR-001 to FR-016). Architecture principles specify validation gates. But project is pre-implementation -- operational details are aspirational, not tested. | Build a proof-of-concept for the critical path (API Gateway to upstream API) to validate assumptions with real operational detail. |
| Learning | Systematic Learning | 2 | Architecture principles mention ADRs but none have been created yet. No lessons-learned framework, retrospective process, or knowledge management system documented. Learning appears incidental, not structured. | Establish ADR practice immediately. Schedule retrospectives at each phase gate. Create a learning log. |

**Phase I Average**: 3.0 / 5.0

---

### Phase II: Becoming More Context Aware

| Category | Principle | Score (1-5) | Evidence | Improvement Action |
|----------|-----------|:-----------:|----------|--------------------|
| Communication | Bias Towards Open | 3 | Architecture principles mandate open source, open standards, open data (Principles 19, 20). TCoP alignment includes "be open and use open source." But openness applies to technology outputs -- no evidence of open decision-making, open roadmaps, or transparent prioritisation within the team. | Publish decision rationale openly (ADRs). Make the roadmap and backlog visible to all stakeholders. |
| Development | Focus on Outcome | 3 | Requirements define measurable outcomes (O-1 through O-5: 500+ developers, 60% time reduction, 8+ departments). But 16+ detailed functional requirements with 42+ acceptance criteria suggest over-specification of solution rather than outcome focus. | Reduce functional requirement detail at this stage. Focus on outcome metrics and let implementation teams determine the "how." |
| Development | Think FIRE | 2 | No evidence of FIRE principles. Requirements are comprehensive and detailed for a project with no code. The scope is ambitious (8+ departments, 500+ developers in 12 months) without evidence of a minimal viable scope. FIRE would suggest starting with 1-2 departments and 10 developers. | Define a Minimum Viable Platform: one department (Companies House), sandbox only, 10 beta developers. Prove the value chain works before scaling. |
| Development | Use Appropriate Tools | 2 | Architecture principles are deliberately technology-agnostic ("principles describe WHAT, not HOW"). No tool evaluation or selection has occurred. Cloud research exists (AWS and Azure) but no tool decisions made. | Conduct tool selection for the critical path: API Gateway product, identity provider, cloud platform. Use evolution stage to guide buy vs. build. |
| Development | Be Pragmatic | 2 | Requirements scope is ambitious for a pre-alpha project. 20 architecture principles, 6 business requirements, 16 functional requirements, 15 non-functional requirements -- all defined before any code or prototype. Pragmatism would suggest starting smaller and learning. | Reduce scope for Alpha to the minimum needed to test the core hypothesis: can a gateway add value between developers and a single department API? |
| Development | Use Standards | 4 | Strong standards adoption: OpenAPI for API specs, OAuth 2.0 for auth, WCAG 2.2 AA for accessibility, ISO 8601 for dates, JSON for data, TCoP, GDS Service Standard, NCSC CAF. Well-documented in both principles (ARC-000-PRIN) and requirements (ARC-001-REQ). | Continue. Ensure standards are applied in implementation, not just documented in architecture. |
| Operation | Manage Inertia | 3 | Stakeholder analysis explicitly identifies department resistance as the primary inertia source (SD-2: "Departments fear loss of autonomy"). MoU framework and co-design workshops proposed as mitigation. But inertia management is planned, not proven. | Engage the most willing department first (likely Companies House or Environment Agency based on existing API maturity). Build momentum through success, not mandates. |
| Operation | Manage Failure | 3 | Architecture principles mandate circuit breakers, fault isolation, and graceful degradation for technical failure. Requirements include exception flows. But no evidence of organisational failure management -- no blameless retrospective process, no failure budget, no experimentation safe space. | Establish a blameless incident review process. Define a failure budget for Alpha phase -- expected failure rate for experiments. |
| Operation | Effectiveness over Efficiency | 3 | Value chain distinguishes custom-built differentiators from commodity components (correct strategic focus). Requirements prioritised with MoSCoW. But no evidence of explicitly validating that the right things are being built before optimising how they are built. | Before building, validate: do developers actually want a unified gateway, or just better documentation? Run user research to confirm the value proposition. |
| Learning | Bias Towards Action | 2 | 14+ architecture artifacts produced with no code, prototype, or experiment. Good documentation quality but learning has come from analysis, not from doing. The project would benefit from a spike or proof-of-concept to validate assumptions. | Build a working proof-of-concept within 4 weeks: API Gateway proxying to one department API. Learn from building, not just documenting. |
| Leading | Move Fast | 2 | Multiple governance gates slow decision-making: Treasury spending review, GDS Service Standard assessment, SRO programme board, Architecture Review Board, department MoU negotiations. Each gate adds latency. The phased model (Discovery/Alpha/Beta/Live) is sound but execution pace is unknown. | Reduce approval chains for Alpha decisions. Delegate technical decisions to the delivery team within agreed guardrails. Reserve board-level decisions for phase gates only. |
| Leading | Strategy is Iterative | 3 | Phased delivery model with stop/go gates suggests iterative capability. Architecture documentation is versioned (v1.0, v1.1). But no evidence of strategy being revisited after initial creation -- all artifacts are v1.0 or v1.1. | Schedule a quarterly strategy review using Wardley Maps. Update the value chain and evolution positions based on what is learned in each phase. |
| Structure | Think Small Teams | 2 | No team structure decisions documented. GDS traditionally uses multidisciplinary teams (service teams of 6-10), but no explicit team design for this programme. | Design team structure using Pioneer/Settler/Town Planner model: a small pioneer team (3-5) for Discovery Engine and Response Normalisation; a settler team for Developer Portal and Gateway. |
| Structure | Distribute Power | 2 | Power is concentrated: GDS Director (HIGH power, decision authority), SRO (programme accountability), Architecture Review Board (technical oversight). Stakeholder analysis shows bottom-heavy interest (developers, local authorities have HIGH interest but LOW power). | Define decision rights matrix: which decisions can the delivery team make autonomously, which require escalation? Push technical decisions to the team. |
| Structure | Aptitude & Attitude | 2 | No evidence of hiring criteria, team composition planning, or talent management approach. No Pioneer/Settler/Town Planner thinking applied to staffing. | Define team roles needed for each component's evolution stage. Hire pioneers for Discovery Engine; seek settlers with API gateway product experience. |

**Phase II Average**: 2.5 / 5.0

---

### Phase III: Better for Less

| Category | Principle | Score (1-5) | Evidence | Improvement Action |
|----------|-----------|:-----------:|----------|--------------------|
| Operation | Optimise Flow | 2 | No evidence of value stream mapping or flow optimisation. Project is pre-implementation with no delivery pipeline to optimise. Backlog exists (ARC-001-BKLG-v1.0) but no flow metrics. | Establish delivery flow metrics (lead time, cycle time, deployment frequency) from the start of Alpha. |
| Operation | Do Better with Less | 2 | Value for money requirement exists (BR-005: 1.5:1 cost-benefit ratio) but is output-focused. No evidence of continuous improvement culture or systematic resource efficiency. | Build cost tracking into the platform from day one. Review resource utilisation quarterly. |
| Operation | Exceptional Standards | 3 | Architecture principles set high standards: security is "NON-NEGOTIABLE," WCAG 2.2 AA required, performance targets defined ( < 50ms gateway overhead). Standards are clearly stated but aspirational until tested against implementation. | Convert standards into automated tests and CI/CD quality gates. Standards that are not measured are not standards. |
| Learning | Bias Towards New | 3 | Value chain identifies custom-built components requiring innovation (Discovery Engine at evolution 0.30). Architecture principles encourage cloud-first. DataScout (ARC-001-DSCT-v1.0) shows exploration of data sources. But no systematic innovation programme or protected experimentation time. | Allocate 20% of Alpha team capacity to exploring alternative approaches for the Discovery Engine. Test multiple crawling strategies. |
| Leading | Commit to Direction | 3 | Clear project objectives and phased delivery plan. GDS Director sponsorship provides political commitment. But direction has not been tested through execution -- commitment is easy when nothing has been built yet. | Maintain direction through first implementation challenges. Use phase gates to validate direction, not to add scope. |
| Leading | Be the Owner | 2 | Every document has `[OWNER_NAME_AND_ROLE]` as the owner -- ownership is literally unassigned across all 15+ artifacts. SRO is identified in stakeholder analysis but document-level ownership is absent. | Assign named owners to every artifact and every component on the value chain within 2 weeks. Ownership without a name is not ownership. |
| Leading | Inspire Others | 2 | No evidence of vision communication beyond formal governance documents. The project vision ("unified government API access") is compelling but appears locked in architecture artifacts rather than communicated broadly. | Publish a public blog post on the GDS blog about the vision. Create a one-page project story for stakeholder engagement. |
| Leading | Embrace Uncertainty | 2 | Open questions documented (Q-01 through Q-04 in the value chain). But uncertainty is treated as something to resolve before acting, not something to act within. The volume of documentation suggests a desire for certainty before execution. | Accept that Q-01 through Q-04 will be answered by building, not by analysis. Start with what is known and iterate. |
| Leading | Be Humble | 2 | No evidence of humility practices: no retrospectives, no external review, no peer feedback mechanisms. Architecture artifacts are internally produced without external challenge. | Invite external review of architecture decisions. Conduct a pre-mortem: "assume this project fails in 12 months -- why?" |
| Structure | Seek the Best | 2 | Cloud research exists (AWS and Azure) but focused on service comparison, not on seeking best-in-class approaches to the aggregation problem. No benchmarking against similar platforms (e.g., API aggregators in other governments or private sector). | Benchmark against: EU API catalogue, Singapore NDI, private-sector aggregators (RapidAPI, Kong). Learn from their approaches. |
| Structure | Purpose, Mastery, Autonomy | 2 | No evidence of intrinsic motivation design. Team structure and developer experience not addressed. The governance model emphasises control and accountability, which can undermine autonomy. | Design team structures that provide autonomy within guardrails. Define clear boundaries where teams can act without escalation. |

**Phase III Average**: 2.3 / 5.0

---

### Phase IV: Continuously Evolving

| Category | Principle | Score (1-5) | Evidence | Improvement Action |
|----------|-----------|:-----------:|----------|--------------------|
| Learning | Listen to Ecosystem | 2 | DataScout document (ARC-001-DSCT-v1.0) shows some ecosystem awareness -- external data sources and APIs catalogued. Stakeholder analysis includes external stakeholders (open data community, NAO, PAC). But no systematic mechanism for ongoing ecosystem listening. | Establish regular developer community engagement (quarterly meetups, feedback surveys). Monitor department API roadmaps for changes that affect the platform. |
| Leading | Exploit the Landscape | 2 | Value chain and evolution positions created but not yet used for strategic exploitation. No gameplay analysis performed. The map exists as documentation, not as a strategic tool being actively used. | Run `/arckit:wardley.gameplay` to identify strategic plays. Use the value chain in leadership discussions, not just architecture reviews. |
| Leading | There is No Core | 1 | Not addressed anywhere in existing artifacts. The platform is treated as the permanent core product. No evidence of willingness to pivot, sunset components, or consider that the aggregation need might be met differently in the future (e.g., by federation standards or department-led improvements). | Add a "strategic exit criteria" section to the programme business case. Under what conditions would the platform be retired or replaced? |
| Structure | No Single Culture | 1 | No evidence of cultural diversity design. No Pioneer/Settler/Town Planner thinking. The project appears to operate with a single governance-heavy culture applied uniformly to all components -- the same heavyweight process for the novel Discovery Engine and the commodity Cloud Hosting. | Differentiate working practices by component evolution: lightweight, experimental process for genesis-stage components; disciplined procurement for commodity components. |
| Structure | Design for Constant Evolution | 2 | Architecture principles mandate maintainability and evolvability (Principle 15) and loose coupling (Principle 10). Adapter pattern enables new API integration without core changes. But structural evolution (team, process, governance) is not designed for change. | Build evolution into the governance model: quarterly re-assessment of team structure, decision rights, and methodology fit. |

**Phase IV Average**: 1.6 / 5.0

---

## Detailed Phase Findings

### Phase I: Stop Self-Harm -- Detailed Findings

**Phase Score**: 3.0 / 5.0

**Strongest principles in this phase**:

- Know Your Users (Score: 4) -- Four well-defined personas with pain points, goals, and proficiency levels. Comprehensive stakeholder mapping with power-interest grid and engagement strategies. This is the strongest foundation in the entire assessment.
- Focus on User Needs (Score: 4) -- Value chain anchored to a genuine user need. All business requirements trace to stakeholder drivers. Use cases written from user perspective with clear actor identification.

**Weakest principles in this phase**:

- Systematic Learning (Score: 2) -- No ADRs created despite being referenced in principles. No lessons-learned framework, retrospective process, or knowledge management. Learning is incidental, not structured.
- Remove Bias & Duplication (Score: 2) -- No landscape scan for existing government API aggregation efforts. No diverse review panels. Potential duplication with existing GDS platforms (GOV.UK, api.gov.uk) not formally assessed.

**Phase I Narrative**:

The organisation has strong user-understanding foundations -- personas, stakeholder analysis, and requirements traceability are well above average for a government programme at this stage. However, this understanding has not been paired with systematic learning processes. The project has generated significant architecture documentation but has no mechanism to capture what it learns from that documentation process or from stakeholder engagement. The risk is that the user understanding becomes a snapshot rather than a living capability.

---

### Phase II: Becoming More Context Aware -- Detailed Findings

**Phase Score**: 2.5 / 5.0

**Strongest principles in this phase**:

- Use Standards (Score: 4) -- Comprehensive standards adoption documented across principles and requirements: OpenAPI, OAuth 2.0, WCAG 2.2 AA, ISO 8601, TCoP, GDS Service Standard, NCSC CAF. Standards are well-chosen and well-documented.
- Manage Inertia (Score: 3) -- Department resistance explicitly identified as the primary inertia source with a mitigation strategy (MoUs, co-design workshops, bilateral agreements). This is unusual self-awareness for a centralising programme.

**Weakest principles in this phase**:

- Think FIRE (Score: 2) -- The project scope is ambitious without evidence of minimal viable definition. Comprehensive requirements before any code suggests over-specification rather than fast, restrained, elegant delivery.
- Bias Towards Action (Score: 2) -- 14+ artifacts with zero code, prototypes, or experiments. The project has prioritised analysis over action, which is common in government but risks building the wrong thing with high confidence.
- Move Fast (Score: 2) -- Multiple governance layers (Treasury, GDS assessment, SRO board, ARB, department negotiations) create decision latency. Speed of execution is unknown but governance structure suggests slow.
- Think Small Teams / Distribute Power / Aptitude & Attitude (Score: 2 each) -- Team and organisational structure is entirely unaddressed. No team design, no decision rights matrix, no staffing model.

**Phase II Narrative**:

The organisation is beginning to develop situational awareness -- the value chain, stakeholder mapping, and inertia identification demonstrate emerging context sensitivity. However, this awareness has not yet translated into action. The most concerning pattern is the combination of high documentation output with low experimentation output. Phase II requires turning awareness into capability, which means building, testing, and learning -- none of which has started. The structural principles (small teams, distributed power, aptitude) are entirely unaddressed, suggesting the organisation has not yet considered how to organise for execution.

---

### Phase III: Better for Less -- Detailed Findings

**Phase Score**: 2.3 / 5.0

**Strongest principles in this phase**:

- Exceptional Standards (Score: 3) -- Architecture principles set genuinely high standards (security non-negotiable, WCAG 2.2 AA, performance targets). Standards are clearly stated and traceable to requirements.
- Bias Towards New (Score: 3) -- Custom-built components identified for innovation (Discovery Engine). DataScout shows willingness to explore external data sources.
- Commit to Direction (Score: 3) -- Clear objectives and phased plan with political sponsorship.

**Weakest principles in this phase**:

- Be the Owner (Score: 2) -- Ownership is literally absent: every artifact has `[OWNER_NAME_AND_ROLE]` as a placeholder. This is a symbolic indicator of a deeper accountability gap.
- Inspire Others / Embrace Uncertainty / Be Humble (Score: 2 each) -- Leadership maturity practices are not evidenced. Vision communication is confined to governance documents. Uncertainty is treated as a problem to solve, not a condition to operate within.

**Phase III Narrative**:

Phase III maturity requires operational experience that this project does not yet have. The high aspirational standards are a strength, but they have not been tested against reality. The most actionable gap is ownership -- assigning named owners to artifacts and components would immediately improve accountability and decision-making speed. Leadership maturity practices (humility, uncertainty tolerance, inspiration) are typical Phase III gaps for government programmes that rely on formal governance structures.

---

### Phase IV: Continuously Evolving -- Detailed Findings

**Phase Score**: 1.6 / 5.0

**Strongest principles in this phase**:

- Listen to Ecosystem (Score: 2) -- Some ecosystem awareness through DataScout and stakeholder analysis, though mechanisms are not systematic.
- Design for Constant Evolution (Score: 2) -- Architecture principles support evolution through loose coupling and adapter patterns.

**Weakest principles in this phase**:

- There is No Core (Score: 1) -- No consideration of strategic impermanence. The platform is treated as a permanent fixture rather than a temporary strategic position.
- No Single Culture (Score: 1) -- No cultural diversity design. A single governance-heavy approach applied to all components regardless of evolution stage.

**Phase IV Narrative**:

Phase IV scores are expected to be low for a project at this maturity level -- these are advanced organisational capabilities that most government programmes never reach. The key insight is not that scores are low, but that two principles score 1 (not practised at all): "There is No Core" and "No Single Culture." These represent blind spots rather than gaps. The organisation has not considered that the aggregator platform itself may be temporary, or that different components need different cultural approaches to management and delivery.

---

## Previous Assessment Comparison

This is the initial assessment. No previous scores are available for comparison.

---

## Critical Gaps

| Rank | Phase | Category | Principle | Current Score | Target Score | Business Impact |
|------|-------|----------|-----------|:-------------:|:------------:|-----------------|
| 1 | I | Learning | Systematic Learning | 2 | 4 | Without structured learning, the project will repeat mistakes across phases. No ADRs means decisions are not traceable. No retrospectives means the same governance friction will persist without correction. Learning compounds -- every month without systematic learning is a month of wasted insight. |
| 2 | II | Learning | Bias Towards Action | 2 | 4 | 14+ artifacts with no code or experiments means all assumptions are untested. The Discovery Engine's feasibility, the API Gateway's performance overhead, and the developer onboarding flow are all theoretical. Delayed validation increases the cost of being wrong. |
| 3 | II | Structure | Distribute Power / Think Small Teams | 2 | 3 | Centralised decision-making through GDS Director, SRO, and ARB creates bottlenecks. Without team structure and decision rights, execution will be slow and decisions will queue behind governance gates. The programme cannot move at the speed the evolving API landscape requires. |
| 4 | III | Leading | Be the Owner | 2 | 4 | Every artifact has unassigned ownership (`[OWNER_NAME_AND_ROLE]`). Without named owners, no one is accountable for keeping documents current, making decisions, or driving outcomes. Collective ownership is no ownership. |
| 5 | I | Development | Remove Bias & Duplication | 2 | 3 | No landscape scan for existing aggregation efforts risks building something that already exists or duplicates department-level improvements. Bias toward building a centralised platform may not be validated against alternatives (federation, standards adoption, enhanced api.gov.uk). |

---

## Implementation Roadmap

### Immediate Actions (0-3 months)

| Action | Principle(s) Addressed | Owner | Success Criteria |
|--------|----------------------|-------|------------------|
| Assign named owners to all 15+ artifacts and all 18 value chain components. Every `[OWNER_NAME_AND_ROLE]` replaced with a real name and role. | Be the Owner | SRO | 100% of documents have named owners within 2 weeks |
| Build a working proof-of-concept: API Gateway proxying requests to one department API (Companies House recommended). Deploy in 4 weeks. | Bias Towards Action, Know the Details | Delivery Lead | Working PoC deployed to sandbox; at least one API call successfully proxied end-to-end |
| Establish ADR practice: create first ADR documenting the decision to start with Companies House as the pilot department. | Systematic Learning | Enterprise Architect | First ADR published within 1 week; template established for all subsequent decisions |
| Run `/arckit:glossary` to generate a project glossary from existing artifacts. Distribute to all stakeholders. | Common Language | Architecture Team | Glossary published and referenced in all subsequent documents |
| Conduct a cross-government landscape scan: does a similar API aggregation initiative already exist within GDS, departments, or devolved governments? | Remove Bias & Duplication | Enterprise Architect | Scan completed; findings documented; any duplication risks identified and mitigated |

### Short-Term Actions (3-12 months)

| Action | Principle(s) Addressed | Owner | Success Criteria |
|--------|----------------------|-------|------------------|
| Define decision rights matrix: which decisions the delivery team can make autonomously vs. which require escalation to ARB or SRO. Aim for 80%+ team-level decisions. | Distribute Power, Move Fast | SRO | Decision rights matrix published; delivery team reports > 80% of technical decisions made without escalation |
| Design team structure using Pioneer/Settler/Town Planner model. Small pioneer team (3-5) for Discovery Engine; settler team for Developer Portal and Gateway integration. | Think Small Teams, Aptitude & Attitude, No Single Culture | Delivery Lead | Team structure defined and staffed; each team has < 8 members with clear scope boundaries |
| Implement delivery flow metrics (lead time, cycle time, deployment frequency, change failure rate) from the start of Beta. | Optimise Flow, Do Better with Less | Delivery Lead | Metrics dashboard live; reviewed at each sprint retrospective |
| Benchmark against comparable platforms: EU API catalogue, Singapore NDI, RapidAPI developer experience, Kong Gateway architecture. | Seek the Best, Listen to Ecosystem | Enterprise Architect | Benchmark report produced; 3+ actionable improvements identified and prioritised |
| Establish quarterly strategy review using Wardley Maps. Update value chain evolution positions based on what has been learned. Reassess doctrine. | Strategy is Iterative, Challenge Assumptions | Enterprise Architect | First quarterly review completed; at least 2 component positions adjusted based on evidence |
| Define a Minimum Viable Platform scope for Private Beta: one department, sandbox + production, 10 invited developers. | Think FIRE, Be Pragmatic | Product Owner | MVP scope defined and agreed; scope is < 30% of full FR-001 to FR-016 requirements |

### Long-Term Actions (12-24 months)

| Action | Principle(s) Addressed | Owner | Success Criteria |
|--------|----------------------|-------|------------------|
| Establish systematic ecosystem listening: developer community meetups (quarterly), department API roadmap monitoring, cross-government digital strategy tracking. | Listen to Ecosystem | Service Owner | Quarterly community events running; feedback systematically captured and acted upon |
| Add strategic exit criteria to the programme business case: under what conditions would the platform be retired, replaced by federation, or merged with api.gov.uk? | There is No Core | SRO | Exit criteria documented and reviewed annually at programme board |
| Differentiate working practices by component evolution stage: lightweight experimental process for genesis-stage components, structured product management for product-stage, procurement discipline for commodity. | No Single Culture, Use Appropriate Methods | Delivery Lead | Different governance applied to different component types; evidence in team retrospectives |
| Build continuous improvement into governance: quarterly re-assessment of team structure, decision rights, methodology fit, and doctrine scores. | Design for Constant Evolution, Do Better with Less | Enterprise Architect | Second doctrine assessment (ARC-001-WDOC-v2.0) shows measurable improvement in Phase I and II scores |

---

## Recommendations

1. **Start building before documenting further**
   - **Rationale**: The project has 14+ architecture artifacts and zero working code or prototypes. The highest-impact action is to build a proof-of-concept that validates the core value chain (Gateway -> upstream API) within 4 weeks. This addresses the critical Bias Towards Action gap and will generate more learning than another round of documentation.
   - **Expected Benefit**: Validated (or invalidated) assumptions about gateway overhead, upstream API integration complexity, and developer experience. Real operational data to inform architecture decisions.
   - **Risk of Inaction**: Continued investment in documentation without validation. If core assumptions are wrong (e.g., gateway overhead exceeds 50ms, or department APIs resist proxying), the later the discovery, the more expensive the correction.

2. **Assign ownership and distribute decision-making power**
   - **Rationale**: Every document has `[OWNER_NAME_AND_ROLE]` as a placeholder. Decision-making is concentrated in GDS Director, SRO, and ARB. This combination means no one is accountable for artifacts and everyone must escalate decisions. The result is slow, unaccountable governance.
   - **Expected Benefit**: Named owners drive document currency and decision speed. Distributed decision rights reduce bottlenecks. Teams move faster when they can act within clear guardrails.
   - **Risk of Inaction**: Governance theatre -- comprehensive documentation with no one responsible for keeping it current or acting on it. Decisions queue behind governance gates while the API landscape evolves around the programme.

3. **Design for different cultures across the value chain**
   - **Rationale**: The Discovery Engine (evolution 0.30, genesis/custom) and Cloud Hosting (evolution 0.90, commodity) require fundamentally different management approaches. Currently, a single governance-heavy culture applies to all components. This over-governs innovation and under-governs operations.
   - **Expected Benefit**: Faster innovation on differentiating components. More disciplined procurement and operations for commodity components. Teams matched to work that suits their aptitude.
   - **Risk of Inaction**: Pioneer-type work (Discovery Engine) smothered by Town Planner governance. Commodity procurement (Cloud Hosting) treated as novel when it should be routine. Both types of work performed poorly because the management approach fits neither.

---

## Traceability

| Artifact | Document ID | Relationship |
|----------|-------------|--------------|
| Architecture Principles | ARC-000-PRIN-v1.0 | Doctrine principles assessed against stated architecture principles; gaps between stated principles and practiced doctrine identified |
| Wardley Value Chain | ARC-001-WVCH-001-v1.0 | Landscape and evolution context for this assessment; component evolution stages inform methodology and culture recommendations |
| Stakeholder Analysis | ARC-001-STKE-v1.0 | Leadership culture, decision-making authority, inertia sources, and stakeholder engagement patterns assessed |
| Requirements | ARC-001-REQ-v1.0 | User needs, personas, and outcome focus assessed; over-specification pattern identified |

---

**Generated by**: ArcKit `/arckit:wardley.doctrine` command
**Generated on**: 2026-03-18 15:00 GMT
**ArcKit Version**: 4.3.1
**Project**: UK Government API Aggregator (Project 001)
**AI Model**: claude-opus-4-6
**Generation Context**: Assessed from ARC-000-PRIN-v1.0 (Principles), ARC-001-STKE-v1.0 (Stakeholders), ARC-001-REQ-v1.0 (Requirements), ARC-001-WVCH-001-v1.0 (Value Chain); no previous WDOC exists
