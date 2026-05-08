---
name: metrics-review
description: Review metrics ad platform có cấu trúc layered (North Star / Demand / Supply / Quality / Operational) cho B2B Ad Platform Vietnam (Zalo Ads/Adtima). Trigger khi PM cần weekly/monthly metric review, post-launch performance check, anomaly investigation, hoặc setup metric tree cho initiative mới. LUÔN intake scope review và data input. KHÔNG fabricate baseline/target - tag TBD. Có gutcheck cho seasonality, vanity metric, Goodhart effect. Output tiếng Việt, metric name giữ English.
---

# Metrics Review — B2B Ad Platform

## Mục đích

Hỗ trợ PM review metric ad platform với framework layered, tránh vanity metric, surface anomaly, link metric ↔ business outcome.

## Workflow 3 phase

### PHASE 1 — INTAKE (BẮT BUỘC)

Hỏi PM 5 câu:

1. **Scope review** — Toàn platform / 1 product line / 1 initiative / 1 cohort advertiser?
2. **Time window** — Week/month/quarter? So với baseline period nào (WoW / MoM / YoY / vs target)?
3. **Data source** — PM cung cấp data từ Superset (`fiza-bi.zaloapp.com`), Qlik (`qlik.adtima.vn`), Excel export, hay BI tool nào? Skill chỉ phân tích data PM feed.
4. **Mục đích** — Status report / Anomaly investigation / Goal-setting / Post-launch review?
5. **Audience** — Exec (1-page narrative) / Squad (detailed dashboard) / Sales (advertiser-facing summary)?

Nếu PM không có data feed (câu 3): KHÔNG generate fake number. Hỏi: "Anh upload data CSV/screenshot dashboard hoặc paste table không?"

### PHASE 2 — GENERATE THEO FRAMEWORK LAYERED

```markdown
# Metric Review — <Scope> | <Period: YYYY-MM-DD đến YYYY-MM-DD>

**Owner**: <PM> | **Source**: <Superset/Qlik/...>
**Comparison**: <vs WoW / MoM / YoY / target>
**Last updated**: <YYYY-MM-DD>

---

## TL;DR (3 dòng)
- Health overall: 🟢 Green / 🟡 Yellow / 🔴 Red
- Top 1 thing đang work: ...
- Top 1 thing cần attention: ...

---

## LAYER 1 — NORTH STAR

| Metric | Period | vs Prior | vs Target | Verdict |
|---|---|---|---|---|
| Net Revenue / Gross Ad Spend | <value> | +X% | <% to target> | 🟢/🟡/🔴 |
| ARPA (Avg Revenue per Active Advertiser) | ... | ... | ... | ... |

**Insight**: <1-2 câu lý giải, không lặp lại số>
**Action**: <suggested next step nếu Yellow/Red>

---

## LAYER 2 — DEMAND-SIDE HEALTH

| Metric | Value | vs Prior | Note |
|---|---|---|---|
| # Active advertisers (MAA) | ... | ... | ... |
| Advertiser retention (cohort) | ... | ... | ... |
| Time-to-first-spend | ... | ... | ... |
| Campaign success rate (% reach pacing goal) | ... | ... | ... |
| Self-serve activation rate | ... | ... | ... |

**Insight**:
**Anomaly**: <flag bất thường nếu data show>

---

## LAYER 3 — SUPPLY-SIDE HEALTH

| Metric | Value | vs Prior | Note |
|---|---|---|---|
| Fill rate | ...% | ... | ... |
| eCPM | ... | ... | ... |
| Ad load / impressions per session | ... | ... | ... |
| Inventory utilization | ...% | ... | ... |

**Insight**:

---

## LAYER 4 — QUALITY

| Metric | Value | Threshold | Status |
|---|---|---|---|
| Viewability rate | ...% | ≥ MRC standard 50%/1s display, 50%/2s video | 🟢/🟡/🔴 |
| CTR / VTR / completion rate | ... | benchmark | ... |
| IVT rate (GIVT + SIVT) | ...% | < industry benchmark | ... |
| Brand safety incident rate | ...% | < internal threshold | ... |
| User complaint rate | ... | ... | ... |

**Insight**:
**Compliance flag**: <PDPL VN, MRC, IAB violation nếu có>

---

## LAYER 5 — OPERATIONAL

| Metric | Value | SLA | Status |
|---|---|---|---|
| Ad serving latency p95 | ...ms | < target | ... |
| Ad serving latency p99 | ...ms | < target | ... |
| Error rate / no-bid rate | ...% | ... | ... |
| Billing reconciliation accuracy | ...% | ≥ 99.x% | ... |
| Policy review SLA hit rate | ...% | ≥ X% | ... |

**Insight**:

---

## ANOMALY & ROOT CAUSE (nếu có)

| Anomaly | Layer | Magnitude | Hypothesis | Verification needed |
|---|---|---|---|---|
| <e.g. eCPM dropped 18% WoW> | Supply | High | <hypothesis A: seasonality / hypothesis B: bid algorithm change> | <data cần pull> |

---

## SEGMENT BREAKDOWN (nếu data đủ)

Slice theo:
- Advertiser tier (Brand T1 / Agency / SMB)
- Vertical (FMCG / Finance / E-commerce / Auto / ...)
- Format (Display / Video / Native / OA / ZNS)
- Geo (HCMC / Hà Nội / khác)
- Device (Android / iOS / Web)

---

## NEXT 3 ACTIONS (PM commit)
1. [ ] ...
2. [ ] ...
3. [ ] ...
```

### PHASE 3 — GUTCHECK & ANTI-VANITY

AI tự check:

#### G-Check 1: Vanity metric warning
- Nếu PM chỉ pick metric "tăng dễ, không link revenue" (vd. impressions, registered advertiser nhưng không spending) → flag: "Metric này có risk vanity — link với <revenue/retention> chưa rõ."

#### G-Check 2: Goodhart effect risk
- Nếu metric đang được optimize aggressive (vd. CTR) → check guardrail (vd. fraud rate, complaint). Nếu thiếu → flag.
- "When a measure becomes a target, it ceases to be a good measure" — nhắc nếu thấy risk.

#### G-Check 3: Seasonality
- Ad spend VN có seasonality mạnh: Tết (Q1 down), back-to-school (Q3), 11.11/12.12 (Q4 spike), Lunar New Year campaign (pre-Tết Q4). Nếu PM compare WoW không adjust → flag.

#### G-Check 4: Sample size / statistical significance
- Cohort size nhỏ (< X advertiser) → flag: "Confidence thấp, cần aggregate dài hơn."
- Δ < natural variance → flag: "Có thể noise, không phải signal."

## GUARDRAILS

### G1. NO FABRICATE NUMBER
- KHÔNG sinh giá trị metric khi PM không feed data.
- Nếu cần benchmark industry → tag `[GIẢ ĐỊNH benchmark — source year]`, yêu cầu verify.

### G2. NO MISLEADING COMPARISON
- Cảnh báo nếu WoW compare giữa kỳ có Tết, holiday, campaign moment lớn.
- Cảnh báo nếu cohort size khác biệt → KHÔNG so % thẳng.

### G3. EXPLICIT CONFIDENCE
- Mỗi insight tag confidence: `[High — clear data]` / `[Medium — directional]` / `[Low — speculative]`.
- Mỗi root-cause hypothesis phải có "Verification needed" column.

## Metric reference cho B2B Ad Platform

Default metric library (PM có thể thêm/bớt):

### North Star candidates
- Net Revenue
- Gross Ad Spend (GMV)
- ARPA (Avg Revenue per Active Advertiser)
- Take rate × volume

### Demand-side
- MAA (Monthly Active Advertiser), QAA, AAA
- New advertiser acquisition rate
- Advertiser retention (NRR — Net Revenue Retention)
- Churn rate (logo + revenue)
- Time-to-first-spend
- Campaign success rate (reach pacing/objective goal)
- Self-serve activation rate
- Sales-led pipeline (T1/Brand)

### Supply-side
- Fill rate (filled impression / total request)
- eCPM (revenue per 1000 impressions)
- Ad load / impressions per session
- Inventory utilization
- Bid density
- Win rate (per auction)

### Quality (compliance + UX)
- Viewability (MRC: ≥ 50% pixels for 1s display, 2s video)
- CTR / VTR / View-through rate
- Completion rate (video)
- IVT — GIVT (general invalid traffic) + SIVT (sophisticated)
- Brand safety incident rate
- Policy violation rate
- User complaint rate / negative feedback
- Ad relevance score

### Operational
- Ad serving latency p50/p95/p99
- Availability / uptime
- QPS peak
- Error rate / no-bid rate
- Billing reconciliation accuracy
- Policy review SLA hit rate
- Time-to-resolution (incident)
- Cost per impression served (infra cost)

### Financial / Commercial
- Revenue per advertiser tier
- Take rate by product
- Gross margin
- Sales productivity (revenue per AM)
- Discount/rebate %

## Convention

- **Color verdict**: 🟢 ≥ target / 🟡 80-100% target / 🔴 < 80% target.
- **Δ format**: `+X%` hoặc `-X%`, kèm absolute value khi cần.
- **Period notation**: ISO date range, vd. `2026-04-01 → 2026-04-30`.
- **Metric name**: giữ English (eCPM, Fill rate, IVT, MAA, NRR).
- **Confidence tag**: `[High]` / `[Medium]` / `[Low]`.

## Anti-pattern

- Generate report đầy color 🟢 mà không có insight (chỉ là dashboard chữ).
- Compare WoW không adjust seasonality.
- Pick metric ngẫu nhiên, không layered (mix demand + supply + quality lộn xộn).
- Conclusion mạnh từ sample nhỏ.
- Skip operational layer vì "không sexy".
