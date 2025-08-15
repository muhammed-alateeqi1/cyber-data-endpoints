
# Cyber Data Endpoints

**Created by: Muhammed Al-Ateeqi**

A clean set of JSON datasets about cyber incidents, meant to be consumed directly from static hosting (e.g., GitHub Pages) by dashboards, websites, or simple APIs.

> **Version:** v2 (2010 → Today, 10k incidents)  
> **Format:** JSON (minified for production, pretty for review)

---

## Overview (English)

This repository provides consistent, filter‑friendly JSON data for cyber security dashboards.  
In **v2**, we added a **unified incidents dataset**, **daily time series**, and **timeline** arrays to all existing files so every tab/chart can consume the same schema without changing its code.

**Key goals:**
- Single source of truth (**incidents.json**) with 10,000 events (2010 → today).
- Backward compatibility: existing totals remain (e.g., `attackTypes`, `countriesOfOrigin`).
- New **timeline** arrays everywhere (date + type + severity + count).
- Lightweight and static-host friendly.

---

## نظرة عامة (عربي)

المستودع يوفّر بيانات JSON جاهزة للوحات القياس الأمنية.  
في إصدار **v2** أضفنا: **ملف أحداث موحّد**، **سلسلة زمنية يومية**، و**timeline** لكل الملفات القديمة، بحيث تقدر كل التابات والرسومات تستهلك نفس نوع البيانات بدون تغيير في الكود.

**الأهداف:**
- مصدر واحد موحّد (**incidents.json**) يحوي 10,000 حدث من 2010 حتى اليوم.
- المحافظة على التوافق للخلف (الإجماليات القديمة ما زالت موجودة).
- إضافة **timeline** (تاريخ + النوع + الشدة + العدد) لكل الملفات.
- ملفات خفيفة ومناسبة للاستضافة الثابتة.

---

## Hosting & Access

Host the JSON files under any static URL (e.g., `https://<username>.github.io/cyber-data-endpoints/`) and point your client to it.

```ts
// Example (Angular) – src/app/base/baseUrl.ts
export enum baseUrl {
  baseUrl = 'https://<your-pages-domain>/cyber-data-endpoints/'
}
```

---

## File Map

> **New in v2** are marked with 🆕

- **`incidents.json`** 🆕 — unified detailed incidents (10,000 events)
- **`facts_daily_counts.json`** 🆕 — daily counts ready for time-series charts
- **`filters.json`** 🆕 — static options for Attack Type & Severity and the active date range
- **`attacks.json`** — totals + `timeline`
- **`attributions.json`** — original mapping + `summary` + `timeline`
- **`countries.json`** — totals + `timeline`
- **`initiatorCountries.json`** — totals + `timeline`
- **`initiatorTypes.json`** — totals + `timeline`
- **`responses.json`** — totals + `timeline`
- **`sectors.json`** — totals + `timeline`
- **`keyInsights.json`** — short insights in English and Arabic

All JSONs are available in **minified** and **pretty** forms (pretty for review only).

---

## Unified Star‑like Data Model

- **Fact:** `incidents.json` — one record per incident.  
- **Derived facts:** `facts_daily_counts.json` — counts per day, attackType, severity.  
- **Dimensions:** attack type, severity, country, sector, initiator type/country, response, attribution.  
- **Rollups:** each legacy file keeps totals and adds a `timeline` for filters.

---

## Schemas & Examples

> Short snippets only; fields may include more keys if needed.

### 1) `incidents.json` (Unified Events) 🆕
Array under `"incidents"`:

```json
{
  "incidents": [
    {
      "id": "CDE-20240218-1a2b3c4d",
      "timestamp": "2024-02-18T10:42:00Z",
      "date": "2024-02-18",
      "attackType": "Ransomware",
      "severity": "High",
      "targetCountry": "USA",
      "targetSector": "Finance",
      "initiatorCountry": "Russia",
      "initiatorType": "State-Sponsored",
      "response": "Mitigation Applied",
      "attributedTo": "Conti Group",
      "affectedRecords": 52341,
      "estimatedDowntimeHours": 36.5
    }
  ]
}
```

- **Date range (v2):** 2010-01-01 → today  
- **Count (v2):** 10,000 events

---

### 2) `facts_daily_counts.json` (Daily Time‑Series) 🆕
Used directly by time‑series charts and filters:

```json
[
  { "date": "2024-01-01", "attackType": "Phishing", "severity": "Medium", "count": 7 },
  { "date": "2024-01-01", "attackType": "DDoS", "severity": "Low", "count": 3 }
]
```

**Fields**
- `date` – YYYY‑MM‑DD
- `attackType` – string
- `severity` – one of `Critical | High | Medium | Low`
- `count` – integer

---

### 3) `filters.json` (Static Filter Options) 🆕

```json
{
  "attackTypes": ["Phishing", "Ransomware", "DDoS", "..."],
  "severityLevels": ["Critical","High","Medium","Low"],
  "dateRange": { "start": "2010-01-01", "end": "2025-08-13" }
}
```

---

### 4) `attacks.json` (Totals + Timeline)

```json
{
  "attackTypes": [
    { "type": "Phishing", "count": 120 },
    { "type": "Ransomware", "count": 95 }
  ],
  "timeline": [
    { "date": "2024-01-01", "type": "Phishing", "severity": "High", "count": 5 },
    { "date": "2024-01-01", "type": "DDoS", "severity": "Low", "count": 2 }
  ]
}
```

**Fields**
- `attackTypes` – totals (backward compatible)  
- `timeline` – `{ date, type, severity, count }`

---

### 5) `attributions.json` (Mapping + Summary + Timeline)

```json
{
  "attributions": [
    { "attack": "Ransomware", "attributedTo": "Conti Group" },
    { "attack": "DDoS", "attributedTo": "Killnet" }
  ],
  "summary": [
    { "attributedTo": "Conti Group", "count": 341 },
    { "attributedTo": "Killnet", "count": 120 }
  ],
  "timeline": [
    { "date": "2023-11-10", "attackType": "Ransomware", "attributedTo": "Conti Group", "severity": "High", "count": 3 }
  ]
}
```

**Fields**
- `attributions` – original mapping list  
- `summary` – totals per group  
- `timeline` – `{ date, attackType, attributedTo, severity, count }`

---

### 6) `countries.json` (Totals + Timeline)

```json
{
  "countriesOfOrigin": [
    { "country": "USA", "count": 200 },
    { "country": "China", "count": 170 }
  ],
  "timeline": [
    { "date": "2024-05-01", "country": "USA", "attackType": "Phishing", "severity": "Medium", "count": 7 }
  ]
}
```

**Fields**
- `countriesOfOrigin` – totals  
- `timeline` – `{ date, country, attackType, severity, count }`

---

### 7) `initiatorCountries.json` (Totals + Timeline)

```json
{
  "initiatorsCountries": [
    { "country": "Russia", "count": 120 },
    { "country": "China", "count": 100 }
  ],
  "timeline": [
    { "date": "2024-03-15", "country": "Russia", "attackType": "DDoS", "severity": "Low", "count": 2 }
  ]
}
```

---

### 8) `initiatorTypes.json` (Totals + Timeline)

```json
{
  "initiatorsTypes": [
    { "type": "State-Sponsored", "count": 150 },
    { "type": "Cybercriminal Group", "count": 130 }
  ],
  "timeline": [
    { "date": "2024-02-01", "type": "State-Sponsored", "attackType": "Malware", "severity": "Critical", "count": 4 }
  ]
}
```

---

### 9) `responses.json` (Totals + Timeline)

```json
{
  "responses": [
    { "response": "Incident Reported", "count": 300 },
    { "response": "Mitigation Applied", "count": 250 }
  ],
  "timeline": [
    { "date": "2024-04-20", "response": "Mitigation Applied", "attackType": "Ransomware", "severity": "High", "count": 6 }
  ]
}
```

---

### 10) `sectors.json` (Totals + Timeline)

```json
{
  "targetedSectors": [
    { "sector": "Government", "count": 180 },
    { "sector": "Finance", "count": 140 }
  ],
  "timeline": [
    { "date": "2024-07-01", "sector": "Finance", "attackType": "Phishing", "severity": "Medium", "count": 5 }
  ]
}
```

---

### 11) `keyInsights.json`

```json
{
  "keyInsights": [
    "Ransomware remains a major trend.",
    "Since 2023, multiple attack types surged."
  ],
  "keyInsights_ar": [
    "لا يزال الابتزاز (Ransomware) اتجاهًا بارزًا.",
    "منذ 2023 لوحظ ارتفاع في عدة أنواع هجمات."
  ]
}
```

---

## Notes: Minified vs Pretty

- **Minified**: one‑line JSON for production (smaller + faster).  
- **Pretty**: human‑readable with indentation for review.  
Content is identical; only formatting differs.
