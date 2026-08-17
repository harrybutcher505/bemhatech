# Bemhatech Content Facts

**Purpose:** Single source of truth for every claim that appears in more than one place.  
Before finishing any edit that touches one of these facts, grep the repo for the old wording.

**Last reviewed:** 2026-08-04

---

## 1. Product version

| Fact | Current value |
|------|--------------|
| App version | **1.4.11** (last published GitHub release) |
| Version string on website | `v1.3.97` |
| Mac download filename | `Composed-mac.zip` (no version in filename — uses `releases/latest`) |
| Windows download filename | `Composed_1.4.11_x64-setup.exe` |
| `latest.json` endpoint | `https://bemhatech.nl/composed/latest.json` |

**Appears in:** `composed/index.html` (hero badge, two download cards), `composed/privacy.html` (meta line — must be updated manually), Windows filename.  
**Grep pattern when updating:** `v1\.3\.[0-9]`  
**Note:** App code is at 1.3.97 locally but 1.3.93 is the last published GitHub release. Website shows the published release version. Update website only when a CI build publishes a new release.

---

## 2. Pricing

| Tier | Price | Payment |
|------|-------|---------|
| Free | €0 — no card needed | — |
| Composed Pro | **€49 one-time** | Paddle (`pri_01kwcazth81t1s1vs0wv5yyxge`) |

- No subscription, ever.
- Returning-user discount available by email.
- Paddle issues proper EU VAT invoices.

**Appears in:** `composed/index.html` (hero, pricing section, social proof strip), language pages if they include pricing.  
**Grep pattern when updating:** `€49`

---

## 3. Product maturity label

| Label | Used where |
|-------|-----------|
| **"Early Access"** | `composed/index.html` hero badge, nav download button |
| **"commercial beta"** | `composed/privacy.html` product description section |

These two labels are intentionally different in register (marketing vs legal). Do not merge them, but keep both accurate. If the product exits beta, update both.

**Grep pattern:** `Early Access\|commercial beta`

---

## 4. Data flow — the two-path model

This is the claim that went stale before. Both paths must be described consistently everywhere.

### Own API key path
> Requests go directly from the user's machine to the Anthropic Claude API. Bemhatech receives nothing — not the CV text, not the API key.

### Pilot code path
> Requests are routed through `proxy.bemhatech.nl`, a server operated by Bemhatech in Amsterdam, Netherlands (TransIP VPS, hosted by TransIP B.V.). The proxy validates the pilot code credit allowance and forwards the request to the Anthropic API. CV text passes through the proxy **in transit only** — it is not stored there beyond the duration of the request. Only aggregate token counts are recorded for credit-cap enforcement.

**Appears in:** `composed/index.html` (download section disclaimer, step 3 install note), `composed/privacy.html` (sections 1, 4, 5), `composed/terms.html` (section 4), `composed/support.html` (highlight box, "What is sent externally" section).  
**Grep patterns:** `never uploaded`, `never held`, `proxy\.bemhatech\.nl`, `in transit`, `not stored`

---

## 5. Local storage claims

> CV, cover letters, job data, and application history are stored as files on the user's own machine (`job-apply-profile.json` and related files on the Desktop). They are not uploaded to Bemhatech as files.  
> The licence key and pilot code are also stored locally and are never sent to Bemhatech (pilot code is sent to the proxy per-request, but is not persisted on the server).

**Appears in:** `composed/index.html` (trust badges in pricing section), `composed/privacy.html` (section 2), `composed/terms.html`, `composed/support.html`.  
**Grep patterns:** `data stay`, `stored locally`, `your machine`, `never held on our server`

---

## 6. Platform support

| Platform | Supported | Notes |
|----------|-----------|-------|
| Mac | ✓ | macOS 12+, Apple Silicon & Intel |
| Windows | ✓ | Windows 10+, 64-bit |
| iOS / Android | ✗ | Not currently supported |
| Browser / PWA | ✗ | Not currently supported (D9 prototype not shipped) |

**Appears in:** `composed/index.html` (hero, download cards, download disclaimer), `composed/privacy.html`, `composed/support.html`.  
**Grep pattern:** `iOS`, `Android`, `browser`, `PWA`, `macOS 12`, `Windows 10`

---

## 7. Supported markets

Current list as of 2026-08-04: **Netherlands, UK, UAE** (and others via market selector).  
Localisation built in v1.3.91 — confirm exact market list once E3 (market selection) is finalised.

**Appears in:** `composed/index.html` (features grid "Multiple markets" card).  
**Grep pattern:** `market\|Netherlands\|United Kingdom\|UAE`

---

## 8. Employer / prior-employer claims

Claims about Harry's professional history appear on the Harry Butcher profile pages and in the language-specific pages. These are **prior-employer claims** — subject to Action Plan workstream B (B2, B3, Gate 5).

| Employer name | Appears in | Consent status |
|---------------|-----------|----------------|
| Geotab | `ar/`, `nl/`, `fr/`, `profile/` | **Not confirmed** — B3 outstanding |
| Telogis / Verizon Connect | `ar/`, `nl/`, `fr/`, `profile/` | **Not confirmed** — B3 outstanding |
| Astrata (formerly Qualcomm) | `ar/`, `nl/`, `fr/`, `profile/` | **Not confirmed** — B3 outstanding |
| Aramex | possibly `profile/` | **Not confirmed** |
| Majid Al Futtaim | possibly `profile/` | **Not confirmed** |

**Action required (B2):** Rename all references to prior-employer content as "Founder's Prior Professional Experience" across website and profile.  
**Action required (B3):** Seek permission from each employer before using their name in external materials.  
**Grep pattern:** `Geotab\|Telogis\|Verizon Connect\|Astrata\|Aramex\|Majid`

---

## 9. Features removed or not yet live

| Feature | Status | Note |
|---------|--------|------|
| Veterans / military mode | **REMOVED** from website (2026-08-04) | Was in features grid — removed in this session |
| Android / PWA client | **Not started** | D9 proxy is live; client not built |
| African market localisation | **Built, caveat** | v1.3.91; confirm which market once E3 selects |

---

## 10. Third-party services disclosed

| Service | Role | Disclosed in privacy.html |
|---------|------|--------------------------|
| Anthropic | AI inference | ✓ |
| Paddle | Payment processing | ✓ |
| proxy.bemhatech.nl (TransIP VPS) | Pilot code proxy / credit enforcement | ✓ (added 2026-08-04) |
| Hunter.io | Contact finder (in-app) | **NOT YET** — D5 outstanding |
| GitHub Pages / Netlify | Website hosting / analytics | **NOT YET** — D5 outstanding |

---

## How to use this file

1. **Before editing any claim in the list above** — read the current-truth entry here first.
2. **After editing** — grep the repo for the old wording to find every copy. Common patterns are listed per section above.
3. **When a fact changes** — update this file in the same commit that changes the content. The two must move together.
4. **Language pages** — currently do not include the two-path data-flow description. If they add any data-handling claims, add them here.
