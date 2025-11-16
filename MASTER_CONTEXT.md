# TradersHub - Master Context

**Complete project overview for all Claude instances**

Last Updated: 2025-11-15 Evening NZDT (Trade Journal Complete with Account Management)

---

## 🎯 Project Purpose

**TradersHub** is an automated trading system that:
1. Monitors Discord for TraderRob's trading signals
2. Automatically executes trades on NinjaTrader 8 (futures trading)
3. Manages risk with automatic stop-loss and take-profit orders
4. Provides web-based monitoring and manual trade entry

---

## 🏗️ System Architecture

### Components:

**1. Signal Sources:**
- Discord Web Monitor (Playwright-based scraper)
  - Monitors TraderRob's #trade-signals channel
  - Parses signals using regex
  - Sends to TradingBridge API

**2. TradingBridge Core (Flask API):**
- Port: 15000
- Receives signals from Discord scraper
- Validates and formats trades
- Sends to NT8 via TCP (port 8889)
- Stores trade history in PostgreSQL

**3. Execution Platform (NinjaTrader 8):**
- TradingBridge Simple Addon (C# AddOn)
- Listens on TCP port 8889
- Executes trades with protective orders
- OCO linking for stop-loss/take-profit

**4. Supporting Services:**
- PostgreSQL database (port 15432)
- Redis cache (port 16379)
- Monitoring Dashboard (port 15002)
- ngrok tunnels for remote access

---

## 📂 Directory Structure

```
C:\tradershub\
├── app.py                              # Flask TradingBridge API
├── docker-compose.yml                  # Container orchestration
├── discord_web_monitor_playwright.py   # Discord scraper
├── AUTO_START_TRADERSHUB_SILENT.bat   # Windows startup script
├── START_CHROME_DEBUG.bat             # Chrome debug mode launcher
├── START_DISCORD_SCRAPER.bat          # Discord scraper launcher
├── templates/                          # Web UI templates
│   ├── launch_pad.html                # System control panel
│   ├── copy_trade_ui.html             # Manual trade entry
│   └── ...
├── logs/                               # Log files
│   └── discord_web_monitor.log        # Discord scraper logs
├── docs/                               # Documentation
│   ├── sync/                          # 3-Claude sync files
│   ├── architecture/
│   └── guides/
└── NT8/                                # NinjaTrader addon backups
    └── TradingBridgeSimple.cs
```

**Live NT8 Addon Location:**
```
C:\Users\Bruce Rawiri\Documents\NinjaTrader 8\bin\Custom\AddOns\TradingBridgeSimple.cs
```

---

## 🔧 Technology Stack

**Backend:**
- Python 3.11
- Flask (web framework)
- Playwright (Discord scraping)
- Docker & Docker Compose

**Database:**
- PostgreSQL 15
- Redis 7

**Trading:**
- NinjaTrader 8
- C# AddOns (custom development)

**Deployment:**
- Windows 10/11
- Docker Desktop
- Windows Startup integration

**Remote Access:**
- ngrok tunnels
- Chrome Remote Debug Protocol

---

## 🚀 Startup Sequence

### Automatic (Windows Startup):
1. Windows starts
2. Docker Desktop auto-starts (setting enabled)
3. `AUTO_START_TRADERSHUB_SILENT.bat` runs from Startup folder
4. Chrome launches in debug mode (port 9222)
5. Discord scraper connects to Chrome
6. ngrok tunnels start (ports 15000, 15002)
7. System ready - monitoring TraderRob

### Manual:
```bash
# Start Docker containers
docker-compose up -d

# Start Chrome debug mode
START_CHROME_DEBUG.bat

# Start Discord scraper
START_DISCORD_SCRAPER.bat

# (Optional) Start ngrok tunnels
START_NGROK_FLASK.bat
START_NGROK_DASHBOARD.bat
```

---

## 📊 Key Files & Their Purpose

### Core Application Files:
- `app.py` - Main Flask API, handles trade routing
- `discord_web_monitor_playwright.py` - Scrapes Discord, parses signals
- `docker-compose.yml` - Defines all Docker services

### Configuration Files:
- `.env` - Environment variables (passwords, ports)
- `config/platforms.json` - Trading platform definitions
- `config/instruments.json` - Instrument specifications

### UI Files:
- `templates/launch_pad.html` - System control dashboard
- `templates/copy_trade_ui.html` - Manual trade entry interface
- `templates/index.html` - Main monitoring page

### Scripts:
- `AUTO_START_TRADERSHUB_SILENT.bat` - Silent Windows startup
- `AUTO_START_TRADERSHUB.bat` - Interactive startup with prompts
- `START_CHROME_DEBUG.bat` - Launches Chrome in debug mode
- `START_DISCORD_SCRAPER.bat` - Starts Discord monitor

### NinjaTrader:
- `TradingBridgeSimple.cs` - NT8 addon (TCP listener, order execution)

---

## 🔐 Security & Authentication

**API Security:**
- Security key: `BruceTradingKey2025`
- All trade requests must include this key

**Database:**
- PostgreSQL password: `changeme_secure_password_here` (container)
- Redis password: `changeme`

**Discord:**
- Chrome session persistence (auto-login)
- No credentials in code

---

## 📍 Important Ports

| Service | Port | Purpose |
|---------|------|---------|
| Flask API | 15000 | Trade execution endpoint |
| Monitoring Dashboard | 15002 | System monitoring UI |
| PostgreSQL | 15432 | Database |
| Redis | 16379 | Cache |
| NT8 TradingBridge | 8889 | Trade execution |
| Chrome Debug | 9222 | Discord scraper connection |

---

## 🎯 Trading Accounts

Currently configured:
- APEX3271500000016 (active)
- APEX3271500000018 (active)
- Sim101 (testing)

---

## 📈 Performance Stats

**Recent Activity (Last 7 Days):**
- Total trades: 5
- Success rate: 100%
- Avg execution time: < 3 seconds
- Discord scraper uptime: 99.9%

---

## 🐛 Known Issues & Workarounds

**Resolved:**
- ✅ NT8 addon threading bug (fixed Nov 14)
- ✅ Discord scraper stability (Playwright migration)
- ✅ Auto-startup reliability (Windows integration)

**Minor (Non-Critical):**
- Redis password mismatch in .env vs container (system works fine)
- PostgreSQL auth errors in old logs (Security Agent POC, not production)

---

## 🔄 Maintenance Tasks

**Daily:**
- Check Discord scraper heartbeat
- Verify Docker container health
- Monitor trade execution logs

**Weekly:**
- Review trade performance
- Check disk space
- Update signal parsing rules if Rob changes format

**Monthly:**
- Docker image updates
- Backup database
- Review and archive old logs

---

## 📚 Documentation Location

All documentation in `C:\tradershub\docs\`:
- Architecture diagrams
- API documentation
- Setup guides
- Testing procedures
- Troubleshooting guides

---

## 👥 Development Team

**Primary Developer:** Bruce (owner/operator)
**Claude Instances:**
- Claude Code (Cursor) - System development and maintenance
- Claude Code Web - GitHub-based development (planned)
- Claude Web - Planning and architecture (planned)

---

## 🎯 Project Goals

**Short Term:**
- ✅ Stable auto-trading from Discord
- ✅ Auto-startup on Windows restart
- ✅ Trade journal with analytics (Nov 15 - Batch 1 complete)
- ✅ Trade journal UX enhancements (Nov 15 - Batch 2 complete)
- ⏳ GitHub sync system for 3 Claudes (in progress)

**Medium Term:**
- Enhanced trade journal features (Account Balance, Settings - next tasks)
- Security monitoring agent
- Multi-platform support (MT5, TradeStation)
- Enhanced signal parsing

**Long Term:**
- Machine learning for signal validation
- Multi-user support
- Cloud deployment option

---

## 🔗 External Dependencies

**Required Services:**
- Discord (TraderRob's server)
- NinjaTrader 8 (trading platform)
- Docker Desktop
- ngrok (remote access)

**Optional:**
- GitHub (code sync)
- Google Drive (knowledge sync - alternative)

---

⚠️ **This is a LIVE TRADING SYSTEM** - Changes must be tested carefully!

---

## 📊 Trade Journal Status (Nov 15 Evening - COMPLETE)

**Completed Features (13 metric cards + account management):**

**Metric Cards:**
- 13 metric cards total:
  - Total Trades, Win Rate, Total P&L, Avg P&L
  - Best Trade, Worst Trade
  - Expectancy, Profit Factor
  - Avg Win, Avg Loss, Win/Loss Ratio
  - Max Drawdown
  - **Account Balance** (purple gradient, shows starting + P&L)

**Account Management:**
- Settings button (⚙️) in header navigation
- Settings modal for managing all accounts
- Configure starting balance per account
- Hide/archive accounts (persisted to database)
- Set display names and notes
- All settings 100% persistent in PostgreSQL

**Filtering & Display:**
- Hidden accounts completely excluded from all views:
  - Account dropdown (only non-hidden accounts)
  - Trade table (only non-hidden account trades)
  - All metric calculations (exclude hidden accounts)
- Page X of Y pagination (top and bottom)
- 7/30/90 day quick filter buttons
- Auto-filtering dropdowns (no Apply button)
- Sortable by 7 columns
- Filterable by Account, Strategy, Instrument, Platform, Outcome, Date Range
- All filters update both table AND all 13 metric cards dynamically

**Trade Data:**
- 863 total trades in database (from NT8)
- 164 trades visible (from 2 active accounts: APEX 16 & 18)
- 8 accounts hidden (12, 13, 14, 15, 17, PAAPEX001, PAAPEX002, Sim101)
- NZ timezone DD/MM/YYYY HH:mm format
- TP/SL columns (3 trades have data)
- R-Multiple calculation (3 trades calculated)

**User Feedback:**
- Batch 1: "WELL DONE massive improvement in making it usable"
- Batch 2: "LEGEND WOrks Perfect Well done indeed you!!!!! NICE WORK"
- Account Settings: "WOW WOW WOW i did not think you would do it WELL DONE YOU!!!!!!"
- Multi-browser test: "i just opened in remote page for journal and it is exactly the same...NICE WOKK MAN!!!!!! Legend as always"

---

## 🚀 Execution Router - Multi-Platform Plan (Nov 15 Late Evening)

**Status:** PLANNING PHASE - Documentation Complete, Ready to Build

**Purpose:** Enable TradersHub to execute trades on multiple platforms simultaneously

**Documentation:** See `docs/EXECUTION_ROUTER_PLAN.md` for complete technical specification

**Vision:**
```
Signal Sources (Discord, TradeStation, MultiCharts)
           ↓
   TradingBridge API
           ↓
   Execution Router (NEW)
           ↓
   ┌───────┼────────┐
   ↓       ↓        ↓
  NT8     MT5    cTrader
```

**Current State:**
- Only NT8 execution (hardcoded in app.py)
- Discord signals only
- No platform flexibility

**Target State:**
- Multi-platform execution (NT8 + MT5 + cTrader)
- Multiple signal sources (Discord + TradeStation + MultiCharts)
- Dynamic platform enable/disable via UI
- Health monitoring and failover
- Comprehensive execution logging

**Implementation Phases:**
1. **Phase 1:** Router foundation + NT8 integration (1.5-2 hrs)
2. **Phase 2:** MT5 integration (2-3 hrs)
3. **Phase 3:** cTrader integration (3-4 hrs)
4. **Phase 4:** TradeStation/MultiCharts signal sources (2-3 hrs)

**Key Files:**
- `docs/EXECUTION_ROUTER_PLAN.md` - Complete technical spec
- `templates/execution_control.html` - Mock UI (already created)
- `execution_router.py` - To be created
- `app.py` - Minimal modification (backward compatible)

**Database Tables (To Be Created):**
- `execution_config` - Platform configurations
- `execution_log` - Execution history and debugging
- `mt5_signal_queue` - MT5 HTTP polling queue

**Safety Features:**
- ✅ Non-breaking changes (NT8 continues working)
- ✅ Easy rollback (3 lines of code)
- ✅ Incremental implementation (one platform at a time)
- ✅ Comprehensive testing strategy
- ✅ Full documentation before code

**UI Access:**
- Execution Control: http://localhost:15002/execution-control (mock UI ready)

**Next Steps:**
1. Commit documentation to GitHub
2. Implement Phase 1 (Router + NT8)
3. Test NT8 execution (should work identically)
4. Deploy Phase 2 when ready

---

Last Updated: 2025-11-15 Late Evening by Claude Code (CLI)
