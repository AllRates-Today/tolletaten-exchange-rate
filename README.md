# Norwegian Customs (Tolletaten) Exchange Rates API — tolletaten-exchange-rate

[![npm version](https://img.shields.io/npm/v/tolletaten-exchange-rate.svg)](https://www.npmjs.com/package/tolletaten-exchange-rate)
[![license](https://img.shields.io/npm/l/tolletaten-exchange-rate.svg)](https://github.com/AllRates-Today/tolletaten-exchange-rate/blob/main/LICENSE)
[![zero dependencies](https://img.shields.io/badge/dependencies-0-brightgreen.svg)](https://www.npmjs.com/package/tolletaten-exchange-rate)
[![TypeScript](https://img.shields.io/badge/TypeScript-types%20included-3178C6.svg)](https://www.typescriptlang.org/)
[![USD/NOK today](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fallratestoday.com%2Fapi%2Fopen%2Fcentral-bank%2Ftolletaten%3Fsource%3DUSD%26target%3DNOK&query=%24.rate&label=USD%2FNOK%20official%2C%20Norwegian%20Customs%20(Tolletaten)&color=0A7E8C&cacheSeconds=3600)](https://allratestoday.com/tax-authority-rates-api/tolletaten/)
[![rate date](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fallratestoday.com%2Fapi%2Fopen%2Fcentral-bank%2Ftolletaten%3Fsource%3DUSD%26target%3DNOK&query=%24.rate_date&label=rate%20date&color=555&cacheSeconds=3600)](https://allratestoday.com/tax-authority-rates-api/tolletaten/)

**Official Norwegian Customs (Tolletaten) (Norway) fortnightly exchange rates for Node.js and TypeScript. The published tax authority rates behind tax filings, customs valuations, audits, and compliant invoicing — not market estimates, but the numbers Norwegian Customs (Tolletaten) itself prints, about every fortnight.**

## 🚀 Why this client?

- 🏛️ **Official rates** — Norwegian Customs (Tolletaten)'s own table, with the publisher's own `rate_date` on every response
- 📅 **History back to 2021** — point-in-time tables and daily series for any past date
- 🔀 **Official vs derived, always flagged** — computed inverse/cross pairs carry `derived: true`, never mixed with official prints
- ⚡ **Zero dependencies** — pure ESM + CJS over global `fetch`; Node 18+, Bun, Deno, and edge runtimes
- 🔷 **Type-safe** — full TypeScript definitions shipped with the package
- 🧾 **Compliance-grade metadata** — `rate_type`, publication date, and source disclaimer on every response

> **Official rate, not mid-market:** every value here is a number Norwegian Customs (Tolletaten) itself published, fixed once printed and carrying the tax authority's own `rate_date` — what filings and audits require. Need the live mid-market rate for pricing or display instead? Use the [mid-market API](https://allratestoday.com/docs/) or [`@allratestoday/sdk`](https://www.npmjs.com/package/@allratestoday/sdk). The two can diverge by several percent.

## 🔑 Get your API key

Get a free API key at [allratestoday.com/register](https://allratestoday.com/register) — no credit card required. Latest rates are on every plan, including free.

## 📈 Latest official table

[![Latest Norwegian Customs (Tolletaten) table](https://allratestoday.com/api/open/central-bank/tolletaten/table.svg)](https://allratestoday.com/tax-authority-rates-api/tolletaten/)

The image is rendered live from the keyless endpoint, so it follows the tax authority's publications on npm and on GitHub alike without a new release. The same table as text is folded below for search and copy-paste: on GitHub [a daily Action](.github/workflows/daily-table.yml) refreshes it whenever the tax authority publishes a new table; on npm it is as of the package's publish date.

<!-- daily-table:start -->
<details>
<summary>Table as text: published 2026-11-12 by Norwegian Customs (Tolletaten) — 22 rates. Updated 2026-11-25.</summary>

| Base | Quote | Type | Rate |
| --- | --- | --- | ---: |
| AUD | NOK | reference | 6.564 |
| CAD | NOK | reference | 6.661 |
| CHF | NOK | reference | 11.3107 |
| CNY | NOK | reference | 1.4014 |
| CZK | NOK | reference | 0.42901 |
| DKK | NOK | reference | 1.3987 |
| EUR | NOK | reference | 10.454 |
| GBP | NOK | reference | 12.472 |
| HKD | NOK | reference | 1.191 |
| HUF | NOK | reference | 0.02845 |
| INR | NOK | reference | 0.09817 |
| JPY | NOK | reference | 0.05935 |
| KRW | NOK | reference | 0.00705 |
| NZD | NOK | reference | 5.308 |
| PKR | NOK | reference | 0.03377 |
| PLN | NOK | reference | 2.374 |
| RON | NOK | reference | 1.9551 |
| SEK | NOK | reference | 0.9386 |
| SGD | NOK | reference | 7.297 |
| THB | NOK | reference | 0.27642 |
| USD | NOK | reference | 9.344 |
| ZAR | NOK | reference | 0.561 |

</details>

Source: [Official rates published by TOLLETATEN, served by AllRatesToday](https://allratestoday.com/tax-authority-rates-api/tolletaten/). Rates are as printed by the tax authority; AllRatesToday is not affiliated with it.
<!-- daily-table:end -->

## 📦 Installation

```bash
npm install tolletaten-exchange-rate
```

```bash
yarn add tolletaten-exchange-rate
```

```bash
pnpm add tolletaten-exchange-rate
```

Requires Node 18+ (global `fetch`); also runs on Bun, Deno and edge runtimes. Also published under the org scope as [`@allratestoday/tolletaten-exchange-rate`](https://www.npmjs.com/package/@allratestoday/tolletaten-exchange-rate) — same code, same versions.

## 🏁 Quick start

```js
import { getRate } from 'tolletaten-exchange-rate';

const pair = await getRate('USD', 'NOK', { apiKey: 'art_live_...' });
console.log(pair.rate, pair.rate_date); // the official Norwegian Customs (Tolletaten) rate, on the tax authority's own date
```

## 📚 API reference

- [Latest pair rate](#latest-pair-rate) — one pair from the latest official table
- [Full official table](#full-official-table) — everything the tax authority printed, in one call
- [Table for a date](#table-for-a-date) — the official table for an invoice or filing date
- [Daily time series](#daily-time-series) — one pair across a date range

---

### Latest pair rate

Free plan and up. Pairs the tax authority does not print directly are resolved from its table and flagged (see *Official vs derived rates* below).

```js
const pair = await getRate('USD', 'NOK', { apiKey: 'art_live_...' });
```

**Response:**

```javascript
{
  bank: 'tolletaten',
  name: 'Norwegian Customs (Tolletaten)',
  rate_date: '2026-11-12',   // Norwegian Customs (Tolletaten)'s own publication date
  source: 'USD',
  target: 'NOK',
  rate: 9.344,
  rate_type: 'reference',
  derived: false,
  method: 'published',
  disclaimer: 'Official rates as published by the named central bank. On weekends/holidays the most recent published rate_date is returned.'
}
```

### Full official table

Free plan and up. The complete table for the latest publication date.

```js
import { getLatestRates } from 'tolletaten-exchange-rate';

const table = await getLatestRates({ apiKey: 'art_live_...' });
console.log(table.rate_date, table.rates.length);
```

**Response:**

```javascript
{
  bank: 'tolletaten',
  name: 'Norwegian Customs (Tolletaten)',
  rate_date: '2026-11-12',
  rates: [
    { "base": "USD", "quote": "NOK", "type": "reference", "value": 9.344 },
    // … the rest of the official table (22 currencies vs NOK)
  ],
  disclaimer: '…'
}
```

### Table for a date

Paid plans. The official table for any date since 2021 — weekends and holidays return the most recent published date, flagged via `published_on_requested_date`, which is exactly the in-force rate a filing needs.

```js
import { getRatesForDate } from 'tolletaten-exchange-rate';

const day = await getRatesForDate('2026-06-30', { apiKey: 'art_live_...' });
// Optionally narrow to one pair:
const one = await getRatesForDate('2026-06-30', { apiKey: 'art_live_...', source: 'USD', target: 'NOK' });
```

**Response:**

```javascript
{
  bank: 'tolletaten',
  requested_date: '2026-06-30',
  rate_date: '2026-06-30',                // the date actually published
  published_on_requested_date: true,      // false when a weekend/holiday fell back
  rates: [ /* the full table for that date */ ],
  disclaimer: '…'
}
```

### Daily time series

Paid plans. One resolved rate per publication date — ready for charting, revaluation runs, or audit workpapers.

```js
import { getHistory } from 'tolletaten-exchange-rate';

const series = await getHistory(
  { source: 'USD', target: 'NOK', from: '2026-01-01', to: '2026-11-12' },
  { apiKey: 'art_live_...' }
);
```

**Response:**

```javascript
{
  bank: 'tolletaten',
  source: 'USD',
  target: 'NOK',
  from: '2026-01-01',
  to: '2026-11-12',
  count: 152,
  rates: [
    // one entry per publication date
    { date: '2026-11-12', rate: 9.344, rate_type: 'reference', derived: false, method: 'published' },
    // …
  ],
  disclaimer: '…'
}
```

Pass `{ symbol: 'USD' }` instead of `source`/`target` to get the raw published rows for one currency (all rate types, no pair resolution).

---

## 🗺️ Currencies covered

Norwegian Customs (Tolletaten) currently publishes rates covering **22 currencies** against the NOK (as of the latest table):

🇦🇺 `AUD` · 🇨🇦 `CAD` · 🇨🇭 `CHF` · 🇨🇳 `CNY` · 🇨🇿 `CZK` · 🇩🇰 `DKK` · 🇪🇺 `EUR` · 🇬🇧 `GBP` · 🇭🇰 `HKD` · 🇭🇺 `HUF` · 🇮🇳 `INR` · 🇯🇵 `JPY` · 🇰🇷 `KRW` · 🇳🇿 `NZD` · 🇵🇰 `PKR` · 🇵🇱 `PLN` · 🇷🇴 `RON` · 🇸🇪 `SEK` · 🇸🇬 `SGD` · 🇹🇭 `THB` · 🇺🇸 `USD` · 🇿🇦 `ZAR`

## 🏛️ Source

Tolletaten's conversion rates (omregningskurser): the NOK rate per foreign currency fixed in advance for each two-week period, used to convert the invoice currency into NOK for the customs value on Norwegian customs declarations (box 22).

- Publisher's own page: [Customs conversion rates (omregningskurser)](https://data.toll.no/dataset/valutakurs) · [data.toll.no](https://data.toll.no/)
- Publication: about every fortnight; the exact schedule, freshness status and any current delay are on the [Norwegian Customs (Tolletaten) rates page](https://allratestoday.com/tax-authority-rates-api/tolletaten/)
- Values are stored unmodified, with the publisher's own `rate_date` on every row — see the [methodology](https://allratestoday.com/official-rates-methodology/)

## 🧭 Reading the numbers

- `value` is always **quote currency per 1 unit of base currency** (`base: "EUR", quote: "USD", value: 1.15` means 1 EUR = 1.15 USD).
- Norwegian Customs (Tolletaten) quotes **NOK per 1 unit of foreign currency** (e.g. `base: "USD", quote: "NOK"` means NOK per one US dollar).
- Need the other way round? Ask `getRate(target, source)` and the API inverts or crosses for you, flagged `derived: true` — never divide a published rate yourself in a compliance workflow.
- `rate_type` tells you which of the tax authority's series a row belongs to (`reference` here); some publishers print buy/sell or several fixings for the same pair.

## 🧩 ERP & accounting systems

Loading the official Norwegian Customs (Tolletaten) rate into an accounting system is a supported workflow, not a hack. Step-by-step guides with the direction each system expects:

- [Dynamics 365 Business Central](https://allratestoday.com/docs/integrations/business-central/) — built-in Currency Exchange Rate Service, no code
- [Xero](https://allratestoday.com/docs/integrations/xero/) · [QuickBooks Online](https://allratestoday.com/docs/integrations/quickbooks/) · [SAP S/4HANA and ECC](https://allratestoday.com/docs/integrations/sap/) · [Odoo](https://allratestoday.com/docs/integrations/odoo/)

The same keyed endpoints return `?format=csv`, `?format=xml` and `?format=xlsx`, and accept the key as `?api_key=` on the URL for importers that cannot send headers:

```bash
curl "https://allratestoday.com/api/v1/central-bank/tolletaten/latest?format=xml&api_key=art_live_..."
```

## 🤖 AI agents

- MCP server: `npx -y @allratestoday/central-bank-mcp` (stdio) or the hosted endpoint `https://allratestoday.com/api/mcp` — tools for official rates, history, cross-bank comparison and publication calendars
- Already using the general SDK or MCP server? Since 2026-10-01 [`@allratestoday/sdk`](https://www.npmjs.com/package/@allratestoday/sdk) 1.4+ has `officialRates('tolletaten')` and [`@allratestoday/mcp-server`](https://www.npmjs.com/package/@allratestoday/mcp-server) 0.6+ has a `get_official_rates` tool — both return this source's latest table with no key, so you can add it without a second dependency
- Claude Code plugin (no key): `/plugin marketplace add AllRates-Today/claude-code-plugin` then `/plugin install allratestoday@allratestoday` — bundles both MCP servers plus an `/official-rate tolletaten ...` command
- Evaluating? Agents can self-issue a trial key with no signup: `POST https://allratestoday.com/api/agent/keys` (send `Content-Type: application/json`) returns a 100-call key valid 7 days that covers the free-plan methods (latest table, pairs); dated tables and history need a [paid plan](https://allratestoday.com/pricing/). The MCP servers expose it as `request_trial_key`
- Machine-readable site guide: [llms.txt](https://allratestoday.com/llms.txt) · [for-ai-agents](https://allratestoday.com/for-ai-agents/)

## ⚖️ Official vs derived rates

If Norwegian Customs (Tolletaten) does not print a pair directly, the API resolves it from the tax authority's own table and says so — official and computed values are never confused:

| `method` | `derived` | Meaning |
| --- | --- | --- |
| `published` | `false` | The tax authority printed this pair directly |
| `inverse` | `true` | Computed as 1 ÷ the published opposite direction |
| `cross` | `true` | Computed via NOK from two published rates |

## 🛡️ Error handling

Errors are thrown as `Error` with `status` (HTTP code) and `body` (the API's JSON error) attached:

```js
try {
  const pair = await getRate('USD', 'XXX', { apiKey: 'art_live_...' });
} catch (err) {
  console.log(err.message); // human-readable reason
  console.log(err.status);  // e.g. 404
}
```

| Status | Meaning |
| ------ | ------- |
| — | Missing `apiKey` (thrown before any request) |
| `400` | Malformed date or parameters |
| `401` | Invalid API key |
| `403` | Endpoint needs a [paid plan](https://allratestoday.com/pricing/) (historical dates & series) |
| `404` | Pair or date range not covered by Norwegian Customs (Tolletaten) |
| `429` | Monthly quota exceeded |

## 🔷 TypeScript

Full definitions ship with the package — no `@types` install:

```ts
import type { LatestRates, PairRate, DatedRates, RateEntry, HistoryQuery, RequestOptions } from 'tolletaten-exchange-rate';
```

## 📦 CommonJS

```javascript
const { getRate } = require('tolletaten-exchange-rate');

getRate('USD', 'NOK', { apiKey: 'art_live_...' }).then((pair) => console.log(pair.rate));
```

## 💡 Quota tips

- Rates change about once a fortnight — cache the official table locally and a small monthly quota goes a long way.
- Every request counts toward your AllRatesToday quota, shared across all AllRatesToday endpoints on your key.

## 📖 Methods reference

| Method | Plan | Description |
| ------ | ---- | ----------- |
| `getRate(source, target, { apiKey })` | Free | Latest rate for one pair, resolved from the official table |
| `getLatestRates({ apiKey })` | Free | The tax authority's full latest official table |
| `getRatesForDate(date, { apiKey, source?, target? })` | Paid | The official table (or one pair) for a YYYY-MM-DD date |
| `getHistory({ symbol \| source+target, from?, to? }, { apiKey })` | Paid | Daily series since 2021 |

## 📥 Bulk data (no key)

Need the whole archive rather than an API call? The same official tables are mirrored daily as open data:

- Hugging Face: [AllRatesToday/central-bank-exchange-rates](https://huggingface.co/datasets/AllRatesToday/central-bank-exchange-rates) — one CSV per institution (`rates/tolletaten.csv`)
- Kaggle: [allratestoday/central-bank-exchange-rates](https://www.kaggle.com/datasets/allratestoday/central-bank-exchange-rates)
- Raw JSON on GitHub: `https://raw.githubusercontent.com/AllRates-Today/central-bank-exchange-rates/main/data/tolletaten/latest.json`

## 🔗 Links

- **Website:** [allratestoday.com](https://allratestoday.com)
- [Norwegian Customs (Tolletaten) rates page](https://allratestoday.com/tax-authority-rates-api/tolletaten/) — live table, publication cadence, FAQ
- [All tax authority sources](https://allratestoday.com/tax-authority-rates-api/) · [Full list of 120+ central banks and 50+ tax authorities](https://allratestoday.com/central-bank-rates-api/institutions/) — one API, the same response shape for every source
- [Download central bank rates](https://allratestoday.com/download-central-bank-rates/) — every bank's latest table and history as Excel, CSV or JSON
- [Bank Exchange Rate API](https://allratestoday.com/bank-exchange-rate-api/) — live buy and sell rates from 1,200+ commercial banks in 120+ countries · [npm](https://www.npmjs.com/package/bank-exchange-rates) · [GitHub](https://github.com/AllRates-Today/bank-exchange-rates)
- [Package docs on the site](https://allratestoday.com/docs/sdk/tolletaten-exchange-rate/) · [ERP integration guides](https://allratestoday.com/docs/integrations/)
- [API documentation](https://allratestoday.com/docs/#central-bank) · [Interactive reference](https://allratestoday.com/api-reference/) · [Methodology](https://allratestoday.com/official-rates-methodology/)
- [Register (Free)](https://allratestoday.com/register) · [Dashboard](https://allratestoday.com/profile) · [Pricing](https://allratestoday.com/pricing/)
- [Status](https://allratestoday.com/status)
- [Postman collection](https://allratestoday.com/postman/)
- [ChatGPT app](https://chatgpt.com/plugins/plugin_asdk_app_6ae1e76098f48191a285ac3f5ab7a83b) — ask ChatGPT for live and official central bank rates
- [OpenAPI reference on Bump.sh](https://bump.sh/allratestoday/doc/allratestoday-api) — also on [SwaggerHub](https://app.swaggerhub.com/apis-docs/allratestoday/allratestoday-exchange-rate-central-bank-rates-api/2.2.0)
- [GitHub](https://github.com/AllRates-Today/tolletaten-exchange-rate)

## 📜 License

MIT
