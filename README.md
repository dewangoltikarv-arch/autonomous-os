# 🤖 Autonomous OS - SOTA Personal AI Agent

> **The greatest open-source autonomous personal OS.** Hermes-based, free LLM fallbacks (DeepSeek primary), Telegram integration, auto-tool installer, skill orchestration, self-improving. Zero-dollar operation.

## Features

✅ **Hermes Core** — Self-improving agent with closed learning loop, skill creation, memory  
✅ **Multi-LLM Stack** — DeepSeek (primary) → Groq → Mistral → OpenRouter → Gemini (free fallbacks)  
✅ **Telegram Integration** — Full remote control from your phone  
✅ **Auto-Tool Installer** — Chat: "Install Docker" → Agent does it  
✅ **Skill Orchestration** — 180+ community skills + plugins integrated  
✅ **Self-Improving** — Creates skills from experience, optimizes workflows  
✅ **Persistent Memory** — Long-term context, user profiles, procedural memory  
✅ **Zero-Cost** — Completely free (DeepSeek API only)  
✅ **Plug-and-Play** — Download → Add API keys → Run

## Quick Start

### Prerequisites

- macOS (M1/M2/M3+) or Linux
- Python 3.11+
- Node.js 18+
- Git

### Installation

```bash
# Clone the repo
git clone https://github.com/dewangoltikarv-arch/autonomous-os.git
cd autonomous-os

# Run installer
bash scripts/install.sh

# Configure
cp .env.example .env
# Edit .env with your API keys (see below)

# Start
bash scripts/start.sh
```

### API Keys Required (All Free)

1. **DeepSeek** (primary LLM)
   - Get free key: https://platform.deepseek.com
   - Free tier: $5 monthly credit (plenty for testing)

2. **Groq** (fallback LLM)
   - Get free key: https://console.groq.com
   - Free: 30 requests/minute

3. **OpenRouter** (optional, multi-model access)
   - Get free key: https://openrouter.ai
   - Free: $5 monthly credit

4. **Telegram Bot** (optional, for remote control)
   - Create bot: https://t.me/BotFather
   - Get: Bot token + Your Telegram user ID

5. **Gemini** (optional, fallback vision)
   - Get free key: https://makersuite.google.com/app/apikey
   - Free: Generous quota

```bash
# .env template
DEEPSEEK_API_KEY=your_deepseek_key
GROQ_API_KEY=your_groq_key
OPENROUTER_API_KEY=your_openrouter_key
GEMINI_API_KEY=your_gemini_key

TELEGRAM_BOT_TOKEN=your_telegram_bot_token
TELEGRAM_USER_ID=your_user_id

# Optional: Firecrawl for web search (free tier available)
FIRECRAWL_API_KEY=optional

# Hermes config
HERMES_HOME=$HOME/.hermes
MODEL_PROVIDER=deepseek
MODEL_NAME=deepseek-chat
```

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│           Autonomous OS (Hermes Core)                    │
├─────────────────────────────────────────────────────────┤
│                                                           │
│  ┌─────────────────────────────────────────────────┐    │
│  │ Multi-LLM Router                                 │    │
│  │ DeepSeek → Groq → Mistral → OpenRouter → Gemini│    │
│  └─────────────────────────────────────────────────┘    │
│                      ↓                                    │
│  ┌─────────────────────────────────────────────────┐    │
│  │ Hermes Agent Engine                             │    │
│  │ • Skill creation & learning                     │    │
│  │ • Persistent memory (hindsight, honcho)         │    │
│  │ • Tool calling & delegation                     │    │
│  │ • Cron scheduling                               │    │
│  └─────────────────────────────────────────────────┘    │
│                      ↓                                    │
│  ┌──────────────────┬──────────────────────────────┐    │
│  │ Skill            │ Tool Orchestration           │    │
│  │ Orchestration    │ • Auto-installer             │    │
│  │ (180+ skills)    │ • Package detection          │    │
│  │                  │ • Environment setup          │    │
│  └──────────────────┴──────────────────────────────┘    │
│                      ↓                                    │
│  ┌─────────────────────────────────────────────────┐    │
│  │ Gateway Layer (Multi-Platform)                  │    │
│  │ • Telegram bot (remote control)                 │    │
│  │ • CLI interface (local terminal)                │    │
│  │ • API server (programmatic access)              │    │
│  └─────────────────────────────────────────────────┘    │
│                                                           │
└─────────────────────────────────────────────────────────┘
```

## Usage

### Telegram Remote Control

```
@your_bot_name: Install Docker and verify it

→ Agent detects you need Docker
→ Checks if installed
→ Downloads & installs if missing
→ Runs `docker --version`
→ Sends result back to Telegram
```

### Auto-Tool Installer

When Hermes needs a tool to complete a task:

1. **Detection** — Agent checks if tool is installed
2. **Decision** — Asks permission (if configured) or auto-installs
3. **Installation** — Uses system package manager (brew, apt, etc.)
4. **Verification** — Confirms installation and availability
5. **Integration** — Adds tool to available skills

### Skill Orchestration

Access 180+ pre-built skills:

```
/skills                    # Browse available skills
/wondelai/skills          # Load production skill suite
/hermes-life-os           # Load personal OS skills
/hermes-dojo              # Load self-improvement skills
```

## Integrations

### Messaging Platforms

- **Telegram** — Full remote control (built-in)
- **Discord** — Via Hermes gateway
- **Slack** — Via Hermes gateway
- **WhatsApp** — Via Hermes gateway
- **Signal** — Via Hermes gateway

### Memory Providers

- **Built-in** — SQLite-based persistent memory
- **Hindsight** — Long-term memory layer (optional)
- **Honcho** — Stateful memory with user modeling (optional)
- **mem0** — Universal memory layer (optional)

### LLM Providers

| Provider | Free Tier | Speed | Quality | Fallback |
|----------|-----------|-------|---------|----------|
| DeepSeek | $5/month | Fast | Excellent | Primary |
| Groq | 30req/min | Fastest | Good | 1st |
| Mistral | Free API | Fast | Good | 2nd |
| OpenRouter | $5/month | Best | Good | 3rd |
| Gemini | Generous | Medium | Good | 4th |

## Configuration

### Primary LLM (DeepSeek)

```bash
hermes config set provider deepseek
hermes config set model deepseek-chat
hermes config set api_key $DEEPSEEK_API_KEY
```

### Fallback Chain

Automatically routes to next provider if current fails:

```
DeepSeek unavailable? → Try Groq
Groq unavailable? → Try Mistral
Mistral unavailable? → Try OpenRouter
OpenRouter unavailable? → Try Gemini
```

### Telegram Setup

```bash
# Configure Telegram gateway
hermes gateway setup
# Choose: Telegram
# Paste bot token when prompted
# Send a message to your bot
```

## Common Commands

```bash
# Start agent in CLI mode
hermes

# Start Telegram gateway
hermes gateway start

# Run a skill
/wondelai/skills load
/hermes-dojo activate

# Check available tools
hermes tools

# View memory
hermes memory show

# Install a tool via agent
# Chat: "Install node-fetch npm package"
```

## Cost Breakdown (Monthly)

| Service | Free Tier | Cost |
|---------|-----------|------|
| DeepSeek | $5 credit/month | $0 |
| Groq | 30 req/min | $0 |
| Mistral | Free API | $0 |
| OpenRouter | $5 credit/month | $0 |
| Gemini | Generous quota | $0 |
| **Total** | | **$0** |

All free tier combined gives you **millions of tokens per month**.

## Roadmap

- [x] Phase 1: Core Hermes + Multi-LLM router + Telegram + Auto-tool installer + Skill orchestration
- [ ] Phase 2: MacBook full control + Voice interface + Computer automation
- [ ] Phase 3: Advanced memory (vector + knowledge graph) + Self-evolution + Deployment hardening

## Project Structure

```
autonomous-os/
├── README.md
├── .env.example
├── pyproject.toml              # Python dependencies
├── package.json                # Node dependencies
│
├── scripts/
│   ├── install.sh              # One-command installer
│   ├── start.sh                # Launch script
│   ├── config-telegram.sh       # Telegram setup wizard
│   └── test.sh                 # Smoke tests
│
├── src/
│   ├── core/
│   │   ├── hermes_wrapper.py    # Hermes integration
│   │   ├── llm_router.py        # Multi-LLM provider routing
│   │   └── skill_loader.py      # Skill orchestration
│   │
│   ├── tools/
│   │   ├── auto_installer.py    # Package detection & installation
│   │   ├── package_manager.py   # Brew/apt/pacman abstraction
│   │   └── tool_registry.py     # Available tools database
│   │
│   ├── integrations/
│   │   ├── telegram_gateway.py   # Telegram bot
│   │   ├── cli_interface.py      # CLI mode
│   │   └── api_server.py         # REST API
│   │
│   └── config/
│       ├── providers.yaml        # LLM provider config
│       ├── skills.yaml           # Skills registry
│       └── fallback_chain.yaml    # LLM fallback rules
│
├── skills/
│   ├── auto-installer/          # Auto-tool installer skill
│   ├── system-monitor/          # System health
│   └── workflow-orchestration/   # Multi-task coordination
│
└── docker/
    ├── Dockerfile               # Container image
    └── docker-compose.yml       # Multi-service setup
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT — Free to use, modify, and distribute.

## Support

- 📚 [Hermes Docs](https://hermes-agent.nousresearch.com/docs/)
- 💬 [Discord](https://discord.gg/NousResearch)
- 🐛 [Issues](https://github.com/dewangoltikarv-arch/autonomous-os/issues)

---

**Built on Hermes Agent by Nous Research. Combined with best-in-class free LLM APIs.**

*The future of personal AI is autonomous, free, and open.*
