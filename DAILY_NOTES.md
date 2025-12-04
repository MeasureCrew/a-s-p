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

## Day 3 - December 4, 2025 🔄 In Progress

### Challenge: Upgrade to Gemini 3 Pro with Advanced Features

**Goal:** Upgrade agent to newer Gemini model and explore advanced features (Live API, Computer Use, Real-time Streaming)

**What We Accomplished:**
1. ✅ Reauthenticated after overnight credential expiration
2. ✅ Updated agent instructions with detailed requirements
   - "Cite your sources. Always provide answers clearly based on search results"
   - Added custom Geordie accent instruction
3. ✅ Investigated model availability in Vertex AI
4. ✅ Discovered authentication and model access mechanisms
5. ✅ Learned about server caching and restart procedures

**What We Discovered (NOT Fixed Yet):**
- ❌ `gemini-3-pro-preview` model is NOT available in your `advent-of-agents` project
- ✅ Agent IS reading your new YAML configuration (Geordie accent proves it!)
- ✅ Agent IS working with fallback model: `gemini-2.0-flash`
- The model name format conversions (simple name → full resource path)

**Model Investigation:**
- Checked Google Cloud Console → Vertex AI → Model Garden
- Found that `gemini-3-pro-preview` exists in Vertex AI BUT your project doesn't have access
- Model Garden shows: "Provisioned Throughput available" but model returns 404 when used

**Key Learnings:**
- **Server Caching:** Changes to YAML don't immediately take effect - server must be fully restarted
  - Simple `Ctrl+C` might not be enough
  - Need to kill ALL Python processes with: `Get-Process | Where-Object {$_.ProcessName -like "*python*"} | Stop-Process -Force`
- **Model Fallback Behavior:** When requested model doesn't exist, ADK appears to fall back to `gemini-2.0-flash`
  - Evidence: YAML says `gemini-3-pro-preview` but Events tab shows `gemini-2.0-flash`
  - But new instructions ARE applied (Geordie accent working!)
- **Configuration Format:** ADK converts simple model names to full resource paths:
  - Input: `gemini-3-pro-preview`
  - Converted to: `projects/advent-of-agents/locations/us-central1/publishers/google/models/gemini-3-pro-preview`
- **Coaching is Better Than Guessing:** Had to actually search for fallback code rather than assuming

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

**Challenges Encountered:**
1. **Model Not Available:** Primary blocker - `gemini-3-pro-preview` not accessible in project
2. **Server Caching:** Changes to YAML not immediately reflected - needed hard restarts
3. **Ambiguous Behavior:** Unclear why agent responds with new instructions but uses old model
4. **Configuration Format Confusion:** Didn't initially understand ADK's model name conversion

**What We Need To Do Next:**
1. **Request Access** to Gemini 3 Pro model in Google Cloud project (might require project admin action)
   OR
2. **Find Available Model:** Determine which Gemini models your project DOES have access to
3. **Update YAML:** Use an available model instead of `gemini-3-pro-preview`

**Why Day 3 is Blocked:**
- Video tutorial uses `gemini-3-pro-preview` (or similar Gemini 3 model)
- Your project doesn't have access to that model
- Agent works, but with older model than intended
- Day 3 specifically focuses on Gemini 3 Pro features

**Status:** Day 3 PARTIALLY COMPLETE
- ✅ Configuration and instructions updated
- ✅ Server restart procedures learned
- ✅ Model availability investigation done
- ❌ Model access issue remains unresolved
- ⏸️ Advanced features testing blocked by model availability

**Next Session Action Items:**
1. Check Google Cloud Console for available Gemini models
2. Either request Gemini 3 Pro access OR switch to available model
3. Continue with Day 3 features once model access is resolved

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

*Last Updated: December 3, 2025*
