# Advent of Agents - Daily Progress Notes

## About This Journey
- **Participant:** Beginner learning AI agent development
- **Repository:** Fork of Agent Starter Pack by eliasecchig
- **Google Cloud Project:** advent-of-agents
- **Account:** mark@measurecrew.co.nz

---

## Day 1 - December 3, 2025 ✅

### Setup & Environment Configuration

**What We Accomplished:**
1. ✅ Installed Python 3.13.9
2. ✅ Created and activated Python virtual environment (`.venv`)
3. ✅ Installed Agent Starter Pack CLI (v0.25.0)
4. ✅ Installed Google GenAI/ADK Python library
5. ✅ Installed Vertex AI SDK (google-cloud-aiplatform v1.129.0)
6. ✅ Installed Google Cloud CLI (gcloud v548.0.0)
7. ✅ Created Google Cloud Project: `advent-of-agents`
8. ✅ Configured gcloud authentication
9. ✅ Set up Application Default Credentials for Python

**Key Learnings:**
- **What is a CLI?** Command Line Interface - a tool to interact with software through text commands
- **What is gcloud?** Google Cloud's CLI that bridges your local computer with your cloud project
- **Why virtual environments?** Keeps project dependencies isolated and organized
- **Repository structure:** Understanding the nested folder issue and working in the correct directory

**Challenges Overcome:**
- Antivirus flagged `uv` installer as high-risk threat → Used alternative Python installation method
- Nested `a-s-p` folders → Clarified correct working directory
- gcloud not recognized after installation → Restarted VS Code to pick up PATH changes

**Tools Installed:**
```
Python: 3.13.9
Agent Starter Pack: 0.25.0
Google Cloud SDK: 548.0.0
Terraform: 1.6.6
Virtual Environment: .venv in C:\git\a-s-p
```

**Tools Pending:**
- Make (optional for development tasks - will install if needed later)

**Current Status:**
- Environment fully configured and ready
- All core prerequisites installed
- Authentication working
- Ready to start Day 2 challenge

---

## Day 2 - December 3, 2025 ✅

### Challenge: Build Your First AI Agent with YAML (No Code!)

**Goal:** Create a working AI agent using only 4 lines of YAML configuration

**What We Accomplished:**
1. ✅ Installed google-adk package (v1.19.0)
2. ✅ Created first YAML-based agent: `my_agent`
3. ✅ Configured Vertex AI backend with Gemini 2.5 Flash
4. ✅ Enabled Vertex AI API in Google Cloud project
5. ✅ Fixed configuration issues (.env file location settings)
6. ✅ Successfully launched ADK web UI
7. ✅ Agent responding to questions via web interface!
8. ✅ Added Google Search tool - agent now has real-time internet access!
9. ✅ Tested and verified search functionality with live weather query

**Key Learnings:**
- **ADK (Agent Development Kit):** Google's toolkit for building YAML-configured agents without code
- **YAML Configuration:** Simple text format to define agent behavior
  - `name`: Agent identifier
  - `description`: What the agent does
  - `instruction`: How the agent should behave
  - `model`: Which AI model to use (gemini-2.5-flash)
- **Vertex AI vs Google AI:** Two different backends for accessing Gemini
  - Vertex AI uses Application Default Credentials (no API key needed)
  - Configuration via `.env` file with project and location settings
- **Working Directory Matters:** ADK must be run from the parent directory containing agent folders
  - ❌ `cd my_agent; adk web .` → looks for agents INSIDE my_agent
  - ✅ `cd C:\git; adk web .` → finds my_agent AS an agent

**Agent Structure Created:**
```
C:\git\my_agent\
  ├── root_agent.yaml    # Agent configuration (name, model, instructions)
  ├── .env              # Vertex AI credentials (project, location)
  └── __init__.py       # Python package marker
```

**Configuration Details:**
```yaml
# root_agent.yaml - Final working version with Google Search
name: root_agent
description: A helpful assistant for user questions.
instruction: Answer user questions to the best of your knowledge
model: gemini-2.5-flash
tools:
  - name: google_search
```

```env
# .env
GOOGLE_GENAI_USE_VERTEXAI=1
GOOGLE_CLOUD_PROJECT=advent-of-agents
GOOGLE_CLOUD_LOCATION=us-central1
```

**Challenges Overcome:**
1. **404 Error with malformed URL:** Initial YAML had wrong format - needed simple string for model, not dictionary
2. **Location set to "y":** Interactive setup didn't save location properly - manually fixed .env file
3. **403 Permission Denied:** Vertex AI API not enabled - ran `gcloud services enable`
4. **Agent not loading in UI:** Running from wrong directory - needed to run from parent folder containing agents
5. **Multiple failed attempts:** Learned through trial and error about ADK's directory expectations
6. **Tools not working:** Server was caching old configuration - had to restart on new port (8006) to pick up tools changes

**Key Discovery:** When adding tools, need to restart the web server completely for changes to take effect!

**Commands Used:**
```powershell
# Create agent
adk create --type=config my_agent

# Enable Vertex AI API
gcloud services enable aiplatform.googleapis.com --project=advent-of-agents

# Launch web UI (from parent directory)
cd C:\git
adk web . --port 8006

# Access UI at: http://127.0.0.1:8006
```

**What's Next:**
- ~~Add Google Search tool to agent~~ ✅ DONE!
- Implement MCP (Model Context Protocol) - Day 3
- Create multi-agent communication

**Status:** Day 2 COMPLETE! Agent with Google Search working perfectly! 🎉

---

## Why This Matters - ELI5

**What is ChatGPT?**
- A single AI chatbot
- One conversation at a time
- Can't do tasks for you
- Limited to what OpenAI built

**What you're building:**
- **YOUR OWN AI system** that you control
- Can connect to YOUR business data (databases, APIs, files)
- Can take ACTIONS (send emails, update databases, make API calls)
- Can have MULTIPLE agents working together (like a team)
- FREE to modify and customize however you want
- Runs on YOUR infrastructure (Google Cloud)
- Can be integrated into YOUR apps

**Real Examples:**

**ChatGPT:** "What's the status of order #12345?"
→ ChatGPT: "I don't have access to your order system"

**YOUR Agent:** "What's the status of order #12345?"
→ Agent checks YOUR database → "Order #12345 shipped yesterday, tracking: ABC123"

**ChatGPT:** "Email the marketing team about the event"
→ ChatGPT: "I can't send emails, but here's a draft"

**YOUR Agent:** "Email the marketing team about the event"
→ Agent accesses YOUR email system → Actually sends the email

**The Big Picture:**
- ChatGPT = Renting someone else's AI
- What you're doing = Building YOUR OWN AI infrastructure
- You're learning to create custom AI workers for YOUR specific needs
- This is the foundation for building AI-powered businesses

---

## Day 3 - December 4, 2025 ✅

### Challenge: Upgrade to Gemini 3 Pro with Advanced Features

**Goal:** Upgrade agent to newer Gemini model and explore advanced features (Live API, Computer Use, Real-time Streaming)

**What We Accomplished:**
1. ✅ Reauthenticated after overnight credential expiration
2. ✅ Updated agent instructions with detailed requirements
   - "Cite your sources. Always provide answers clearly based on search results"
   - Added custom Geordie accent instruction
3. ✅ Investigated model availability in Vertex AI
4. ✅ **FIXED: Discovered `gemini-3-pro-preview` works with `location=global`**
5. ✅ Confirmed ADK automatically handles publisher path conversion
6. ✅ Verified new agent configuration working with Gemini 3 Pro

**What We Discovered (AND FIXED):**
- ✅ `gemini-3-pro-preview` requires `GOOGLE_CLOUD_LOCATION=global` (not `us-central1`)
- ✅ Agent now reads YAML config correctly (Geordie accent verified!)
- ✅ Tested and working with Gemini 3 Pro model
- ✅ ADK converts simple model names to full resource paths automatically

**Model Investigation:**
- Checked Google Cloud Console → Vertex AI → Model Garden
- Found that `gemini-3-pro-preview` exists in Vertex AI BUT your project doesn't have access
- Model Garden shows: "Provisioned Throughput available" but model returns 404 when used

**Key Learnings:**
- **Region Matters:** Preview model only works with `GOOGLE_CLOUD_LOCATION=global`
- **Server Caching:** Full restart still required to pick up YAML changes
- **Model Name Format:** Use short name; ADK builds the full publisher path automatically
- **Configuration Verification:** Check Events tab in web UI to confirm model in use
- **Official Samples Help:** Matched Python SDK sample to understand location/model requirements

**Commands Learned:**
```powershell
# Kill all Python processes
Get-Process | Where-Object {$_.ProcessName -like "*python*"} | Stop-Process -Force

# Complete fresh restart
cd C:\git\a-s-p
& "C:\Users\markc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\local-packages\Python313\Scripts\adk.exe" web . --port 8006

# Access web UI
http://localhost:8006
```

**Current Agent Configuration:**
```yaml
name: root_agent
description: A helpful assistant for user questions.
instruction: Answer user questions to the best of your knowledge and cite your sources. Always provide answers clearly based on search results. Answer with a Geordie accent.
model: gemini-3-pro-preview
tools:
  - name: google_search
```

**Environment (CORRECTED):**
```env
GOOGLE_GENAI_USE_VERTEXAI=1
GOOGLE_CLOUD_PROJECT=advent-of-agents
GOOGLE_CLOUD_LOCATION=global
```

**Status:** Day 3 COMPLETE ✅
- ✅ Model updated to Gemini 3 Pro
- ✅ Region corrected to `global` (was `us-central1`)
- ✅ Agent working with new model and instructions
- ✅ Google Search tool integrated

---

## Resources & Quick Reference

### Important Commands
```powershell
# Activate virtual environment
.\.venv\Scripts\Activate.ps1

# Check installations
python --version
agent-starter-pack --version
gcloud --version

# Navigate to project
cd C:\git\a-s-p

# Check gcloud config
gcloud config list
```

### Project Paths
- **Repository:** `C:\git\a-s-p`
- **Virtual Environment:** `C:\git\a-s-p\.venv`
- **Google Cloud Project ID:** `advent-of-agents`

### Useful Links
- [Advent of Agents](https://adventofagents.com/)
- [Agent Starter Pack Docs](https://googlecloudplatform.github.io/agent-starter-pack/)
- [ADK Documentation](https://google.github.io/adk-docs/)
- [Vertex AI Agent Engine](https://docs.cloud.google.com/agent-builder/agent-engine/overview)

---

## Notes for Future Days

### Things to Remember:
- Always activate virtual environment before working
- VS Code may need restart after installing system-level tools
- Keep track of Project ID when working with Google Cloud

### Coaching Notes:
- Ask for permission before running commands
- Explain what each step does
- One step at a time, building understanding

---

## Day 4 - December 5, 2025 🔄 In Progress

### Challenge: Source-Based Deployment with Agent Engine

**Goal:** Deploy source directly to Agent Engine using the new deployment flow.

**What We Accomplished:**
1. ✅ Enabled Windows long paths in registry; rebooted
2. ✅ Fixed uv/uvx installation issues (antivirus blocking)
3. ✅ Installed `uv` package manager (v0.9.15) into `C:\git\a-s-p`
4. ✅ Installed `agent-starter-pack` package locally
5. ✅ Created new project `C:\git\agent-4` via `uv tool run agent-starter-pack -- create agent-4 -a adk_base -d agent_engine -y`
   - Clean scaffold with Agent Engine deployment target
   - Automatic GCP project verification (advent-of-agents confirmed)
6. ✅ Uninstalled/reinstalled Chocolatey (admin PowerShell)
7. ✅ Installed GNU Make v4.4.1 via Chocolatey
8. ✅ Exported dependencies: `uv export` → `app/app_utils/.requirements.txt`
9. ✅ Verified deployment tooling available

**Key Learnings (Day 4):**
- **Windows Long Paths:** Needed registry fix + reboot for agent-starter-pack Jinja templating
- **Separate Projects:** Keep `agent-4` separate from `a-s-p` repo to avoid template collisions
- **uv Tool Management:** `uv tool run` lets you run CLIs without polluting your environment
- **Chocolatey + Admin:** Some package managers (Chocolatey) require elevated PowerShell
- **Requirements Export:** `uv export` generates the exact dependency list for deployment

**Final Deployment:**
- ✅ Reauthenticated: `gcloud auth application-default login`
- ✅ Deployed: `uv run -m app.app_utils.deploy --source-packages=./app --entrypoint-module=app.agent_engine_app --entrypoint-object=agent_engine --requirements-file=app/app_utils/.requirements.txt`
- ✅ Agent Engine ID: 3999649467895644160
- ✅ Service Account: service-233209475586@gcp-sa-aiplatform-re.iam.gserviceaccount.com
- ✅ Console Playground: https://console.cloud.google.com/vertex-ai/agents/locations/us-central1/agent-engines/3999649467895644160/playground

**Status:** Day 4 COMPLETE ✅
- All tooling installed and working
- agent-4 deployed to Vertex AI Agent Engine
- Telemetry enabled (GOOGLE_CLOUD_AGENT_ENGINE_ENABLE_TELEMETRY=true)
- Production observability automatically provisioned

---

## Day 5 - December 8, 2025 ✅

### Challenge: Production Observability

**Goal:** Verify zero-config observability infrastructure automatically provisioned during deployment

**What We Accomplished:**
1. ✅ Verified Cloud Trace captures agent execution traces, LLM calls, and latency
2. ✅ Confirmed Log Analytics and Log Buckets are collecting agent logs
3. ✅ Checked BigQuery dataset for agent execution logs with custom views
4. ✅ Tested agent in Console Playground to generate telemetry data

**Key Learnings:**
- **Zero-Config Observability:** Agent Starter Pack auto-provisions:
  - Cloud Trace for execution traces with latency breakdown
  - Log Analytics + Log Buckets with custom retention
  - BigQuery Delta Lake with custom views for querying
- **Already Enabled:** Telemetry automatically configured during Day 4 deployment:
  - `GOOGLE_CLOUD_AGENT_ENGINE_ENABLE_TELEMETRY=true`
  - `OTEL_INSTRUMENTATION_GENAI_CAPTURE_MESSAGE_CONTENT=true`
- **Terraform Provisioned:** All infrastructure deployed automatically
- **Privacy by Design:** Sensitive content stored in GCS, not logs

**Verification:**
- Console Playground: https://console.cloud.google.com/vertex-ai/agents/locations/us-central1/agent-engines/3999649467895644160/playground
- Cloud Trace: https://console.cloud.google.com/traces/list?project=advent-of-agents
- Logs: https://console.cloud.google.com/logs/query?project=advent-of-agents
- BigQuery: https://console.cloud.google.com/bigquery?project=advent-of-agents

**Status:** Day 5 COMPLETE ✅
- Observability was automatic from Day 4 deployment
- All traces, logs, and analytics verified working

---

## Day 6 - December 8, 2025 ✅

### Challenge: IDE Integration

**Goal:** Verify ADK works in multiple IDEs without configuration

**What We Learned:**
1. ✅ **IDE = Integrated Development Environment** - Super-powered text editor for coding
   - Text editor with syntax highlighting and auto-completion
   - Terminal for running commands
   - File explorer for browsing project structure
   - Debugging tools for finding errors
   
2. ✅ **VS Code is an IDE** - What we've been using this whole time!
   - Successfully editing YAML files
   - Running commands in integrated terminal
   - Browsing project files in sidebar
   
3. ✅ **IDE Magnet Context** - Agent Starter Pack works everywhere:
   - No special IDE setup required
   - ADK commands work from any IDE terminal
   - Configuration files get syntax highlighting automatically
   
4. ✅ **Other IDE Options:**
   - **Cursor** - AI-powered IDE with built-in coding assistant
   - **Firebase Studio** - Google's web-based IDE (browser-based)
   - **Gemini CLI** - Command-line interface for Gemini
   - **PyCharm** - Python-focused IDE

**Key Insight - llms.txt for Technical SEO:**
- Discovered https://llmstxt.org/ - standard for making documentation LLM-readable
- Similar to robots.txt but for AI agents/LLMs
- Could become essential for technical SEO as AI search becomes dominant
- Makes documentation accessible to AI tools without custom scraping

**Status:** Day 6 COMPLETE ✅
- Verified VS Code works seamlessly with ADK
- No configuration required - everything just works
- Understanding of IDE concept and tooling options

---

## Summary - December 8, 2025

**Completed This Session:**
- ✅ Day 4: Deployed agent-4 to Vertex AI Agent Engine
- ✅ Day 5: Verified production observability (Cloud Trace, Logs, BigQuery)
- ✅ Day 6: IDE integration verified (VS Code working perfectly)

**Key Learnings:**
- Observability is zero-config with Agent Starter Pack
- IDE support works out-of-the-box (no setup needed)
- llms.txt could become critical for technical SEO with AI search

**Installed Tools Summary:**
- Python 3.13.9 ✅
- Google Cloud SDK ✅
- Agent Starter Pack ✅
- uv package manager v0.9.15 ✅
- Chocolatey v2.6.0 ✅
- GNU Make 4.4.1 ✅
- google-adk v1.19.0 ✅
- Vertex AI SDK ✅

---

*Last Updated: December 8, 2025*
