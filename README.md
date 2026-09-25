<img width="1616" height="942" alt="image" src="https://github.com/user-attachments/assets/478bc478-0cd1-49ef-8fc8-e2ce5a7f406e" />

# BaFin AML/CFT & Cyber Fusion Dashboard
## Post-July 2026 Reorganization Edition

A unified SOC analyst frontend that fuses cyber and financial crime signals for German banks navigating BaFin's new Anti-Financial-Crime Division structure and 2026 enforcement priorities.

---

## Overview

Effective July 1, 2026, BaFin reorganized into a dedicated **Anti-Financial-Crime Division** with 30+ new positions, explicitly shifting resources toward AML/CTF and cyber risk supervision. German banks now face converged scrutiny where cyber incidents (account takeover, API abuse, BEC) often enable financial crime — yet SOC and AML teams historically operate in silos.

This dashboard breaks down those silos by correlating cyber alerts with transaction monitoring alerts in real time, detecting emerging attack-financial crime chains, and generating BaFin examination-ready case files.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     FUSION ENGINE LAYER                          │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────────────┐  │
│  │  SIEM Feed  │◄──►│ Correlation │◄──►│  Transaction Monitor│  │
│  │  (Cyber)    │    │   Engine    │    │  (AML/CTF)           │  │
│  └─────────────┘    └──────┬──────┘    └─────────────────────┘  │
│                             │                                    │
│                    ┌────────┴────────┐                          │
│                    │  Fusion Score   │  ML-based cross-domain    │
│                    │  Algorithm      │  risk scoring             │
│                    └────────┬────────┘                          │
│                             │                                    │
│  ┌──────────────────────────┼────────────────────────────────┐   │
│  │                          ▼         FRONTEND              │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐   │   │
│  │  │ Cyber Pane  │  │  AML Pane   │  │ Chain Visualizer│   │   │
│  │  │  (Left)     │  │  (Right)    │  │   (Center)      │   │   │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘   │   │
│  │                                                            │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐   │   │
│  │  │  Sanctions  │  │ Travel Rule │  │  Risk Heatmap   │   │   │
│  │  │   Overlay   │  │  Tracker    │  │                 │   │   │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘   │   │
│  │                                                            │   │
│  │  ┌─────────────────────────────────────────────────────┐  │   │
│  │  │      BaFin Examination Ready Case File Exporter       │  │   │
│  │  └─────────────────────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

---

## Features

### 1. Dual-Pane Alert Correlation View
- **Cyber Alerts Panel (Left)**: Phishing, credential stuffing, unusual login patterns, API abuse, TOR exit nodes, self-hosted wallet interactions
- **Transaction Monitoring Panel (Right)**: Rapid fund movements, structuring, cross-border wires, crypto conversions, terrorism financing typologies
- **Correlation Scoring**: ML-based fusion scores (0-100%) displayed on correlated alert pairs
- **Animated Indicators**: Pulsing red borders on fused cases; timeline mini-bars showing temporal proximity

### 2. Attack-Financial Crime Chain Visualizer
Visualizes the full kill chain from initial compromise to integration:

| Stage | Example | BaFin Relevance |
|-------|---------|-----------------|
| Initial Compromise | BEC phishing email to CFO | Cyber incident reporting (MaRisk) |
| Lateral Movement | Credential harvest via proxy phishing | IAM weakness → financial access |
| Privilege Escalation | Admin access to wire transfer system | Internal controls failure |
| Financial Crime | Fraudulent EUR 2.4M wire | AML transaction monitoring trigger |
| Layering | Split across 6 accounts in 3 jurisdictions | Structuring / sanctions evasion |
| Integration | CASP conversion to BTC via unhosted wallet | Travel Rule violation, self-hosted wallet |

### 3. Sanctions Screening Hit Overlay
- Real-time screening against EU Consolidated List, OFAC SDN, UN 1267
- Match confidence scoring (fuzzy logic + entity resolution)
- BaFin 2026 focus: Iran phantom trade, Rostec subsidiaries, Kazakhstan intermediaries
- Color-coded risk levels: Critical (red border), High (purple border), Medium (default)

### 4. Travel Rule Compliance Tracker
- Monitors CASP (Crypto-Asset Service Provider) transactions for Travel Rule data completeness
- Flags violations: missing originator data, unverified beneficiary, missing proof of ownership for self-hosted wallets
- Zero-threshold monitoring per German Travel Rule (applicable since December 2024)
- BaFin 2026 special examination focus area

### 5. Fusion Risk Heatmap
- 4x4 grid showing cross-domain correlation intensity by customer segment
- Segments: Corporate, Retail, Wealth, CASP, PSP, EMI, Fund, Insurer
- Color scale: Low (dark green) → Medium (green) → High (amber) → Critical (red)

### 6. BaFin Examination Ready Case File Exporter
Three export modes:

| Export | Contents | Format |
|--------|----------|--------|
| **Timeline** | Fused investigation chronology, correlation timestamps, chain of custody | PDF |
| **Evidence Package** | Raw alerts (JSON/STIX), transaction records, sanctions logs, Travel Rule proof, digital signatures/hashes | ZIP (JSON + PDF) |
| **Full Case File** | Complete narrative + visualization + analysis + recommended supervisory actions | PDF + XML/JSON |

All exports formatted for BaFin's new Anti-Financial-Crime Division special examination standards.

---

## BaFin 2026 Alignment

| BaFin Priority | Dashboard Feature | Data Source |
|----------------|-------------------|-------------|
| **Terrorism financing typologies** | Small-value donation alerts, adverse media screening, NGO risk flags | Transaction monitoring + open-source intelligence |
| **Sanctions evasion** | Phantom trade detection, Iran/Kazakhstan routing alerts, price manipulation flags | Trade finance + wire monitoring + sanctions lists |
| **CASP Travel Rule** | Real-time Travel Rule compliance tracking, missing data alerts | CASP API integrations |
| **Self-hosted wallets** | Enhanced due diligence triggers, proof-of-ownership verification | Blockchain analytics (Chainalysis/Elliptic) |
| **75+ special examinations** | One-click examination-ready case file generation | All fused data sources |

---

## Technology Stack

- **Frontend**: Vanilla HTML5 + CSS3 + JavaScript (no framework dependencies)
- **Styling**: CSS custom properties (dark mode SOC aesthetic)
- **Data**: Embedded demo data models (replaceable with API endpoints)
- **Responsive**: CSS Grid + Flexbox, mobile-first breakpoints at 1024px
- **Icons**: Unicode symbols (no external icon libraries)
- **Fonts**: System font stack + monospace for data fields

---

## File Structure

```
bafin_fusion_dashboard.html    # Single self-contained file
  ├── <head>
  │   ├── CSS variables (theme tokens)
  │   ├── Layout system (dashboard-container, grids, panels)
  │   ├── Component styles (alerts, chains, sanctions, travel, heatmap)
  │   └── Animations (pulse, borderPulse)
  ├── <body>
  │   ├── Header (BaFin badge, live clock, status pills)
  │   ├── Focus Banner (2026 priorities)
  │   ├── Stats Bar (5 KPI cards)
  │   ├── Dual-Pane Grid (Cyber + AML)
  │   ├── Chain Visualizer
  │   ├── Bottom Grid (Sanctions + Travel + Heatmap)
  │   └── Exporter Panel
  └── <script>
      ├── Data models (cyberAlerts, amlAlerts, sanctionsHits, travelRules, chainData)
      ├── Render functions (renderCyberAlerts, renderAMLAlerts, renderChain, etc.)
      ├── Filter handlers (filterCyber, filterAML)
      ├── Selection handler (selectAlert)
      └── Export handlers (exportTimeline, exportEvidence, exportFullCase)
```

---

## Usage

1. Open `bafin_fusion_dashboard.html` in any modern browser
2. Click alert filter buttons (All / Phishing / Credentials / API Abuse / Structuring / Cross-Border / Crypto) to narrow views
3. Click any alert card to select it for investigation
4. Correlated alerts show fusion scores and animated timeline dots
5. Scroll the chain visualizer to see the full attack-financial crime progression
6. Use export buttons to generate BaFin examination documentation

---

## Integration Notes

To connect to live systems, replace the embedded data arrays with API calls:

```javascript
// Replace this:
const cyberAlerts = [/* embedded data */];

// With this:
async function fetchCyberAlerts() {
  const res = await fetch('/api/v1/cyber-alerts?timeRange=24h');
  return await res.json();
}
```

Recommended backend integrations:
- **Cyber**: Splunk, QRadar, Sentinel, Chronicle
- **AML**: Actimize, FICO TONBELLER, SAS AML, Nice Actimize
- **Sanctions**: Dow Jones Risk & Compliance, Refinitiv World-Check, LexisNexis
- **Blockchain**: Chainalysis KYT, Elliptic Navigator, TRM Labs
- **Travel Rule**: Sygna Bridge, Notabene, TRISA

---

## Compliance

- **MaRisk (Minimum Requirements for Risk Management)**: Cyber incident reporting, IT risk management
- **GwG (Geldwäschegesetz)**: AML/CTF obligations, customer due diligence, transaction monitoring
- **MiCAR (Markets in Crypto-Assets Regulation)**: CASP licensing, Travel Rule implementation
- **BaFin Circulars**: 06/2023 (TFG), 03/2024 (Digitalization), 2026 special examination guidelines

---

## Architecture & Production Path

**Current implementation:** Zero-dependency, single-file vanilla JS (HTML/CSS/JS) —
deployable in restricted SOC environments with no build step or external dependencies.

**Production implementation path:** Where multi-user, real-time, or enterprise integration
requirements demand it, the production build is implemented in **React with D3.js/Chart.js**
for componentized state management, API-driven data layers, and role-based access —
migrating the current state-driven rendering pattern into a component architecture.

---

## License

Proprietary — developed for German financial institutions preparing for BaFin's 2026 Anti-Financial-Crime Division special examinations.

---

## Contact

For integration support or BaFin examination readiness consulting, contact your firm's AML/CFT and Cyber Risk functions.

---

*Built for the post-July 2026 BaFin reorganization. Breaking down SOC/AML silos before the next wave of special examinations.*
