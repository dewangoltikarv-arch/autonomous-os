# HANDOFF PACKAGE - Autonomous OS Phase 1

## What Was Done ✅

### 1. Repository Setup
- Created public repo: `dewangoltikarv-arch/autonomous-os`
- Initialized with MIT license
- Added comprehensive README with architecture, features, and quick start

### 2. Architecture Defined
- **Multi-LLM Stack**: DeepSeek (primary) → Groq → Mistral → OpenRouter → Gemini
- **Hermes Integration**: Self-improving agent with skill creation
- **Telegram Gateway**: Remote control from phone
- **Auto-Tool Installer**: Chat-driven package management
- **Skill Orchestration**: 180+ community skills integration
- **Persistent Memory**: Long-term context storage

### 3. Documentation Complete
- Full setup instructions
- API key requirements (all free)
- Architecture diagrams
- Usage examples
- Cost breakdown (zero-cost)
- Project structure
- Roadmap

---

## What Needs to Be Done (Phase 1 Remaining)

### CRITICAL FILES TO CREATE:

#### 1. **Core Python Implementation** (`src/core/`)
- `llm_router.py` - Multi-provider LLM routing with fallback chain
- `hermes_wrapper.py` - Hermes agent integration
- `skill_loader.py` - Skill registry and loader

#### 2. **Tools & Installation** (`src/tools/`)
- `auto_installer.py` - Detect tools needed, install via package manager
- `package_manager.py` - Abstraction for brew/apt/pacman/other
- `tool_registry.py` - Database of available tools

#### 3. **Integrations** (`src/integrations/`)
- `telegram_gateway.py` - Telegram bot with full command support
- `cli_interface.py` - Terminal interface
- `api_server.py` - REST API wrapper (optional)

#### 4. **Configuration Files**
- `.env.example` - API keys template
- `pyproject.toml` - Python dependencies
- `package.json` - Node.js dependencies (for some tools)
- `providers.yaml` - LLM provider configuration
- `skills.yaml` - Skills registry
- `fallback_chain.yaml` - LLM fallback rules

#### 5. **Installation & Startup Scripts** (`scripts/`)
- `install.sh` - One-command installer
  - Install Hermes
  - Install Python 3.11+
  - Install Node.js
  - Set up venv
  - Install dependencies
  - Configure .env
  
- `start.sh` - Launch script
  - Load .env
  - Start Hermes core
  - Initialize LLM router
  - Load skills
  - Start Telegram gateway (optional)
  
- `config-telegram.sh` - Telegram setup wizard
- `test.sh` - Smoke tests

#### 6. **Skills** (`skills/`)
- `auto-installer/` - Core auto-install skill
- `system-monitor/` - System health checks
- `workflow-orchestration/` - Multi-task coordination

#### 7. **Docker Support** (`docker/`)
- `Dockerfile` - Container image
- `docker-compose.yml` - Multi-service setup

---

## Technical Specifications

### Multi-LLM Router Logic
```
1. Try DeepSeek API
2. If timeout/error → Try Groq
3. If Groq fails → Try Mistral (via OpenRouter)
4. If Mistral fails → Try OpenRouter directly
5. If OpenRouter fails → Try Gemini
6. If all fail → Return error with fallback suggestion

Each call: timeout=30s, retry=2x before failover
```

### Auto-Tool Installer Flow
```
1. User: "Install Docker"
2. Agent queries tool_registry.py
3. Detects macOS + brew available
4. Runs: brew install docker
5. Verifies: docker --version
6. Returns result to user
7. Adds to available skills
```

### Telegram Gateway
```
1. Poll Telegram API for new messages
2. Parse command (e.g., "/install Docker")
3. Pass to Hermes agent
4. Execute tool orchestration
5. Send result back to Telegram
6. Support multi-user sessions
```

### Skill Orchestration
```
1. Load ecosystem skills from:
   - wondelai/skills
   - hermes-life-os
   - hermes-dojo
   - community skills
2. Register with Hermes
3. Make available via /skill command
4. Auto-load on startup
```

---

## File Structure Template

```
autonomous-os/
├── README.md ✅
├── HANDOFF.md (THIS FILE)
├── .env.example 📝 TODO
├── pyproject.toml 📝 TODO
├── package.json 📝 TODO
│
├── scripts/
│   ├── install.sh 📝 TODO
│   ├── start.sh 📝 TODO
│   ├── config-telegram.sh 📝 TODO
│   └── test.sh 📝 TODO
│
├── src/
│   ├── __init__.py
│   ├── core/
│   │   ├── __init__.py
│   │   ├── llm_router.py 📝 TODO
│   │   ├── hermes_wrapper.py 📝 TODO
│   │   └── skill_loader.py 📝 TODO
│   │
│   ├── tools/
│   │   ├── __init__.py
│   │   ├── auto_installer.py 📝 TODO
│   │   ├── package_manager.py 📝 TODO
│   │   └── tool_registry.py 📝 TODO
│   │
│   ├── integrations/
│   │   ├── __init__.py
│   │   ├── telegram_gateway.py 📝 TODO
│   │   ├── cli_interface.py 📝 TODO
│   │   └── api_server.py 📝 TODO
│   │
│   └── config/ (YAML config loaders)
│       ├── __init__.py
│       ├── config.py 📝 TODO
│       └── validators.py 📝 TODO
│
├── config/
│   ├── providers.yaml 📝 TODO
│   ├── skills.yaml 📝 TODO
│   └── fallback_chain.yaml 📝 TODO
│
├── skills/
│   ├── auto-installer/ 📝 TODO
│   ├── system-monitor/ 📝 TODO
│   └── workflow-orchestration/ 📝 TODO
│
├── docker/
│   ├── Dockerfile 📝 TODO
│   └── docker-compose.yml 📝 TODO
│
├── tests/
│   ├── test_llm_router.py 📝 TODO
│   ├── test_auto_installer.py 📝 TODO
│   └── test_telegram_gateway.py 📝 TODO
│
└── docs/
    ├── API.md 📝 TODO
    ├── ARCHITECTURE.md 📝 TODO
    └── DEPLOYMENT.md 📝 TODO
```

---

## Handoff Instructions for Codex

### 1. **Access the Repository**
```bash
git clone https://github.com/dewangoltikarv-arch/autonomous-os.git
cd autonomous-os
cat HANDOFF.md  # This file
```

### 2. **Priority Order (Complete in this sequence)**

#### Priority 1 (Critical Path):
1. `pyproject.toml` - Define dependencies
2. `.env.example` - API key template
3. `src/core/llm_router.py` - Multi-LLM routing
4. `src/core/hermes_wrapper.py` - Hermes integration
5. `scripts/install.sh` - One-command setup

#### Priority 2 (Core Features):
6. `src/tools/auto_installer.py` - Package detection
7. `src/tools/package_manager.py` - Package manager abstraction
8. `src/tools/tool_registry.py` - Tools database
9. `src/integrations/telegram_gateway.py` - Telegram bot
10. `scripts/start.sh` - Startup script

#### Priority 3 (Polish):
11. `src/core/skill_loader.py` - Skill orchestration
12. `config/providers.yaml` - Provider config
13. `config/skills.yaml` - Skills registry
14. `scripts/config-telegram.sh` - Setup wizard
15. Docker files (optional for Phase 1)

### 3. **Key Dependencies to Include**

```
Core:
- hermes-agent (latest from pip)
- python-dotenv
- pyyaml
- requests

LLM Providers:
- openai (for API compatibility)
- groq
- anthropic (for fallbacks)

Telegram:
- python-telegram-bot

Tools:
- setuptools
- wheel
- click (CLI)

Utilities:
- pydantic (validation)
- loguru (logging)
- tenacity (retries)
```

### 4. **Critical Implementation Notes**

#### LLM Router
- Must support streaming responses
- Fallback on timeout (30s) not just errors
- Track provider health/availability
- Log all API calls for debugging

#### Auto-Installer
- Detect system: macOS → brew, Linux → apt/pacman
- Check if tool already installed before installing
- Verify installation post-install
- Support both CLI tools and Python packages (pip)

#### Telegram Gateway
- Support multiple users (per-user session state)
- Commands: `/install`, `/skills`, `/run`, `/status`, `/help`
- Long-polling (no webhooks for simplicity)
- Error messages back to Telegram

#### Hermes Integration
- Use official Hermes Python SDK
- Load skills from ecosystem
- Persist memory between sessions
- Support for Hermes cron jobs

### 5. **Testing Requirements**

Each component should have:
- Unit tests
- Integration tests with mocks
- Smoke tests (scripts/test.sh)

Test checklist:
- [ ] LLM router failover works
- [ ] Auto-installer detects and installs tools
- [ ] Telegram gateway receives and sends messages
- [ ] Hermes loads and executes skills
- [ ] Skills appear in `/skills` command

### 6. **Environment Setup Pattern**

```python
# Example pattern for all modules
import os
from dotenv import load_dotenv

load_dotenv()

DEEPSEEK_API_KEY = os.getenv("DEEPSEEK_API_KEY")
GROQ_API_KEY = os.getenv("GROQ_API_KEY")
# ... etc

if not DEEPSEEK_API_KEY:
    raise ValueError("DEEPSEEK_API_KEY not set in .env")
```

### 7. **Error Handling Pattern**

```python
# All modules should use this pattern
try:
    result = call_llm()
except TimeoutError:
    logger.warning("Primary LLM timeout, trying fallback")
    result = call_fallback_llm()
except Exception as e:
    logger.error(f"All LLMs failed: {e}")
    raise
```

### 8. **Questions Codex Will Need Answered**

Q: Should auto-installer ask for confirmation before installing?
A: Yes, configurable via `.env` (AUTO_INSTALL_CONFIRM=true/false)

Q: Should Telegram sessions persist across restarts?
A: Yes, save session state to local SQLite database

Q: Should skills auto-load or require activation?
A: Auto-load core skills, optional skills require `/skill load <name>`

Q: What's the default LLM model?
A: `deepseek-chat` for DeepSeek API

Q: Should Hermes gateway run automatically?
A: Yes, `scripts/start.sh` should start it in background

---

## Commit Messages Pattern

```
feat: add multi-LLM router with fallback chain
feat: implement Telegram gateway
fix: handle auto-installer edge cases
docs: add API documentation
test: add LLM router integration tests
```

---

## Success Criteria for Phase 1 Completion

- [ ] User can run `bash scripts/install.sh` on macOS M2
- [ ] After setup, `hermes` CLI works
- [ ] Telegram bot responds to `/help` command
- [ ] Chat: "Install brew" → Agent installs if missing
- [ ] Skills from wondelai/skills load successfully
- [ ] LLM router fails over to Groq if DeepSeek unavailable
- [ ] All free API keys work (no paid tier required)
- [ ] Memory persists across sessions
- [ ] Zero errors in logs on happy path

---

## Repo Status

- **Repository**: https://github.com/dewangoltikarv-arch/autonomous-os
- **Visibility**: Public ✅
- **Branch**: main
- **Commits**: 2 (init + README)
- **Ready for**: Codex handoff

---

## Next Steps

1. Codex clones repo
2. Follows Priority 1 order
3. Creates PRs for each component
4. Tests each integration
5. Pushes to main
6. Phase 1 complete → Ready for Phase 2

---

**Handoff prepared by: Copilot**
**Date: 2026-09-12**
**For: Codex**
