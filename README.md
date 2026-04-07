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

### Create Your Own Workflows

**🎨 Interactive in VS Code**: Open Copilot Chat and ask "Help me create a workflow that..." - the VS Code agent will guide you step-by-step

**📋 Or use the web form**: Submit a workflow request via Issues and an AI agent will generate it automatically

📖 **See [Creating Your Own Agentic Workflows](#-creating-your-own-agentic-workflows) for all options**

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

**How to Use**:

1. **Open VS Code** in this repository
2. **Open Copilot Chat** (Ctrl+Alt+I or Cmd+Alt+I)
3. **Start a conversation** with prompts like:
   ```
   Help me create a workflow that sends a Slack notification when PRs are merged
   ```
   ```
   Create a workflow that runs security scans on new commits
   ```
   ```
   I need a workflow that auto-assigns reviewers based on file paths
   ```

4. **The agent will**:
   - Ask clarifying questions (trigger, actions, tools needed)
   - Suggest a workflow design
   - Generate the `.md` file
   - Compile it for you
   - Provide testing instructions

**Example Conversation**:
```
You: Create a workflow that welcomes new contributors

Agent: I'll help you create a welcome workflow! A few questions:
1. When should it trigger? (first issue, first PR, both?)
2. Should it comment, add a label, or both?
3. Any specific message you'd like to include?

You: Trigger on first PR, add a comment and a "first-contribution" label

Agent: Perfect! I'll create a workflow that:
- Triggers on pull_request (opened)
- Checks if it's the contributor's first PR
- Adds a welcoming comment
- Applies the "first-contribution" label

[Agent generates the workflow file]

Done! I've created .github/workflows/welcome-contributor.md
Run this to compile it:
gh aw compile welcome-contributor
```

**Why use the VS Code agent?**
- 🎯 **Interactive** - Back-and-forth conversation to refine requirements
- 🧠 **Smart suggestions** - Knows common patterns and best practices
- ⚡ **Fast iteration** - Test and modify workflows quickly
- 📚 **Learning tool** - Explains decisions and teaches you gh-aw

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

## � Pricing & Cost Considerations

### AI Engine Costs

GitHub Agentic Workflows require an AI engine to power the agents. Here's what you need to know about pricing:

#### Option 1: GitHub Copilot (Recommended)

**Pricing Models**:
- **GitHub Copilot Individual**: $10/month or $100/year
- **GitHub Copilot Business**: $19/user/month
- **GitHub Copilot Enterprise**: $39/user/month

**What's Included for Agentic Workflows**:
- ✅ Unlimited workflow executions
- ✅ Access to GPT-4 and GPT-4-turbo models
- ✅ No per-request charges
- ✅ Built-in rate limiting and quotas
- ✅ Enterprise-grade security and compliance

**Best For**: Teams already using GitHub Copilot, or those wanting predictable monthly costs.

**Example Cost**:
```
Organization with 10 developers using Copilot Business
= $19 × 10 = $190/month (all workflows included)
```

#### Option 2: External AI Models (Claude, GPT-4, etc.)

**Claude (Anthropic)**:
- **Claude 3.5 Sonnet**: $3 per million input tokens, $15 per million output tokens
- **Claude 3 Opus**: $15 per million input tokens, $75 per million output tokens
- **Claude 3 Haiku**: $0.25 per million input tokens, $1.25 per million output tokens

**OpenAI Direct**:
- **GPT-4 Turbo**: $10 per million input tokens, $30 per million output tokens
- **GPT-4**: $30 per million input tokens, $60 per million output tokens
- **GPT-3.5 Turbo**: $0.50 per million input tokens, $1.50 per million output tokens

**Best For**: Organizations wanting flexibility, using multiple AI providers, or needing specific model capabilities.

**Example Cost** (Claude 3.5 Sonnet):
```
Typical issue triage workflow:
- Input: ~2,000 tokens (issue content + instructions)
- Output: ~500 tokens (labels, comments, analysis)
- Cost per execution: ($3 × 0.002) + ($15 × 0.0005) = $0.006 + $0.0075 = ~$0.014

For 100 issues/month: $1.40/month
For 1,000 issues/month: $14/month
```

### GitHub Actions Costs

Workflows run on GitHub Actions, which has its own pricing:

**GitHub Actions Minutes**:
- **Public repositories**: ✅ Free unlimited
- **Private repositories**: 
  - Free tier: 2,000 minutes/month (GitHub Free)
  - Team: 3,000 minutes/month
  - Enterprise: 50,000 minutes/month
  - Additional: $0.008/minute (Linux runners)

**Typical Workflow Executions**:
- Simple issue triage: ~30-60 seconds
- Complex PR review: ~2-5 minutes
- Daily report generation: ~1-3 minutes

**Example Cost**:
```
Private repo with 500 issues/month:
- Executions: 500 × 1 minute = 500 minutes
- Within free tier: $0/month
- If exceeding: 500 × $0.008 = $4/month (Actions overage)
```

### Total Cost Estimation

#### Scenario 1: Small Team (5 developers, ~200 issues/month)

**Option A - Using Copilot**:
```
GitHub Copilot Business:     $95/month (5 × $19)
GitHub Actions:               $0/month (within free tier)
────────────────────────────
Total:                        $95/month
Cost per workflow execution:  $0.48
```

**Option B - Using Claude 3.5 Sonnet**:
```
Claude API costs:             ~$2.80/month (200 × $0.014)
GitHub Actions:               $0/month (within free tier)
────────────────────────────
Total:                        $2.80/month
Cost per workflow execution:  $0.014
```

#### Scenario 2: Medium Team (20 developers, ~1,500 issues+PRs/month)

**Option A - Using Copilot**:
```
GitHub Copilot Business:      $380/month (20 × $19)
GitHub Actions:               $0/month (within free tier)
────────────────────────────
Total:                        $380/month
Cost per workflow execution:  $0.25
```

**Option B - Using Claude 3.5 Sonnet**:
```
Claude API costs:             ~$21/month (1,500 × $0.014)
GitHub Actions:               $5/month (overage)
────────────────────────────
Total:                        $26/month
Cost per workflow execution:  $0.017
```

#### Scenario 3: Enterprise (100+ developers, 10,000+ events/month)

**Option A - Using Copilot Enterprise**:
```
GitHub Copilot Enterprise:    $3,900/month (100 × $39)
GitHub Actions:               Included in Enterprise
────────────────────────────
Total:                        $3,900/month
Cost per workflow execution:  $0.39
```

**Option B - Using Claude (optimized)**:
```
Claude 3 Haiku (fast tasks):  ~$20/month (8,000 × $0.0025)
Claude 3.5 Sonnet (complex):  ~$28/month (2,000 × $0.014)
GitHub Actions:               $50/month (overage)
────────────────────────────
Total:                        $98/month
Cost per workflow execution:  $0.01
```

### Cost Optimization Tips

1. **Choose the Right Engine**:
   - Already have Copilot? → Use it (no additional cost)
   - Pay-per-use preference? → Use Claude Haiku for simple tasks
   - Need latest capabilities? → Use Claude 3.5 Sonnet or GPT-4

2. **Optimize Workflow Triggers**:
   - Use debouncing: Wait for multiple edits before reprocessing
   - Filter events: Only trigger on meaningful changes
   - Use `workflow_dispatch` for testing (manual triggers)

3. **Configure Safe Outputs Wisely**:
   - Set `max` limits to prevent runaway costs
   - Use `noop` output when no action is needed

4. **Token Optimization**:
   - Keep prompts concise and focused
   - Use summarization for long issues/PRs
   - Cache context when possible (upcoming feature)

5. **Use Scheduled Workflows Efficiently**:
   - Batch operations (daily reports vs per-event)
   - Run during off-peak hours
   - Use fuzzy scheduling to spread load

6. **Monitor Usage**:
   - Track workflow execution counts
   - Monitor API token usage
   - Review GitHub Actions minutes consumption
   - Set up budget alerts

### Cost Comparison Summary

| Use Case | Best Choice | Monthly Cost | Notes |
|----------|-------------|--------------|-------|
| Small team, already using Copilot | GitHub Copilot | ~$95-$190 | No additional cost if you have Copilot |
| Small team, no Copilot | Claude Haiku | ~$1-5 | Most cost-effective for low volume |
| Medium team with Copilot | GitHub Copilot | ~$380 | Predictable, unlimited usage |
| Medium team, no Copilot | Claude 3.5 Sonnet | ~$20-50 | Pay-per-use flexibility |
| Enterprise with Copilot | GitHub Copilot Enterprise | ~$3,900+ | Includes advanced features |
| Enterprise, cost-sensitive | Claude (mixed) | ~$100-500 | Use Haiku for simple tasks, Sonnet for complex |
| Public open-source projects | Any option | $0-10 | GitHub Actions free, minimal AI costs |

### Hidden Costs to Consider

- **Development Time**: Setting up and maintaining workflows
- **Learning Curve**: Training team on agentic workflow patterns
- **Infrastructure**: Additional tooling, monitoring, and logging
- **Support**: Troubleshooting and debugging workflow issues

**💡 Pro Tip**: For most teams, GitHub Copilot provides the best value if you're already using it for code completion. For new teams or low-volume usage, Claude Haiku offers the lowest per-execution cost.

---

## �🐛 Troubleshooting

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