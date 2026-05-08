---
name: competitive-brief
description: Phân tích cạnh tranh cho B2B Ad Platform Vietnam (Zalo Ads/Adtima). Trigger khi PM cần competitive landscape analysis, deep-dive 1 competitor, feature parity check, pricing benchmark, hoặc battlecard cho Sales. Bake context VN/APAC ad-tech - competitor chính Meta Ads, Google Ads, TikTok Ads, Cốc Cốc Ads, regional players (Trade Desk APAC, Criteo). LUÔN intake scope analysis trước. KHÔNG fabricate market share/pricing data - tag CẦN VERIFY và yêu cầu PM cung cấp source. Output tiếng Việt, term giữ English.
---

# Competitive Brief — B2B Ad Platform VN/APAC

## Mục đích

Hỗ trợ PM ra competitive brief có cấu trúc, tránh "list feature phân biệt theo Wikipedia", tập trung vào insight actionable cho roadmap/positioning/sales.

## Workflow 3 phase

### PHASE 1 — INTAKE (BẮT BUỘC)

Hỏi PM 5 câu:

1. **Mục đích brief** — Roadmap input / Sales battlecard / Positioning / Pricing benchmark / M&A scan? Output sẽ khác nhau đáng kể.
2. **Competitor scope** — Direct competitor (Meta, Google, TikTok, Cốc Cốc cho VN) hay analogous (regional/global ad-tech)? Bao nhiêu competitor (1 deep-dive vs landscape)?
3. **Comparison axis** — Feature parity, pricing, GTM, customer experience, tech (latency/QPS), policy, integration ecosystem? Pick top 3-5.
4. **Data source PM có sẵn** — Public site, sales call note, customer interview, 3rd-party (SimilarWeb, Statista APAC), internal CI? Skill chỉ tổng hợp data PM cung cấp + flag CẦN VERIFY chỗ thiếu.
5. **Audience** — Brief cho Exec (1 page narrative), Roadmap planning (table parity), Sales (battlecard talking points)?

Nếu PM không có data source rõ (câu 4) → cảnh báo: "Output sẽ có nhiều `[CẦN VERIFY]`, chất lượng phụ thuộc vào data anh feed sau."

### PHASE 2 — GENERATE THEO MỤC ĐÍCH

#### Mode A — Roadmap input (feature parity matrix)

```markdown
# Competitive Brief — Roadmap input | <date>

**Scope**: <competitor list> | **Axis**: <comparison axis>
**Source**: <list source PM cung cấp>

---

## Executive summary (5 dòng)
- Top 3 gap mình có vs competitor
- Top 2 advantage mình giữ
- 1 strategic recommendation cho roadmap

## Feature parity matrix

| Feature/Capability | Adtima/Zalo Ads | Meta Ads | Google Ads | TikTok Ads | Cốc Cốc | Gap level |
|---|---|---|---|---|---|---|
| Lookalike audience | ✅ | ✅ Advanced | ✅ Advanced | ✅ | ❌ | Medium |
| Cookieless solution | [CẦN VERIFY] | ✅ Advantage+ | ✅ Privacy Sandbox | ✅ Smart+ | [CẦN VERIFY] | High |
| ... | | | | | | |

Gap level: High / Medium / Low / Parity / Advantage

## Per-competitor deep-dive (nếu < 3 competitor)

### <Competitor A>
**Position trong VN**: [CẦN VERIFY market share data]
**Strength**: ...
**Weakness**: ...
**Recent move (12m)**: <feature launch / pricing change / partnership>
**Implication cho mình**: ...

## Strategic recommendation
1. **Build**: <feature gap đáng đầu tư, rationale>
2. **Differentiate**: <area mình mạnh, double-down>
3. **Park**: <feature competitor có nhưng không đáng đuổi>
```

#### Mode B — Sales battlecard

```markdown
# Battlecard: <Adtima/Zalo Ads> vs <Competitor> | <date>

## Khi gặp customer đang dùng <Competitor>

### Đối thủ — quick view
- Top strength: ...
- Top weakness: ...
- Pricing model: ...
- Typical customer profile: ...

### Win story (mình thắng vì)
1. **<Strength A>**: <1-2 câu, có proof point — case study, customer quote>
2. **<Strength B>**: ...
3. **<Strength C>**: ...

### Loss story (mình thua khi)
- <Scenario>: ...
- Mitigation/talking point: ...

### Talking points cho Sales/AM

**Khi customer nói "Meta cheap hơn":**
> "Meta CPM thấp nhưng eCPM hiệu quả thật phụ thuộc vào audience VN-specific. Zalo có 75M+ MAU và 1P data từ chat/OA — case study X cho thấy ARPA cao hơn Y%."  [CẦN VERIFY case study]

**Khi customer nói "Google reach rộng hơn":**
> "Google reach toàn cầu ưu thế cho web display, nhưng cho mobile-first VN audience, Zalo có thâm nhập app/SMB self-serve mạnh hơn..."  [CẦN VERIFY data]

### Đối thủ pricing (CẦN VERIFY định kỳ)
- CPM benchmark: [CẦN VERIFY — Sales call note hoặc 3P]
- Take rate: [CẦN VERIFY]
- MOQ: [CẦN VERIFY]

### Câu hỏi qualify customer
- "Anh chị đang chạy objective nào trên <Competitor>?"
- "Pain point lớn nhất với <Competitor> là gì?"
- "KPI campaign hiện tại đang đo thế nào?"
```

#### Mode C — Exec brief (1-page)

```markdown
# Competitive Snapshot — <date>

**TL;DR (3 dòng)**: <strategic narrative>

---

## Landscape (1 đoạn)
<Position của mình + competitor chính trong thị trường VN B2B ad>

## Top 3 threat
1. ...
2. ...
3. ...

## Top 3 opportunity
1. ...
2. ...
3. ...

## Recommended action (next 90 days)
- [ ] ...
- [ ] ...

## Source & limitation
- Data tin cậy: <source>
- Data CẦN VERIFY: <area>
- Refresh cadence đề xuất: monthly / quarterly
```

### PHASE 3 — REVIEW

AI tự gutcheck:

- **Source coverage**: nếu > 30% claim ở `[CẦN VERIFY]` → warn "Brief này độ tin cậy thấp, PM cần thu thập thêm data."
- **Anchoring bias**: nếu AI thấy bản thân có xu hướng tô hồng Adtima → flag.
- **Outdated risk**: ad-tech move nhanh. Output luôn có "Refresh cadence: <suggested>".

## GUARDRAILS

### G1. NO FABRICATE COMPETITIVE DATA
- KHÔNG tự sinh market share, ARPA competitor, pricing CPM/CPC, take rate, MAU/DAU competitor.
- Nếu PM không có data → `[CẦN VERIFY — source: ?]`.
- Industry benchmark generic (vd. "Meta CPM ở SEA ~$X") → tag `[GIẢ ĐỊNH benchmark industry, year YYYY]` và yêu cầu PM verify.

### G2. NO ANCHORING TO ADTIMA SIDE
- Phân tích phải fair. Output phải có ít nhất 1 mục Adtima yếu vs competitor (nếu thật sự có).
- Nếu PM input chỉ toàn lợi điểm Adtima → AI hỏi "Còn weakness nào không?".

### G3. CITE ALL CLAIM
- Mọi data point quan trọng phải có source: PM-provided / public / 3P.
- Format: `<claim> [source: SimilarWeb 2025-Q3]` hoặc `[CẦN VERIFY]`.

## Competitor reference (VN/APAC ad-tech)

Default landscape (PM có thể thêm/bớt):

**Direct VN**:
- Zalo Ads / Adtima (mình)
- Meta Ads (Facebook, Instagram)
- Google Ads (Search, Display, YouTube)
- TikTok Ads (TikTok For Business)
- Cốc Cốc Ads
- VNG ecosystem (Zing MP3 Ads, ZaloPay Ads)

**Analogous APAC/Global**:
- Trade Desk (DSP)
- Criteo (retargeting / commerce)
- LINE Ads (Japan/Thailand)
- KakaoTalk Ads (Korea)
- Naver Ads (Korea)
- ShareChat / Moj (India)

**Tech category** (B2B platform tooling):
- AppsFlyer / Adjust / Branch (MMP)
- MOAT / IAS / DV (verification)
- LiveRamp (data clean room)

## Convention

- **Source tag**: `[source: <name>, <date>]` hoặc `[CẦN VERIFY]`.
- **Confidence**: High (≥ 2 source độc lập) / Medium (1 source) / Low (suy luận).
- **Recency**: Mọi data cũ > 6 tháng → tag `[may be outdated]`.
