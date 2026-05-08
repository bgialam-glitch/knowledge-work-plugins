---
name: roadmap-update
description: Tạo hoặc update product roadmap cho B2B Ad Platform Vietnam (Zalo Ads/Adtima). Trigger khi PM cần build roadmap mới, re-prioritize backlog, plan quarterly OKR, hoặc reshape roadmap theo strategic shift. Hỗ trợ format Now/Next/Later, quarterly themes, OKR-aligned. Bake context ad-tech (advertiser tier, ad format launch, integration DSP/SSP, compliance). LUÔN intake input strategic context trước khi generate. KHÔNG tự sort theo RICE/MoSCoW khi PM chưa cung cấp scoring data. Output tiếng Việt, term giữ English.
---

# Roadmap Update — B2B Ad Platform

## Mục đích

Hỗ trợ Senior PM build/update roadmap cho ad platform với context VN/APAC, link rõ initiative ↔ OKR ↔ guardrail metric.

## Workflow 3 phase

### PHASE 1 — INTAKE (BẮT BUỘC)

Hỏi PM 6 câu trước khi generate:

1. **Strategic horizon** — Roadmap cho quarter, half, hay full year? Theo fiscal nào?
2. **Format** — Now/Next/Later, quarterly theme, hay OKR-aligned table?
3. **Company OKR / North Star** — Top 1-3 OKR cấp company hoặc BU đang follow là gì? Có mục tiêu định lượng?
4. **Initiatives candidate** — Liệt kê initiative đang cân nhắc (PM cung cấp danh sách, không tự nghĩ ra).
5. **Constraint** — Eng capacity (số squad/team)? Budget cap? Dependency cứng (legal, partner, infra)?
6. **Scoring framework** — RICE / Weighted Scoring / Effort×Value / không score (chỉ theo strategic alignment)?

Nếu PM không cung cấp initiative list (câu 4): KHÔNG tự generate initiative giả. Hỏi lại.

### PHASE 2 — GENERATE THEO FORMAT

#### Format A — Now/Next/Later

```markdown
# Roadmap — <BU/Product> | <Quarter Q? FY??>

**Owner**: <PM/Head of Product> | **Last updated**: <YYYY-MM-DD>
**Linked OKR**: <Company OKR ID + statement>

---

## NOW (đang chạy / cam kết quarter này)

| Initiative | Owner | Type | Linked OKR/KR | Target metric | Status | Risk |
|---|---|---|---|---|---|---|
| <Name> | <PM> | Feature/Infra/Compliance | KR-X | <metric: baseline → target> | On track / At risk / Blocked | <key risk> |

## NEXT (next quarter, committed nhưng chưa start)

| Initiative | Owner | Type | Why now | Target metric | Dependency |
|---|---|---|---|---|---|

## LATER (backlog, chưa committed)

| Initiative | Type | Trigger to promote (signal cần thấy) | Estimated effort | Estimated value |
|---|---|---|---|---|

---

## Bets không pursue (explicit)
- <Initiative>: <lý do — capacity / strategic fit / market timing>

## Open questions
- [ ] ...
```

#### Format B — Quarterly Theme

```markdown
# Roadmap Theme — Q? FY??

**Theme**: <1 dòng strategic narrative — vd. "Tăng take rate từ SMB self-serve">
**North Star**: <metric, baseline → target Q-end>
**Linked OKR**: <statement>

---

## Pillar 1: <name, vd. "Demand growth">
**KR contribution**: <%>
**Initiatives**:
- **<Initiative A>** — <1-line outcome>. Owner: <PM>. Effort: <S/M/L>. [Link PRD]
- **<Initiative B>** — ...

## Pillar 2: <name, vd. "Supply quality">
**KR contribution**: <%>
**Initiatives**:
- ...

## Pillar 3: <name, vd. "Operational efficiency">
**KR contribution**: <%>
**Initiatives**:
- ...

---

## Cross-cutting work (compliance, infra, debt)
- ...

## Trade-off / Anti-goal
- KHÔNG làm: ...
```

#### Format C — OKR-aligned Table

```markdown
# Roadmap OKR-aligned — <Period>

## Objective 1: <statement>
| KR | Baseline | Target | Initiative | Owner | Confidence (%) |
|---|---|---|---|---|---|
| KR-1.1 | ... | ... | ... | ... | ... |

## Objective 2: <statement>
| KR | Baseline | Target | Initiative | Owner | Confidence |
|---|---|---|---|---|---|
```

### PHASE 3 — STRATEGIC GUTCHECK

Sau khi generate, AI tự gutcheck (báo cho PM nếu thấy):

- **Capacity stress**: nếu Now > 1.5x squad capacity (rough estimate dựa effort tag) → flag.
- **OKR coverage gap**: nếu KR có < 1 initiative supporting → flag.
- **Concentration risk**: nếu > 70% initiative cùng pillar → flag.
- **Compliance gap**: B2B ad platform thường cần initiative cho PDPL/brand safety/IVT. Nếu roadmap không có → flag.

Output gutcheck dưới roadmap, format:
```
## Gutcheck từ skill
- [WARNING] <observation>
- [SUGGEST] <follow-up question>
```

## GUARDRAILS

### G1. NO FABRICATE INITIATIVE
- KHÔNG tự nghĩ ra initiative không có trong list PM cung cấp.
- KHÔNG tự gán effort estimate (S/M/L hoặc Story Points) khi PM không có Eng input.

### G2. MARK ASSUMPTION
- `[GIẢ ĐỊNH]` cho confidence, target, dependency chưa verify.
- `[CẦN ENG ESTIMATE]` cho effort.
- `[CẦN OKR ALIGNMENT REVIEW]` nếu link KR yếu.

### G3. RESPECT SCORING FRAMEWORK
- Chỉ score initiative theo framework PM chọn (câu 6 intake).
- KHÔNG ép RICE nếu PM nói không score.

## Convention

- **Initiative type tag**: Feature / Infra / Compliance / Tech-debt / Experiment / Partnership.
- **Effort**: S (≤ 1 sprint) / M (1-2 sprint) / L (≥ 3 sprint) [CẦN ENG ESTIMATE confirm].
- **Status**: On track / At risk / Blocked / Done / Killed.
- **Priority signal**: Now (committed, in flight), Next (committed, not started), Later (backlog).

## Ad-platform-specific consideration

Khi generate roadmap, AI nên cân nhắc các loại initiative thường có ở B2B ad platform:

- **Demand-side**: campaign objective mới, advertiser self-serve UX, agency tooling, MMP integration
- **Supply-side**: inventory expansion (new placement, new format), publisher tool, yield optimization
- **Quality**: brand safety, IVT prevention, viewability, MRC compliance
- **Pricing**: new pricing model, take rate experiment, discount automation
- **Reporting**: advertiser dashboard, attribution, incrementality test
- **Compliance**: PDPL VN, Nghị định 13/2023, IAB Tech Lab signal (TCF, GPP)
- **Infra**: ad serving latency, QPS scaling, cost optimization

Nếu PM bỏ qua hẳn 1 area (vd. không có compliance trong list) → gutcheck flag.

## Anti-pattern

- Generate roadmap đẹp nhưng không link OKR.
- Auto-prioritize bằng RICE khi PM chưa có data.
- Fill "Later" bằng generic initiative để cho đủ visual.
- Ép template Now/Next/Later khi team đang dùng quarterly theme.
