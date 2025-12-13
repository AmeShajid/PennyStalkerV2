# PennyStalker V1

**Research-First Penny Stock Discovery Engine**

---

## What PennyStalker Is

PennyStalker V1 is a **terminal-based research engine** designed to surface penny stocks **early** by detecting **real catalysts**, validating them with **official SEC filings**, flagging **dilution risk**, and producing a **ranked watchlist** with transparent reasoning.

**PennyStalker is NOT:**
- A price prediction tool
- A trading bot
- A recommendation engine
- Chart analysis software

**PennyStalker IS:**
- A discovery and filtering system
- A research automation engine
- A catalyst verification tool
- A dilution defense mechanism

---

## The Problem We're Solving

Penny stock traders fail because they:

- Find catalysts **after** the move starts
- Chase **promotional press releases** without verification
- Ignore **dilution risk** until it's too late
- Lack a **consistent research workflow**
- Drown in **noise** from dozens of daily "opportunities"

PennyStalker transforms research from manual guesswork into a **repeatable, defensive system** that finds legitimate opportunities early and filters out traps.

---

## How It Works

### The Pipeline

```
Collect → Parse → Classify → Score → Defend → Rank → Store → Output
```

### 1. Data Collection

PennyStalker pulls from three critical sources:

**News & Press Releases** (e.g., StockTitan)
- Identifies potential catalysts early
- Captures market-moving headlines
- Provides initial discovery candidates

**SEC Filings** (Edgar Database)
- Confirms legitimacy of press releases
- Detects dilution risk (S-1, 424B, ATM offerings)
- Tracks filing patterns over time

**Insider Activity** (e.g., OpenInsider)
- Provides supporting confidence signals
- Tracks meaningful buy/sell activity
- Never used as primary justification

### 2. Intelligent Analysis

**Catalyst Classification**
Every news event is categorized by strength:

- **Hard Catalysts** (30-40 pts): FDA approvals, acquisitions, government contracts with dollar amounts
- **Soft Catalysts** (15-29 pts): Partnerships, licensing deals, compliance milestones
- **Promotional/Weak** (0-14 pts): LOIs, vague corporate updates, buzzword PR

**SEC Confirmation**
Press releases are validated against official filings:
- PR + matching 8-K → Strong confidence bonus
- PR-only → Capped confidence tier
- Filing contradicts PR → Penalty

**Dilution Detection** (The Firewall)
Aggressive risk assessment using:
- High-risk filing types (S-1, S-3, 424B, ATM programs)
- Keyword escalation ("may offer and sell", "from time to time", "convertible notes")
- Historical dilution patterns (serial diluters get permanent penalties)

### 3. Transparent Scoring System

**0-100 Point Scale** with five components:

| Component | Max Impact | Purpose |
|-----------|-----------|----------|
| Catalyst Strength | +40 | Rewards legitimate, substantive catalysts |
| SEC Confirmation | +15 | Bonus for official filing support |
| Dilution Risk | -40 | **Heavy penalty** - cannot be offset |
| Insider Activity | ±10 | Small adjustment, never primary factor |
| Time Decay | -15 | Reduces stale signals automatically |

**Core Principle:** Dilution penalties dominate all other factors. No catalyst is strong enough to overcome active dilution risk.

### 4. Confidence Tier Mapping

Scores are translated into **actionable confidence levels**, not blind recommendations:

- **High Confidence**: Immediate manual review warranted
- **Medium Confidence**: Watch and verify independently
- **Low Confidence**: Research-only, proceed with caution
- **Filtered**: Ignore - fails minimum quality thresholds

**Mandatory Overrides:**
- Active dilution → Never High confidence
- PR-only catalyst → Capped at Low confidence
- Serial diluter history → Permanently capped at Medium

### 5. Persistent Storage

Every scan stores:
- News events with deduplication
- SEC filings with full text snippets
- Insider transactions
- Scores and rankings
- Run metadata

**Benefits:**
- Avoids repeat alerts on same headlines
- Tracks dilution patterns over time
- Enables future backtesting
- Powers website/API later (V2+)

### 6. Output

**Terminal Report:**
- Ranked candidates
- Score breakdown with reasoning
- Dilution risk flags
- Confidence tier
- Direct links to sources
- Clear disclaimers

**JSON Export:**
- Complete scan snapshot
- Structured data for analysis
- API-ready format

---

## Architecture Overview

PennyStalker follows **Single Responsibility Principle** with clean separation of concerns:

```
pennystalker/
├── core/           # Orchestration & configuration
├── sources/        # Data collectors (news, SEC, insiders)
├── analysis/       # Intelligence layer (classifier, detector, scorer)
├── storage/        # Database layer (SQLite + repositories)
└── reporting/      # Output layer (terminal, JSON)
```

### Key Design Principles

1. **Defense over optimism** - Conservative defaults, aggressive risk filtering
2. **Transparency over black-box** - Every score is explainable
3. **Research over prediction** - Finds opportunities, doesn't predict outcomes
4. **Fail-soft behavior** - Partial data is better than no output
5. **Modular architecture** - Easy to test, extend, and scale

---

## What PennyStalker Guarantees

### ✅ Will Do:
- Surface early catalyst opportunities
- Aggressively filter promotional noise
- Detect obvious dilution traps
- Rank candidates transparently
- Explain uncertainty clearly
- Operate reliably even with partial data

### ❌ Will NOT Do:
- Predict price movements
- Guarantee profitability
- Replace human judgment
- Automate trading decisions
- Eliminate market risk
- Provide financial advice

---

## Risk Awareness

PennyStalker is built with **defensive awareness** of real failure modes:

**Data-Level Risks:**
- Press releases can be manipulative
- SEC filings may be delayed or ambiguous
- Insider activity can be symbolic or misleading

**Market Risks:**
- Legitimate catalysts don't always move price
- Dilution can occur overnight without warning
- Liquidity can vanish during exits
- Trading halts happen without notice

**Tool Limitations:**
- Cannot see hidden dilution
- Misses non-press-release catalysts
- Scraping may break when sites change
- False positives and false negatives will exist

**User Psychology:**
- Research tools can create false confidence
- Discovery ≠ recommendation to buy
- Edge decays as tools become popular

PennyStalker is positioned as a **research assistant**, not a crystal ball.

---

## Technology Stack

**Language:** Python 3.9+

**Core Dependencies:**
- `requests` - HTTP client for data fetching
- `beautifulsoup4` - HTML parsing and extraction
- `sqlite3` - Embedded database (stdlib)
- Standard library: `re`, `json`, `datetime`, `logging`

**Architecture:**
- Object-oriented with SRP
- Repository pattern for data access
- Clean separation: collection → analysis → storage → output

**Future-Ready:**
- SQLite → PostgreSQL migration path
- Modular design for API layer (FastAPI)
- Testable components

---

## Development Philosophy

PennyStalker V1 is built like a **professional financial product**, not a disposable script:

- Comprehensive risk mitigation by design
- Defensive scoring that admits uncertainty
- Persistent memory for pattern recognition
- Graceful degradation when sources fail
- Clear boundaries between components
- Non-advisory positioning to avoid misuse

---

## Project Status

**Current Version:** V1 (Terminal MVP)

**Completed:**
- ✅ Complete architecture design
- ✅ Risk mitigation strategy
- ✅ Scoring system specification
- ✅ Dilution detection rules
- ✅ Data model definition

**In Progress:**
- Implementation of core modules

**Roadmap (V2+):**
- Web interface
- Real-time alerts
- Additional data sources
- Enhanced backtesting
- User customization

---

## License & Disclaimer

**For research and educational purposes only.**

PennyStalker does not provide investment advice, recommendations, or guidance on specific securities. All output is for informational purposes only. Users are solely responsible for their own investment decisions and due diligence.

Trading penny stocks involves substantial risk of loss. Past performance of catalysts does not guarantee future results.

---

## Philosophy

> "The hardest problem isn't finding stocks — it's excluding them."

PennyStalker exists to solve the signal-to-noise problem in penny stock research through systematic discovery, aggressive filtering, and transparent reasoning.

It's a tool that **augments judgment**, never replaces it.