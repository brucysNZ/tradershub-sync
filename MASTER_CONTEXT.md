# TradersHub - Master Context

**Complete project overview for all Claude instances**

Last Updated: 2025-11-14 18:15 NZDT

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
- ⏳ GitHub sync system for 3 Claudes

**Medium Term:**
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

Last Updated: 2025-11-14 by Claude Code (Cursor)
