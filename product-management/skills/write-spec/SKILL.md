---
name: write-spec
description: Viết PRD (Product Requirement Document) cho B2B Ad Platform Vietnam (Zalo Ads/Adtima). Trigger khi user cần tạo product spec, feature spec, requirement doc cho campaign objective mới, targeting capability mới, billing model mới, integration DSP/SSP/MMP, dashboard reporting feature, hoặc bất kỳ feature/initiative nào trên ad platform. Hỗ trợ 2 mode - Lite cho feature ≤ 2 sprints single team, Full cho strategic bet multi-quarter cross-team. LUÔN intake 5-7 câu critical trước khi generate. KHÔNG fabricate số liệu - nếu PM không cung cấp data thì tag TBD. Output tiếng Việt, field technical giữ English.
---

# Write Spec — B2B Ad Platform PRD

## Mục đích

Hỗ trợ Senior PM ở B2B Ad Platform (Zalo Ads/Adtima context) viết PRD chuẩn, tối ưu thời gian dev/QC bằng Acceptance Criteria format Given/When/Then và test scenarios explicit.

## Workflow 3 phase

### PHASE 1 — INTAKE (BẮT BUỘC, không bỏ qua)

Trước khi generate, hỏi PM 7 câu critical. Nếu PM trả lời thiếu, KHÔNG generate, hỏi tiếp đến khi đủ:

1. **Problem statement & evidence** — Vấn đề là gì? Có data/customer quote/incident gì làm bằng chứng?
2. **Hypothesis** — Nếu giải quyết, kỳ vọng tác động gì (định lượng được)?
3. **Target user/advertiser** — Persona chính? Advertiser tier nào (Brand T1, Agency, SMB self-serve)? Publisher 1P hay 3P?
4. **Success metric** — Primary metric + 1-2 guardrail. Baseline hiện tại bao nhiêu?
5. **Constraint** — Timeline cứng? Eng cost cap? Compliance constraint (PDPL VN, Nghị định 13/2023)?
6. **Anti-goal** — Cái gì explicit KHÔNG làm trong scope này?
7. **Mode** — PM muốn Lite (≤ 2 sprints, single team) hay Full (multi-quarter, cross-team)?

Nếu PM không có data cho câu 1-4: tag `[CẦN VERIFY]` hoặc `[CẦN BASELINE]` trong output, KHÔNG tự fabricate.

### PHASE 2 — GENERATE THEO MODE

#### LITE MODE (feature ≤ 2 sprints, single team)

```markdown
# PRD: <Feature Name>

**PM**: <name> | **Eng Lead**: TBD | **Designer**: TBD
**Status**: Draft | **Last updated**: <YYYY-MM-DD>
**Mode**: Lite

---

## WHY

### 1. Problem statement
<Vấn đề user/advertiser đang gặp, 3-5 dòng>
**Evidence**: <data point / customer quote / incident link>

### 2. Hypothesis & Business impact
**Hypothesis**: Nếu <làm X>, thì <kỳ vọng Y> bởi vì <lý do Z>.
**Expected impact**: <định lượng — revenue, ARPA, retention, etc.> [CẦN VERIFY nếu PM không có baseline]

### 3. Success metric
- **Primary**: <metric, baseline → target, measurement window>
- **Guardrail**: <metric không được giảm dưới ngưỡng>

---

## WHAT

### 4. User stories
- As a <advertiser tier / publisher / internal user>, I want <action>, so that <outcome>.
- (3-5 user story chính)

### 5. Scope
**In-scope**:
- ...

**Out-of-scope** (explicit):
- ...

### 6. Acceptance Criteria
Format Given/When/Then. Mỗi user story → 2-4 AC.

**AC-1.1**: Given <precondition>, When <action>, Then <expected result>.
**AC-1.2**: ...

---

## HOW

### 7. Functional spec
- UI flow / screen behavior (đính kèm wireframe link nếu có)
- API behavior / data flow
- Đủ chi tiết để dev estimate Story Points

### 8. Non-functional
- Latency / performance budget
- Error handling
- Edge case (null, timeout, concurrent, fraud signal)

### 9. Test scenarios
- Happy path: ...
- Edge case: ...
- Negative case: ...
- Compliance check: PDPL VN consent, brand safety filter

---

## ROLLOUT

### 10. Release plan
- Feature flag: <name>
- Rollout %: <internal → 1% → 10% → 100%>
- Rollback trigger: <metric breach>
- Monitoring: <dashboard link / alert>

### 11. Open questions & dependencies
- [ ] <Question for Eng/Legal/Sales>
- [ ] <Dependency on team X>
```

#### FULL MODE (strategic bet, multi-quarter, cross-team)

```markdown
# PRD: <Initiative Name>

**Owner**: <PM> | **Sponsor**: <Head of Product / GM>
**Eng Lead**: TBD | **Designer**: TBD | **Data**: TBD | **Legal review**: TBD
**Status**: Draft | **Last updated**: <YYYY-MM-DD>
**Mode**: Full
**Tier**: Strategic Bet

---

## WHY

### 1. Context & market signal
- VN/APAC ad-tech landscape relevant
- Competitive context (Meta, Google, TikTok, Cốc Cốc, regional players)
- Trigger event (advertiser feedback, market shift, regulatory)

### 2. Problem & opportunity
- Problem dài hạn cần giải quyết
- Size of opportunity [CẦN VERIFY — PM cung cấp TAM/SAM/SOM hoặc tag CẦN VERIFY]

### 3. Goals, hypothesis, North Star + guardrails
- **North Star**: <metric>, baseline → target, timeline
- **Hypothesis**: ...
- **Leading indicators**: ...
- **Lagging indicators**: ...
- **Guardrails**: <metric không được giảm>

### 4. Anti-goals (explicit không làm)
- ...

---

## WHAT

### 5. Stakeholders & personas
| Persona | Tier/role | Pain point | Win condition |
|---|---|---|---|
| Advertiser Brand T1 | Enterprise direct | ... | ... |
| Agency | Mid-market | ... | ... |
| SMB self-serve | Long tail | ... | ... |
| Publisher 1P | Zalo property | ... | ... |
| Internal Sales/AM | Commercial | ... | ... |

### 6. User stories / use cases (theo persona)
- (5-15 user story, group by persona)

### 7. Functional requirements
- **Campaign setup**: objective, targeting, creative, budget, schedule
- **Delivery & pacing**: bid logic, frequency cap, dayparting
- **Billing & reconciliation**: invoice cycle, dispute flow, write-off
- **Reporting**: advertiser-facing + publisher report + internal BI

### 8. Acceptance Criteria
Per requirement, format Given/When/Then. Có thể dài → break theo functional area.

**AC for Campaign Setup**:
- AC-CS-1: Given <...>, When <...>, Then <...>
- ...

**AC for Delivery**:
- ...

### 9. Scope
**Phase 1 (Alpha internal)**:
**Phase 2 (Managed Beta T1)**:
**Phase 3 (GA)**:
**Out of scope (this initiative)**:

---

## HOW

### 10. Non-functional
- Ad serving latency: p95 < <ms>, p99 < <ms>
- QPS target: <X> peak
- Availability: 99.9% / 99.95%
- Brand safety: < <X>% incident rate
- IVT: < <X>% (per MRC standard)

### 11. Targeting & inventory
- Taxonomy mapping (IAB v3.0 / custom)
- Frequency cap rule
- Cookieless / 1P data strategy

### 12. Pricing & billing model
- Pricing model: CPM / CPC / CPV / CPA / CPL
- MOQ: <amount> [CẦN VERIFY pricing committee]
- Take rate: <%> [GIẢ ĐỊNH nếu chưa confirm]
- Billing cycle: net 30 / net 45

### 13. Creative & policy
- Format spec (size, weight, duration)
- Policy review SLA: <X hours>
- Auto-reject vs manual review rule

### 14. Integration
- DSP/SSP partner: <list>
- MMP: AppsFlyer / Adjust / Branch
- 3P verification: MOAT / IAS / DV
- API contract: <link to spec>

### 15. Data model & API contract
- Entity: Campaign / LineItem / Creative / Insertion Order
- Key field schema
- API endpoint list (link to OpenAPI doc)

### 16. Test plan / QC scenarios
- Test plan derived from AC ở section 8
- Integration test với DSP/SSP partner
- Load test scenario
- Compliance test: PDPL VN, MRC viewability, brand safety

### 17. Risk & mitigation
| Risk | Impact | Likelihood | Mitigation |
|---|---|---|---|
| Fraud (IVT spike) | High | Medium | IAS/DV integration trước GA |
| Brand safety incident | High | Low | Pre-bid filtering + post-bid monitoring |
| PDPL VN compliance (Nghị định 13/2023) | High | Medium | Legal review trước Beta |
| ... | | | |

---

## ROLLOUT

### 18. Phased rollout
- **Alpha (internal)**: <date>, scope: <X advertisers internal>
- **Managed Beta**: <date>, scope: <Y T1 advertisers>, AM hand-hold
- **GA**: <date>, full self-serve

### 19. Migration / deprecation
- Feature thay thế cái nào không?
- Deprecation timeline cho legacy
- Customer communication plan

### 20. Monitoring & success review
- Dashboard: <link Superset/Qlik>
- Review cadence: weekly trong 4 tuần đầu, monthly sau đó
- Success/kill criteria: <explicit threshold>

---

## APPENDIX

### 21. Wireframes / mockups
<Figma link>

### 22. Open questions & dependencies
- [ ] <Question for Legal>
- [ ] <Dependency on Data team>
- [ ] <Cross-team coordination needed>

### 23. Glossary
- **eCPM**: effective Cost Per Mille
- **IVT**: Invalid Traffic
- **MRC**: Media Rating Council
- ... (term mới với reader)
```

### PHASE 3 — REVIEW & ITERATE

Sau khi generate, hỏi PM:
- Có section nào AI giả định nhưng PM muốn replace bằng data thật không?
- Cần expand AC cho area nào (thường Eng request thêm AC ở complex area)?
- Stakeholder profile output cho ai (skill khác `/stakeholder-update` xử lý)?

## GUARDRAILS (BẮT BUỘC tuân thủ)

### G1. NO FABRICATE NUMBERS
- KHÔNG tự sinh số market share, ARPA, conversion rate, CTR, eCPM, cost.
- Nếu PM không cung cấp data → ghi `TBD — PM fill từ Superset/Qlik/research/Customer interview`.
- Nếu cần benchmark → tag `[GIẢ ĐỊNH benchmark industry]` và yêu cầu PM verify.

### G2. MARK ASSUMPTION EXPLICIT
- Mọi assumption không có evidence → `[GIẢ ĐỊNH]`.
- Mọi metric không có baseline → `[CẦN BASELINE]`.
- Mọi yêu cầu cần legal/compliance check → `[CẦN LEGAL REVIEW]`.

### G3. INTAKE FIRST
- KHÔNG generate khi 7 câu intake chưa đủ.
- Nếu PM nói "skip intake, viết luôn" → vẫn generate nhưng output đầy `[CẦN VERIFY]` placeholder và warn PM ở đầu doc.

## Convention

- **Ngôn ngữ**: Tiếng Việt.
- **Term technical giữ English**: Sprint, Story Points, Epic, AC, eCPM, fill rate, viewability, IVT, brand safety, cookieless, frequency cap, OKR, North Star, MRC, OpenRTB, DSP, SSP, MMP, MOQ, take rate.
- **AC format**: Given/When/Then, đánh số AC-X.Y.
- **Date**: ISO YYYY-MM-DD.
- **Compliance reference**: PDPL VN, Nghị định 13/2023/NĐ-CP, MRC, IAB Tech Lab.

## Anti-pattern (KHÔNG làm)

- Sinh PRD đầy buzzword "synergy", "leverage", "best-in-class".
- Fill section bằng generic text khi không có input PM.
- Auto-prioritize MoSCoW/RICE khi PM không cung cấp scoring data.
- Skip AC vì "phức tạp quá".
- Translate term technical sang tiếng Việt nửa vời (vd. "khả dụng" cho availability — giữ "availability").
