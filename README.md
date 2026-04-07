# GitHub Agentic Workflow - Technical Demo

An interactive technical presentation on GitHub Agentic Workflow architecture, implementation patterns, and enterprise deployment strategies. Designed for software architects, senior developers, and engineering leads.

## 🎯 Purpose

This project provides a comprehensive technical overview of **GitHub Agentic Workflow** - an architectural pattern leveraging LLM-powered autonomous agents to orchestrate SDLC tasks through event-driven architecture, tool integration, and state management.

### Target Audience
- Software Architects & Technical Leads
- Senior/Staff Engineers
- DevOps & Platform Engineers
- Engineering Managers evaluating AI tooling

## 🚀 Quick Start

### View the Technical Demo

Simply open `website/index.html` in your web browser to view the demo:

```bash
# Option 1: Direct open
start website\index.html

# Option 2: Using Python's HTTP server
cd website
python -m http.server 8000

# Option 3: Using Node's http-server (if installed)
cd website
npx http-server
```

Then navigate to `http://localhost:8000` in your browser.

### Try the Live Workflows

This repository includes **3 active agentic workflows** you can test right now:

1. **🤖 Test Issue Triage**: [Create a test issue](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/issues/new) and watch it get automatically labeled and triaged

2. **📊 Generate Daily Report**: Go to [Actions](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/actions) → "Daily Repository Activity Report" → "Run workflow"

3. **🔧 Create a New Workflow**: Use the [workflow creation template](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/issues/new/choose) to generate a custom workflow via AI

📖 **See [Testing the Workflows](#-testing-the-workflows) for detailed instructions**

## 📁 Project Structure

```
.
├── .github/
│   ├── agents/
│   │   └── workflow-creator.agent.md      # VS Code agent for creating workflows
│   ├── ISSUE_TEMPLATE/
│   │   └── create-workflow.yml            # Issue template for workflow requests
│   └── workflows/
│       ├── issue-triage.md                # Agentic workflow: Issue triage
│       ├── issue-triage.lock.yml          # Compiled workflow (auto-generated)
│       ├── daily-activity-report.md       # Agentic workflow: Daily reports
│       ├── daily-activity-report.lock.yml # Compiled workflow (auto-generated)
│       ├── workflow-generator.md          # Agentic workflow: Workflow creation
│       └── workflow-generator.lock.yml    # Compiled workflow (auto-generated)
├── website/
│   ├── index.html                         # Main HTML page with content
│   ├── styles.css                         # Modern dark-themed styling
│   └── script.js                          # Interactive JavaScript features
├── TEST_SCENARIOS.md                      # Test scenarios for issue triage
├── create-test-issues.ps1                 # Automated test script
├── .gitattributes                         # Git attributes for lock files
└── README.md                              # This file
```

## 🤖 Live Workflow Example: Issue Triage Agent

This repository includes a real **GitHub Agentic Workflow** that demonstrates automated issue triage. The workflow automatically:

- **Labels by type**: Classifies issues as bug, feature, documentation, question, or maintenance
- **Assesses priority**: Evaluates urgency and assigns priority levels (critical, high, medium, low)
- **Detects duplicates**: Searches for similar existing issues and flags potential duplicates
- **Requests clarification**: Asks follow-up questions when issue descriptions are unclear
- **Assigns team members**: Routes issues to appropriate team members based on content

### Setup Instructions

To activate this workflow in your fork:

1. **Compile the workflow** (requires [gh-aw CLI](https://github.com/github/gh-aw)):
   ```bash
   # Install gh-aw if not already installed
   curl -sL https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh | bash
   
   # Compile the workflow
   gh aw compile issue-triage
   ```

2. **Commit and push**:
   ```bash
   git add .gitattributes .github/workflows/issue-triage.md .github/workflows/issue-triage.lock.yml
   git commit -m "Add issue triage agentic workflow"
   git push
   ```

3. **Test it**: Open a new issue in your repository and watch the agent automatically triage it!

### How It Works

The workflow uses:
- **Trigger**: Activates on `issues: [opened, edited]`
- **Permissions**: Read-only access (secure by default)
- **Tools**: GitHub MCP server for searching and analyzing issues
- **Safe Outputs**: Controlled actions (commenting, labeling, assigning) with rate limits
- **AI Engine**: GitHub Copilot (default) for intelligent decision-making

See [.github/workflows/issue-triage.md](.github/workflows/issue-triage.md) for the complete workflow definition.

## 🔧 Creating Your Own Agentic Workflows

This repository provides **3 different ways** to create new agentic workflows:

### Option A: VS Code Agent Assistant 🤖

Use the **Workflow Creator Agent** directly in VS Code:

1. Open VS Code in this repository
2. Start a chat with GitHub Copilot
3. Ask: "Help me create a workflow that..."
4. The agent will guide you through the creation process interactively

The agent knows:
- Common workflow patterns (issue triage, PR review, daily reports)
- Security best practices
- Safe outputs configuration
- Tool selection and integration

**Files**: [.github/agents/workflow-creator.agent.md](.github/agents/workflow-creator.agent.md)

### Option B: Automated Workflow Generator 🚀

Submit a workflow request via GitHub Issues and let an AI agent create it for you:

1. **Go to Issues** → **New Issue**
2. **Select**: "🤖 Create Agentic Workflow" template
3. **Fill out the form**:
   - Workflow name and description
   - When it should run (trigger)
   - What actions it should perform
4. **Submit** the issue
5. **Wait** for the AI agent to:
   - Generate the workflow files
   - Compile them
   - Create a Pull Request
   - Comment on your issue with the PR link

**Files**: 
- Template: [.github/ISSUE_TEMPLATE/create-workflow.yml](.github/ISSUE_TEMPLATE/create-workflow.yml)
- Workflow: [.github/workflows/workflow-generator.md](.github/workflows/workflow-generator.md)

### Option C: Manual Creation with gh-aw CLI 💻

Create workflows manually using the gh-aw CLI:

1. **Install gh-aw** (if not already installed):
   ```bash
   # Linux/Mac
   curl -sL https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh | bash
   
   # Windows PowerShell
   $ExtensionDir = "$env:USERPROFILE\.local\share\gh\extensions\gh-aw"
   New-Item -ItemType Directory -Force -Path $ExtensionDir | Out-Null
   Invoke-WebRequest -Uri "https://github.com/github/gh-aw/releases/latest/download/windows-amd64.exe" -OutFile "$ExtensionDir\gh-aw.exe"
   ```

2. **Create a workflow file** `.github/workflows/my-workflow.md`:
   ```markdown
   ---
   description: Brief description of what this workflow does
   on:
     issues:
       types: [opened]
   permissions:
     contents: read
     issues: read
   tools:
     github:
       toolsets: [default]
   safe-outputs:
     add-comment:
       max: 1
   ---
   
   # Workflow Name
   
   You are an AI agent that [does something].
   
   ## Your Task
   
   [Instructions for the agent]
   ```

3. **Compile the workflow**:
   ```bash
   # Linux/Mac
   gh aw compile my-workflow
   
   # Windows
   & "$env:USERPROFILE\.local\share\gh\extensions\gh-aw\gh-aw.exe" compile my-workflow
   ```

4. **Commit and push**:
   ```bash
   git add .github/workflows/
   git commit -m "Add my-workflow"
   git push
   ```

**Resources**:
- [Official gh-aw Documentation](https://github.github.com/gh-aw/)
- [Workflow Examples](.github/workflows/)

---

## 📊 Active Workflows in This Repository

| Workflow | Trigger | Purpose | Test Instructions |
|----------|---------|---------|-------------------|
| **Issue Triage** | New/edited issues | Automatically labels, prioritizes, and assigns issues | [Create an issue](#testing-issue-triage) |
| **Daily Activity Report** | Daily (weekdays) | Generates a comprehensive activity report | [Run manually](#testing-daily-report) or wait for schedule |
| **Workflow Generator** | Issue with template | Creates new workflows from issue templates | [Use issue template](#testing-workflow-generator) |

## 🧪 Testing the Workflows

### Testing Issue Triage

The easiest way is to use the **pre-built test scenarios**:

#### Option 1: Automated Test Script (Recommended)

```powershell
.\create-test-issues.ps1
```

This automatically creates 7 test issues covering different scenarios (bugs, features, vague questions, duplicates, etc.).

#### Option 2: Manual Testing

1. Go to [Issues → New Issue](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/issues/new)
2. Create an issue with one of the scenarios from [TEST_SCENARIOS.md](TEST_SCENARIOS.md)
3. Wait 30-60 seconds
4. Check the issue for:
   - ✅ Applied labels (bug, feature, priority levels)
   - 💬 Comments (clarifying questions, duplicate detection)
   - 👤 Assignments (if configured)

**Expected Results**:
- Critical bugs get `priority: critical` label
- Vague issues get clarifying questions + `needs-info` label
- Similar issues are flagged as potential duplicates

### Testing Daily Report

#### Option 1: Manual Trigger (Fastest)

1. Go to [Actions](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/actions)
2. Click **"Daily Repository Activity Report"**
3. Click **"Run workflow"** button
4. Wait ~60 seconds
5. Check [Issues](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/issues) for the new report

#### Option 2: Wait for Scheduled Run

The workflow runs automatically every weekday morning (fuzzy scheduled time).

**Expected Results**:
- 📊 New issue titled "📊 Daily Activity Report - [Date]"
- 📈 Summary statistics (issues, PRs, commits)
- ✅ Action items checklist
- 🔄 Previous daily reports automatically closed

### Testing Workflow Generator

1. Go to [New Issue → Choose Template](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/issues/new/choose)
2. Select **"🤖 Create Agentic Workflow"** template
3. Fill out the form with a test workflow:
   ```
   Name: Test Greeting Workflow
   Description: Comment "Hello!" on new issues
   Trigger: When issues are opened or edited
   Actions: ✓ Add comments to issues or PRs
   ```
4. Check both acknowledgments and submit
5. Go to [Actions](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/actions) to watch it run
6. After ~2 minutes, check:
   - 💬 Comment on your issue with status
   - 🔀 New PR with the generated workflow files

**Expected Results**:
- PR created with `.github/workflows/test-greeting-workflow.md` and `.lock.yml`
- PR includes testing instructions
- Workflow is ready to merge and activate

## 📝 Test Resources

- **[TEST_SCENARIOS.md](TEST_SCENARIOS.md)**: Detailed test scenarios for issue triage
- **[create-test-issues.ps1](create-test-issues.ps1)**: Automated script to create all test scenarios

---

## 🔧 Configuration & Secrets

### Required Secrets

To use GitHub Copilot as the AI engine, you need to configure:

1. **Create a Fine-Grained Personal Access Token**:
   - Go to https://github.com/settings/personal-access-tokens/new
   - Name: `GitHub Copilot for Workflows`
   - Repository access: Select this repository
   - Permissions:
     - **Copilot**: Read and write
     - **Issues**: Read and write
     - **Metadata**: Read-only
   - Account permissions:
     - **Copilot user**: Read

2. **Add Secret to Repository**:
   - Go to [Settings → Secrets → Actions](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/settings/secrets/actions)
   - Click **"New repository secret"**
   - Name: `COPILOT_GITHUB_TOKEN`
   - Value: Paste your fine-grained token (starts with `github_pat_...`)

### Alternative: Use Claude

To use Claude instead of Copilot, add `engine: claude` to any workflow frontmatter and configure `ANTHROPIC_API_KEY` secret.

---

## 🐛 Troubleshooting

### Workflow Not Triggering

**Problem**: Created an issue but the workflow didn't run.

**Solutions**:
1. Check [Actions tab](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/actions) - workflow might have run but failed
2. Verify the workflow files are pushed to the `main` branch
3. Check repository Settings → Actions → General → ensure workflows are enabled

### "COPILOT_GITHUB_TOKEN secret not found"

**Problem**: Workflow fails with secret validation error.

**Solution**:
1. Create a fine-grained PAT (not classic): https://github.com/settings/personal-access-tokens/new
2. Token must start with `github_pat_...` (not `ghp_...`)
3. Select scopes: `copilot` (read+write), `copilot:user` (read)
4. Add to repository secrets as `COPILOT_GITHUB_TOKEN`

### Workflow Generator Creates PR but Files are Protected

**Problem**: "Cannot create pull request: patch modifies protected files"

**Solution**: This should be fixed in the latest version. Pull the latest changes:
```bash
git pull origin main
```

### Agent Comments but Doesn't Apply Labels

**Problem**: Agent comments on issues but labels aren't applied.

**Possible Causes**:
1. Labels don't exist in the repository - create them manually first
2. Permissions issue - check that safe-outputs are configured correctly
3. Check [Actions logs](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/actions) for detailed error messages

### Daily Report Not Generating

**Problem**: Scheduled workflow doesn't create daily reports.

**Solutions**:
1. Test manually first: Actions → "Daily Repository Activity Report" → "Run workflow"
2. Check if there was any activity in the last 24 hours (no activity = no report via `noop`)
3. Verify the workflow is on the `main` branch
4. Check [Actions tab](https://github.com/Ch0wseth/GitHubAgenticWorkflow_Demo/actions) for execution history

---

## ✨ Features

- **Technical Architecture Diagrams** - Visual representation of agent orchestration layers
- **Code Examples** - YAML configs, Python (AutoGen), GitHub Actions workflows
- **Implementation Patterns** - ReAct, multi-agent systems, state management
- **Security Best Practices** - Prompt injection defense, secret management, sandboxing
- **Enterprise Use Cases** - Microservices scaffolding, security-first review, legacy migration
- **API References** - GitHub REST/GraphQL, agent frameworks, vector databases
- **Metrics & KPIs** - Development velocity, code quality, technical debt reduction
- **Production Deployment** - CI/CD integration, monitoring, SLA considerations

## 📚 Content Sections

1. **Technical Overview** - Architecture patterns and implementation approaches
2. **Core Architecture Patterns** - Agent orchestration, tool integration, state management, event-driven design
3. **Architecture Diagram** - Multi-layer system visualization
4. **Technical Benefits & Metrics** - Quantifiable improvements with real KPIs
5. **Implementation Examples** - YAML agent config, AutoGen orchestration, GitHub Actions integration
6. **Enterprise Use Cases** - Production scenarios with technical depth
7. **Technical Resources & APIs** - SDKs, frameworks, APIs, tools
8. **Security & Compliance** - Comprehensive security considerations
9. **Implementation Roadmap** - POC to production deployment strategy

## 🔗 Featured Technical Resources

### Agent Frameworks & SDKs
- Microsoft AutoGen - Multi-agent orchestration
- LangChain & LangGraph - Agent chains and workflows
- Semantic Kernel - Enterprise AI orchestration
- Microsoft Agent Framework SDK

### Platform APIs
- GitHub REST API v3 & GraphQL v4
- GitHub Webhooks & Actions API
- Model Context Protocol (MCP)

### Infrastructure
- Vector Databases (ChromaDB, Pinecone, Weaviate, Qdrant)
- Code Analysis Tools (Semgrep, CodeQL, SonarQube)
- Tree-sitter for incremental parsing

### Reference Implementations
- Production-ready AutoGen examples
- LangChain templates and patterns
- GitHub Actions workflow integrations

## 🎨 Customization

You can easily customize:
- **Colors**: Edit CSS variables in `website/styles.css`
- **Content**: Modify sections in `website/index.html`
- **Features**: Add interactivity in `website/script.js`

## 🤝 Contributing

Feel free to enhance this demo by:
- Adding more resources
- Improving the design
- Adding new sections
- Fixing issues

## 📄 License

This project is open source and available for educational purposes.

## 🌟 Credits

Created as a demonstration project for GitHub Agentic Workflow in 2026.

---

**Happy Coding! 🤖✨**