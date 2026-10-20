# 📋 GitHub Profile README — Full Project History

**Project:** Professional GitHub Profile README for Aymane Bozian  
**GitHub:** [github.com/BozIAymane](https://github.com/BozIAymane)  
**Date:** 2026-10-20  

---

## 🔍 Phase 1 — Research & Inspection

### What we did:
1. **Inspected the workspace** → Empty directory at `c:\Users\LENOVO\Desktop\EST_K\my_git`
2. **Verified GitHub username** → `BozIAymane` confirmed (user ID: 239175087)
3. **GitHub bio found:** "BozIA – AI & Big Data Projects by Aymane Bozian" — 6 repositories
4. **Inspected all 5 featured repos** to get accurate descriptions:

| Repository | Actual Description (from og:description) |
|-----------|------------------------------------------|
| [Analyse-Bitcoin-BTC-MAD](https://github.com/BozIAymane/Analyse-Bitcoin-BTC-MAD) | Analyse technique et financière du Bitcoin en Dirham Marocain (2019-2025) - Stratégies de trading, tests statistiques et backtesting |
| [crypto-realtime-analytics](https://github.com/BozIAymane/crypto-realtime-analytics) | Real-Time Crypto Analytics & Anomaly Detection using Kafka, Spark Structured Streaming, ML (Isolation Forest), PostgreSQL & Grafana |
| [chatbot-whatsapp-nvs](https://github.com/BozIAymane/chatbot-whatsapp-nvs) | AI-powered WhatsApp chatbot for Moroccan e-commerce using RAG architecture. Supports Darija, French and English. Built with Flask, ChromaDB, Groq (Llama 4) and Infobip API. PFE 2026. |
| [Projet_IoT_Cassandra](https://github.com/BozIAymane/Projet_IoT_Cassandra) | Real-time IoT Wind Turbine Monitoring — Big Data architecture for ingestion, processing, and visualization. Stack: Python, Cassandra, Grafana, Docker |
| [wildfire-tracker](https://github.com/BozIAymane/wildfire-tracker) | Real-time Wildfire Tracking Project |

5. **Researched reference repos:**
   - [lowlighter/metrics](https://github.com/lowlighter/metrics) → For GitHub Actions metrics SVG
   - [Platane/snk](https://github.com/Platane/snk) → For contribution snake animation
   - [capsule-render](https://github.com/kyechan99/capsule-render) → For waving header/footer
   - [readme-typing-svg](https://github.com/DenverCoder1/readme-typing-svg) → For typing animation

---

## 🏗️ Phase 2 — Initial Build

### Files created (first version):

| File | Description |
|------|-------------|
| `README.md` | Full profile README with custom SVG header/footer |
| `assets/header.svg` | Custom animated SVG (dark navy, particles, neural network lines) |
| `assets/footer.svg` | Custom animated SVG footer |
| `.github/workflows/metrics.yml` | lowlighter/metrics workflow |
| `.github/workflows/snake.yml` | Platane/snk contribution snake workflow |
| `SETUP.md` | Step-by-step deployment guide |
| `assets/README.md` | Assets directory documentation |

### Initial metrics.yml plugins:
- ✅ Languages (indepth)
- ✅ Isometric calendar (half-year)
- ❌ Achievements → **caused error later**
- ❌ Activity → **caused error later**
- ✅ Lines of code

---

## 🚀 Phase 3 — Automated Deployment

### Steps executed automatically:

```
1. git init                                          ✅
2. git config user.name "Aymane Bozian"              ✅
3. git config user.email "aymanebozian@gmail.com"    ✅
4. git add -A                                        ✅ (7 files)
5. git commit                                        ✅ (commit c0c7dbd)
6. git branch -M main                                ✅
7. gh auth status                                    ✅ Logged in as BozIAymane
   Token type: OAuth (gho_****)
   Scopes: gist, read:org, repo, workflow
8. gh repo create BozIAymane --public                ✅ Created
9. git remote add origin                             ✅
10. git push -u origin main                          ✅
11. gh secret set METRICS_TOKEN                      ✅ (used gh auth token)
12. gh workflow run "Metrics"                        ✅ Success (1m12s)
13. gh workflow run "Contribution Snake"             ✅ Success (13s)
14. git pull origin main                             ✅ (got github-metrics.svg)
```

---

## 🐛 Phase 4 — Error Fix

### Problem:
The metrics SVG showed **"Unexpected error"** on two plugins:
- ❌ **Recent activity** → `GraphqlResponseError`
- ❌ **Achievements** → `GraphqlResponseError`

### Root cause:
The `METRICS_TOKEN` was set using `gh auth token` which returns an **OAuth token** (`gho_****`).
This OAuth token does NOT support the GraphQL queries required by the achievements and activity plugins.
Those plugins need a **classic Personal Access Token** (`ghp_****`).

### Proof from logs:
```
x-accepted-oauth-scopes: repo
x-oauth-scopes: gist, read:org, repo, workflow
instance: GraphqlResponseError: Request failed due to following response errors
message: 'Unexpected error'
```

### Fix applied:
Removed `plugin_achievements` and `plugin_activity` from `metrics.yml`.
Replaced with `plugin_notable` and `plugin_stars`.

```diff
- plugin_achievements: yes
- plugin_achievements_display: compact
- plugin_achievements_threshold: C
- plugin_activity: yes
- plugin_activity_days: 14
- plugin_activity_filter: all
- plugin_activity_limit: 5
- plugin_activity_load: 300
- plugin_activity_visibility: public
+ plugin_notable: yes
+ plugin_stars: yes
+ plugin_stars_limit: 3
```

### Result: Commit `f86d0e7` → Workflow re-run → **Success, no errors** ✅

---

## 🎨 Phase 5 — Visual Redesign

### User feedback:
- Header/footer looked AI-generated, not professional
- Broken animated emoji icons before section titles
- Redis missing from databases

### Changes made:

| Before | After |
|--------|-------|
| Custom `assets/header.svg` | **capsule-render** waving gradient |
| Custom `assets/footer.svg` | **capsule-render** waving footer |
| No typing animation | **readme-typing-svg** with Fira Code |
| Animated Fluent Emoji icons (broken) | Standard Unicode emojis |
| `flat-square` tech badges | `for-the-badge` style (larger) |
| Table layout for tech stack | Clean section layout |
| No Redis | **Redis added** in Databases |

### Key URLs used:

**Header:**
```
https://capsule-render.vercel.app/api?type=waving&color=0:0a0e27,50:0d47a1,100:00d4ff&height=220&section=header&text=Aymane%20Bozian&fontSize=50&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=AI%20%26%20Big%20Data%20Developer&descSize=18&descColor=8892b0&descAlignY=55
```

**Typing SVG:**
```
https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=22&duration=3000&pause=1000&color=00D4FF&center=true&vCenter=true&multiline=true&width=600&height=80&lines=Data+Engineering+%7C+Machine+Learning+%7C+Big+Data;Building+Real-Time+Streaming+%26+RAG+Applications
```

**Footer:**
```
https://capsule-render.vercel.app/api?type=waving&color=0:00d4ff,50:0d47a1,100:0a0e27&height=120&section=footer
```

### Commit: `39af5fd` — pushed and live ✅

---

## 📁 Final File Structure

```
BozIAymane/BozIAymane (GitHub repo)
├── README.md                          ← Profile README (v3 — redesigned)
├── SETUP.md                           ← Deployment guide
├── HISTORY.md                         ← This file
├── github-metrics.svg                 ← Auto-generated by metrics workflow
├── assets/
│   ├── README.md
│   ├── header.svg                     ← Old header (no longer referenced)
│   └── footer.svg                     ← Old footer (no longer referenced)
├── .github/
│   └── workflows/
│       ├── metrics.yml                ← lowlighter/metrics (daily)
│       └── snake.yml                  ← Platane/snk (every 12h)
└── [output branch]
    ├── github-snake.svg               ← Light mode snake
    └── github-snake-dark.svg          ← Dark mode snake
```

---

## ⚙️ Current Workflow Configuration

### metrics.yml (v2 — fixed)
```yaml
Schedule: daily at 00:00 UTC + manual dispatch
Action: lowlighter/metrics@latest
Plugins:
  - Languages (indepth, 8 max, custom cyan colors)
  - Isometric calendar (half-year)
  - Lines of code
  - Notable contributions
  - Stars (limit 3)
Output: github-metrics.svg
Timezone: Africa/Casablanca
```

### snake.yml
```yaml
Schedule: every 12 hours + manual dispatch
Action: Platane/snk/svg-only@v3
Output: dist/github-snake.svg + dist/github-snake-dark.svg
Push to: output branch via peaceiris/actions-gh-pages@v3
```

---

## 🔑 Secrets & Permissions

| Secret | Value Source | Status |
|--------|------------|--------|
| `METRICS_TOKEN` | `gh auth token` (OAuth `gho_****`) | ✅ Set |
| `GITHUB_TOKEN` | Auto-provided by GitHub Actions | ✅ Auto |

| Permission | Setting |
|-----------|---------|
| Workflow permissions | Read and write ✅ |

---

## 🎯 Git Commit History

```
39af5fd  redesign: capsule-render header/footer, typing SVG, add Redis, fix section icons
80a2543  [metrics] Update github-metrics.svg (automated, 2nd run — no errors)
f86d0e7  fix: remove achievements and activity plugins (incompatible with OAuth token)
64901cf  [metrics] Update github-metrics.svg (automated, 1st run — had errors)
c0c7dbd  feat: add professional GitHub profile README with metrics and snake workflows
```

---

## ✅ What's Complete

- [x] Profile repository created (`BozIAymane/BozIAymane`)
- [x] README.md with capsule-render header/footer
- [x] Typing SVG animation
- [x] Social badges (GitHub, LinkedIn, Email)
- [x] About Me section
- [x] Tech stack with Redis, all badges working
- [x] Featured projects (5 repos, accurate descriptions)
- [x] GitHub stats cards (Stats + Languages + Streak)
- [x] lowlighter/metrics SVG (auto-generated daily)
- [x] Contribution snake animation (auto-generated every 12h)
- [x] Both workflows tested and passing
- [x] SETUP.md documentation
- [x] All errors fixed

---

## 🔮 What You Can Do Next

### Quick improvements:
1. **Create a classic PAT** (`ghp_****`) at [github.com/settings/tokens](https://github.com/settings/tokens) with `repo` + `read:user` scopes, then update the `METRICS_TOKEN` secret → unlocks achievements and activity plugins
2. **Clean up old files:** Delete `assets/header.svg` and `assets/footer.svg` (no longer used)
3. **Pin repos:** Go to your profile and pin the 5 featured repos

### Adding new projects:
```html
<td width="50%" valign="top">
  <h3 align="center">Project Name</h3>
  <p align="center">
    <a href="https://github.com/BozIAymane/repo-name">
      <img src="https://img.shields.io/badge/View_Repository-0d1117?style=for-the-badge&logo=github&logoColor=white"/>
    </a>
  </p>
  <p>Description here.</p>
  <p>
    <img src="https://img.shields.io/badge/Tech-Color?style=flat-square&logo=tech&logoColor=white"/>
  </p>
</td>
```

### Changing colors:
- Header gradient: `color=0:HEX1,50:HEX2,100:HEX3` in capsule-render URL
- Stats cards: `bg_color`, `title_color`, `border_color` params
- Typing SVG: `color=HEX` param

### Badge format:
```
https://img.shields.io/badge/NAME-HEXCOLOR?style=for-the-badge&logo=LOGO_NAME&logoColor=white
```
Find logo names at: [simpleicons.org](https://simpleicons.org)

---

## 📍 Useful Links

| Resource | URL |
|----------|-----|
| Profile page | https://github.com/BozIAymane |
| Profile repo | https://github.com/BozIAymane/BozIAymane |
| Actions tab | https://github.com/BozIAymane/BozIAymane/actions |
| Repo secrets | https://github.com/BozIAymane/BozIAymane/settings/secrets/actions |
| Create PAT | https://github.com/settings/tokens |
| capsule-render | https://github.com/kyechan99/capsule-render |
| readme-typing-svg | https://github.com/DenverCoder1/readme-typing-svg |
| lowlighter/metrics | https://github.com/lowlighter/metrics |
| Platane/snk | https://github.com/Platane/snk |
| Simple Icons | https://simpleicons.org |
| Shields.io | https://shields.io |
| skillicons.dev | https://skillicons.dev |
