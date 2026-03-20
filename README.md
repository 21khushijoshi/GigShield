# GigShield - AI-Powered Parametric Income Insurance for India's Delivery Partners

**Protecting the last mile, one week at a time.**

GigShield is an AI-enabled parametric insurance platform that safeguards **food delivery partners** (Zomato / Swiggy) against income loss caused by uncontrollable external disruptions like, extreme weather, flooding, severe pollution, and sudden civic events like curfews or zone lockdowns. When the world stops, their income shouldn't.

---

## 📌 Table of Contents

1. [The Problem](#the-problem)
2. [Persona & Scenarios](#persona--scenarios)
3. [Application Workflow](#application-workflow)
4. [Weekly Premium Model](#weekly-premium-model)
5. [Parametric Triggers](#parametric-triggers)
6. [Platform Choice: Web vs Mobile](#platform-choice-web-vs-mobile)
7. [AI/ML Integration](#aiml-integration)
8. [Tech Stack](#tech-stack)
9. [Development Plan](#development-plan)
10. [Exclusions & Compliance](#exclusions--compliance)
11. [Minimal Viable Scope (Phase 1)](#minimal-viable-scope-phase-1)

---

## The Problem

India's food delivery ecosystem runs on hundreds of thousands of gig workers who earn ₹15,000–₹25,000/month on average. Their income is entirely event-driven, no rides, no pay. When disruptions hit:

- A single day of heavy rain can wipe out ₹600-₹1,000 in earnings
- AQI spikes above 400 reduce outdoor rider hours by 40-60%
- A local curfew or bandh can zero out an entire day's income

There is **no financial safety net** today. Banks won't lend. Platforms don't compensate. Family savings erode. GigShield changes that.

---

## Persona & Scenarios

**Chosen Segment:** Food Delivery Partners - Zomato & Swiggy riders in Tier-1 and Tier-2 Indian cities.

**Why this segment?**
- Largest and most active gig workforce category in India (~5 million active riders)
- Extremely weather-sensitive - rain, heat, and pollution directly halt deliveries
- Strong smartphone penetration with existing app familiarity
- Weekly payout culture already established by platforms

### Persona Profiles

| Persona | Profile | Avg Weekly Earnings | Key Risk |
|---|---|---|---|
| **Ravi, 28** | Full-time Swiggy rider, Bengaluru | ₹4,500 | Monsoon flooding, zone shutdowns |
| **Meena, 34** | Part-time Zomato rider, Chennai | ₹2,200 | Extreme heat (45°C+), cyclone alerts |
| **Arjun, 22** | New joiner, Pune | ₹3,000 | AQI pollution days, local bandh |

### Disruption Scenarios

**Scenario 1 - Heavy Rainfall (Bengaluru, July)**
> Ravi's city experiences IMD Red Alert rainfall. Deliveries drop 70% for 2 days. GigShield's weather API detects ≥ 60mm/day rainfall in Ravi's active zone. Payout of ₹800 (2-day income estimate) is automatically triggered and credited to his UPI within 4 hours, no claim form required.

**Scenario 2 - AQI Pollution Spike (Delhi, November)**
> Arjun's city crosses AQI 400 (Severe+). Government advisories recommend no outdoor activity. GigShield detects this via real-time AQI API. Arjun's policy auto-triggers a 1-day partial payout of ₹350, proportional to expected earnings.

**Scenario 3 - Civic Bandh / Curfew (Chennai, January)**
> A sudden state bandh is declared. Meena's delivery zone is locked. GigShield's civic event monitor (scraping government notifications + news API) flags the disruption. A full-day payout is processed automatically.

**Scenario 4 - Extreme Heat (Rajasthan, May)**
> Temperature crosses 46°C - above GigShield's heat threshold. Meena cannot safely ride. A heat-day payout is triggered, covering 60% of her average daily earning for up to 2 days per week.

---

## Application Workflow

```
┌─────────────────────────────────────────────────────────┐
│                    GIGSHIELD WORKFLOW                   │
└─────────────────────────────────────────────────────────┘

  [1. ONBOARDING]
   ↓
  Rider registers via mobile-web app
  → Aadhaar-based KYC (DigiLocker API)
  → Platform linkage: Zomato/Swiggy rider ID verified
  → AI Risk Profiler runs (city, zone, activity history)
  → Personalised weekly premium quote generated
  ↓

  [2. POLICY ACTIVATION]
   ↓
  Rider selects weekly coverage tier (Basic / Standard / Pro)
  → Weekly premium deducted via UPI AutoPay or wallet
  → Policy activates Monday 00:00 IST
  → Coverage zones registered (rider's active delivery zones)
  ↓

  [3. REAL-TIME DISRUPTION MONITORING]
   ↓
  GigShield's Event Engine polls every 15 minutes:
  → IMD Weather API (rainfall, temperature, cyclone alerts)
  → CPCB AQI API (Air Quality Index by city)
  → Civic Event Monitor (news API + government bulletin scraper)
  → Platform Activity Feed (Swiggy/Zomato mock API - delivery volume drop signals)
  ↓

  [4. PARAMETRIC TRIGGER EVALUATION]
   ↓
  When a trigger threshold is crossed in a rider's zone:
  → System validates: Is rider's policy active? Is it within coverage period?
  → AI Fraud Guard runs: Is activity pattern consistent? Location match?
  → If valid: Payout amount computed (daily average × disruption multiplier)
  ↓

  [5. AUTOMATIC PAYOUT]
   ↓
  Payout initiated without rider filing a claim
  → Credited to registered UPI ID within 2-4 hours
  → Rider receives push notification with payout summary
  → Payout capped at 2 days' equivalent per disruption event
  ↓

  [6. DASHBOARD & ANALYTICS]
   ↓
  Rider Dashboard: earnings protected, payouts received, active coverage
  Admin Dashboard: disruption events, payout volumes, fraud flags, loss ratios
```

---

## Weekly Premium Model

GigShield's pricing is **weekly** to match the payout rhythm of Zomato/Swiggy riders.

### Premium Tiers

| Tier | Weekly Premium | Max Weekly Payout | Coverage |
|---|---|---|---|
| **Basic** | ₹29 | ₹500 | Rain + AQI only |
| **Standard** | ₹49 | ₹900 | Rain + AQI + Heat + Bandh |
| **Pro** | ₹79 | ₹1,500 | All triggers + extended 3-day coverage |

> **Design rationale:** ₹29–79/week is 1-2% of average weekly earnings, affordable, and positioned as a "safety coffee" expense.

### Dynamic Premium Calculation

The base weekly premium is adjusted by the AI Risk Engine using:

```
Final Premium = Base Tier Premium × City Risk Multiplier × Zone Risk Score × Historical Disruption Index
```

**Factors used:**
- **City Risk Multiplier** - cities with higher historical disruption frequency (e.g., Mumbai monsoon, Delhi pollution) have higher multipliers (1.0x-1.4x)
- **Zone Risk Score** - hyperlocal risk score per delivery zone (flood-prone areas, heat corridors)
- **Historical Disruption Index** - rolling 52-week average of payable disruption days in that geography
- **Rider Activity Pattern** - riders who are consistently active on disruption days (and thus lose more) get marginally higher premiums, fairly priced

Premiums are **recalculated every 4 weeks** using updated rolling data. Riders are notified 3 days before renewal with the new rate and can opt out.

---

## Parametric Triggers

Parametric insurance pays out automatically when a **measurable external condition** crosses a defined threshold, no claim form, no adjuster, no wait.

### GigShield Trigger Matrix

| Disruption Type | Trigger Condition | Data Source | Payout Level |
|---|---|---|---|
| **Heavy Rain** | ≥ 60mm rainfall in 24hr in rider's city/zone | IMD Weather API | 100% of daily average |
| **Extreme Heat** | ≥ 44°C for 2+ consecutive hours between 10AM–5PM | OpenWeatherMap API | 60% of daily average |
| **Severe AQI** | AQI ≥ 400 (Severe+) for ≥ 4 hours | CPCB AQI API | 75% of daily average |
| **Cyclone / Flood Alert** | IMD Red/Orange Alert issued for rider's district | IMD API + NDMA feed | 100% of daily average |
| **Civic Bandh / Curfew** | Official government notification OR 80%+ delivery volume drop in zone | News API + Platform mock API | 100% of daily average |

**Payout Caps:**
- Maximum 2 disruption days per week per policy
- Maximum 1 payout per disruption event per rider
- Consecutive disruptions (e.g., 3-day flood): treated as one event, capped at 2-day payout

**Daily Average Calculation:**
Each rider's "daily average earnings" is computed from their platform activity data - last 30 days' average, excluding Sundays and platform-declared holidays.

---

## Platform Choice: Web vs Mobile

**Decision: Progressive Web App (PWA) - Mobile-first Web**

### Rationale

| Criterion | Native App | PWA (Our Choice) |
|---|---|---|
| Install friction | High (App Store / Play Store review) | Low (browser bookmark or install prompt) |
| Rider familiarity | Moderate | High - riders already use mobile browsers |
| Development speed | Slow (2 codebases: iOS + Android) | Fast (single codebase) |
| Offline support | Strong | Good (Service Workers) |
| Distribution | Gated | Instant - shareable via WhatsApp link |
| Low-end device support | App size can be heavy | Lightweight, works on 2GB RAM devices |

**Key insight:** Delivery partners predominantly use low-to-mid-range Android phones. They share WhatsApp links and distrust downloading unknown APKs. A PWA delivered via a WhatsApp link from their platform (Swiggy/Zomato) partnership is the **lowest-friction onboarding path**.

The PWA supports:
- Home screen installation on Android
- Push notifications for payout alerts
- Offline-capable policy viewing via Service Workers
- Lightweight (target < 200KB initial load)

---

## AI/ML Integration

### 1. Risk Profiling & Premium Calculation

**Model:** Gradient Boosted Trees (XGBoost) trained on historical disruption and earnings data

**Inputs:**
- Rider's city and active delivery zones
- Historical disruption frequency in those zones (IMD historical data)
- Rider's average active hours per day/week
- Platform tier (Swiggy Gold / Zomato Pro vs standard)
- Seasonal risk index (monsoon season = higher risk weight)

**Output:** Personalised weekly premium and risk tier assignment

**In Phase 1:** Rule-based heuristic proxy (city × season × zone tier) until sufficient training data is available

### 2. Fraud Detection

**Threat model:**
- Riders falsely claiming they were working during a disruption (when they actually stayed home due to a different reason)
- Duplicate accounts claiming the same event
- Collusion between riders in a zone to inflate platform-drop signals

**Detection mechanisms:**

| Signal | Method |
|---|---|
| GPS location during disruption | Platform API mock - was rider's last-known location in an affected zone? |
| Activity pattern anomaly | ML anomaly detector: is this rider's claim behavior statistically consistent with peers in same zone? |
| Duplicate claim detection | Hash-based dedup on (rider ID, event ID, date) |
| Velocity check | No more than 2 payouts per week per rider; flag if > 80% of weeks have payouts (suspicious) |
| Social graph clustering | Flag riders who all onboarded together and all claim simultaneously (potential ring fraud) |

**Model:** Isolation Forest for anomaly detection on claim patterns; rule-based hard filters for deduplication

### 3. Disruption Event Validation

Before any payout is triggered, an AI event validator cross-references:
- Primary source (IMD / CPCB)
- Secondary source (news API sentiment around "rain", "flood", "bandh" in city)
- Platform delivery volume signal (mocked — sudden drop in orders in zone)

A payout requires **2 of 3 signals** to confirm the disruption. This prevents false triggers from API glitches.

### 4. Personalized Notifications

A lightweight NLP-based notification system sends riders contextual alerts in **Hindi or regional language** based on their registered state, using template-based generation with language localization.

---

## Tech Stack

### Frontend
- **React.js** (PWA with Vite)
- **Tailwind CSS** - mobile-first UI
- **Service Workers** - offline support
- **Push Notifications API**

### Backend
- **Node.js + Express** - REST API server
- **Python (FastAPI)** - AI/ML inference service (risk scoring, fraud detection)
- **PostgreSQL** - rider profiles, policies, payout records
- **Redis** - real-time event cache, disruption state management

### AI/ML
- **XGBoost** - risk profiling and premium calculation
- **scikit-learn (Isolation Forest)** - fraud/anomaly detection
- **Pandas + NumPy** - data pipelines

### External Integrations (Free Tier / Mocked)
- **OpenWeatherMap API** - temperature, rainfall data (free tier)
- **CPCB AQI API** - air quality index (open government API)
- **IMD Bulletins** - weather alert scraper (public data)
- **NewsAPI** - civic event detection
- **Razorpay (Sandbox)** - UPI AutoPay for premium collection and payout disbursement
- **DigiLocker API (Mock)** - Aadhaar-based KYC
- **Platform APIs (Mocked)** - Zomato/Swiggy rider ID verification and activity signals

### Infrastructure
- **Docker** - containerised services
- **GitHub Actions** - CI/CD
- **Render / Railway** - low-cost cloud deployment for demo

---

## Development Plan

### Phase 1 - MVP (Current Scope, 4 Weeks)

| Week | Deliverable |
|---|---|
| **Week 1** | Rider onboarding flow (KYC mock + zone selection), policy creation UI, weekly premium calculator (rule-based) |
| **Week 2** | Disruption monitoring engine (Weather + AQI APIs), parametric trigger logic, payout simulation |
| **Week 3** | Fraud detection (rule-based + Isolation Forest MVP), admin dashboard, analytics views |
| **Week 4** | End-to-end integration testing, PWA polish, demo video, README finalisation |

---

## Exclusions & Compliance

GigShield **strictly excludes** the following (by design and technical enforcement):

- Health insurance or hospitalisation cover
- Life insurance or accidental death benefits
- Vehicle repair or maintenance coverage
- Any coverage for personal negligence or voluntary non-working days
- Payouts for disruptions not corroborated by external data sources

These exclusions are enforced at the policy creation layer - the system will not generate a policy or process a payout for any excluded event type.

---

## Why GigShield Wins

| Dimension | Existing Options | GigShield |
|---|---|---|
| **Claim process** | Manual, 7-30 days | Zero-touch, 2-4 hours |
| **Pricing cycle** | Monthly / annual | Weekly - matches rider income |
| **Coverage relevance** | Generic health/life | Hyperlocal income disruption |
| **Accessibility** | App download, documentation | PWA via WhatsApp link |
| **Affordability** | ₹200-500/month | ₹29-79/week (₹120-320/month) |
| **AI integration** | None | Risk scoring, fraud detection, event validation |
