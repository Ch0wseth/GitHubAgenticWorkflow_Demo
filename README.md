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

## 📁 Project Structure

```
.
├── .github/
│   └── workflows/
│       └── issue-triage.md   # Agentic workflow for issue triage
├── website/
│   ├── index.html            # Main HTML page with content
│   ├── styles.css            # Modern dark-themed styling
│   └── script.js             # Interactive JavaScript features
├── .gitattributes            # Git attributes for lock files
└── README.md                 # This file
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

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| **Issue Triage** | New/edited issues | Automatically labels, prioritizes, and assigns issues |
| **Daily Activity Report** | Daily (weekdays) | Generates a comprehensive activity report |
| **Workflow Generator** | Issue with `workflow-request` label | Creates new workflows from issue templates |

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