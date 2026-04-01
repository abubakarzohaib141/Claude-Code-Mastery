# Claude Code — Complete Course 🔥

> **The most comprehensive, beginner-to-advanced guide for Claude Code** — from zero setup to building real AI-powered workflows with custom models via Ollama.

![Claude Code Banner](https://img.shields.io/badge/Claude%20Code-Complete%20Course-orange?style=for-the-badge&logo=anthropic)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)
![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge)

---

## 📚 Table of Contents

| # | Chapter | Description |
|---|---------|-------------|
| 1 | [What is Claude Code?](#-chapter-1-what-is-claude-code) | Overview, use cases, and why it matters |
| 2 | [Installation & Setup](#-chapter-2-installation--setup) | System requirements, install steps, authentication |
| 3 | [Core Features](#-chapter-3-core-features) | All major capabilities explained |
| 4 | [How to Write Great Prompts](#-chapter-4-how-to-write-great-prompts) | Prompting strategies, templates, and anti-patterns |
| 5 | [Claude Code + Ollama](#-chapter-5-claude-code--ollama) | Run local models with Claude Code |
| 6 | [Real-World Workflows](#-chapter-6-real-world-workflows) | Projects, automation, and agentic tasks |
| 7 | [Tips, Tricks & Best Practices](#-chapter-7-tips-tricks--best-practices) | Power user guide |
| 8 | [Resources & Community](#-chapter-8-resources--community) | Docs, links, repos |

---

## 📖 Chapter 1: What is Claude Code?

### Overview

**Claude Code** is Anthropic's official **agentic coding tool** — a command-line interface (CLI) that gives you a fully autonomous AI coding assistant directly in your terminal.

Unlike simple chatbots, Claude Code can:

- Read, write, and edit your actual files on disk
- Execute shell commands and scripts
- Understand your entire codebase as context
- Make multi-step plans and execute them autonomously
- Search the web for real-time information
- Integrate with external tools via **MCP (Model Context Protocol)**

Think of it as having a senior software engineer embedded in your terminal — one that never gets tired, always reads the docs, and executes tasks end to end.

### Why Claude Code?

| Feature | Claude Code | Traditional AI Chat |
|--------|-------------|---------------------|
| File access | ✅ Real disk read/write | ❌ Copy-paste only |
| Command execution | ✅ Runs bash, Python, etc. | ❌ No execution |
| Codebase context | ✅ Full repo awareness | ⚠️ Limited by paste |
| Autonomous agents | ✅ Multi-step tasks | ❌ One-shot only |
| Local model support | ✅ Via Ollama | ❌ Cloud only |

### Use Cases

- 🧱 **Scaffold entire projects** from a single prompt
- 🐛 **Debug complex bugs** across multiple files
- ✍️ **Write and run tests** automatically
- 📝 **Generate documentation** from code
- 🔄 **Refactor legacy codebases**
- 🌐 **Build web scrapers, APIs, and automation scripts**
- 🤖 **Create agentic pipelines** with tool use

---

## ⚙️ Chapter 2: Installation & Setup

### System Requirements

- **OS**: macOS, Linux, or Windows (via WSL2)
- **Node.js**: v18 or higher
- **npm**: v8 or higher
- **RAM**: Minimum 4GB (8GB+ recommended)
- **Internet**: Required for Anthropic API (optional if using Ollama)

Check your Node version:

```bash
node --version   # should be v18+
npm --version    # should be v8+
```

### Step 1: Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

Verify the installation:

```bash
claude --version
```

### Step 2: Authenticate with Anthropic

```bash
claude
```

On first launch, Claude Code will prompt you to log in. You can authenticate via:

**Option A — Browser Login (Recommended)**

Claude Code will open a browser window. Log in with your Anthropic / Claude.ai account. Your session is stored locally.

**Option B — API Key**

```bash
export ANTHROPIC_API_KEY=your_api_key_here
```

To make this permanent, add it to your shell profile:

```bash
# For bash
echo 'export ANTHROPIC_API_KEY=your_api_key_here' >> ~/.bashrc
source ~/.bashrc

# For zsh
echo 'export ANTHROPIC_API_KEY=your_api_key_here' >> ~/.zshrc
source ~/.zshrc
```

Get your API key at: [console.anthropic.com](https://console.anthropic.com)

### Step 3: Verify Setup

```bash
claude "Hello! Are you working?"
```

You should see Claude respond directly in your terminal. 🎉

### Step 4: Navigate to Your Project

```bash
cd /your/project/folder
claude
```

Claude Code automatically reads your project structure as context.

### Configuration File (Optional)

Create a `CLAUDE.md` file in your project root to give Claude persistent instructions:

```markdown
# CLAUDE.md

## Project: My Awesome App
- Stack: Next.js, TypeScript, Tailwind CSS, PostgreSQL
- Always write tests for new functions
- Use conventional commit messages
- Prefer functional components over class components
```

Claude reads this file every session automatically.

---

## 🚀 Chapter 3: Core Features

### 3.1 File Operations

Claude Code can read, create, and edit files directly:

```bash
claude "Read all the files in src/ and give me a summary of the architecture"
claude "Create a new file called utils/helpers.ts with date formatting utilities"
claude "Refactor auth.js to use async/await instead of callbacks"
```

### 3.2 Shell Command Execution

Claude can run terminal commands on your behalf:

```bash
claude "Install the required dependencies and start the dev server"
claude "Run the tests and fix any that are failing"
claude "Build the Docker image and show me the output"
```

> ⚠️ **Safety**: Claude will always ask for your confirmation before running potentially destructive commands (like `rm`, database resets, etc.)

### 3.3 Codebase Understanding

When you open Claude Code inside a project folder, it can:

- Map your entire file tree
- Understand imports and dependencies
- Trace function calls across files
- Identify patterns and anti-patterns

```bash
claude "Where is user authentication handled in this codebase?"
claude "Find all places where we make API calls and check for error handling"
```

### 3.4 Agentic / Autonomous Mode

For longer tasks, Claude Code works autonomously:

```bash
claude "Build me a REST API with Node.js and Express that has CRUD for a blog — with validation, error handling, and tests"
```

Claude will:
1. Plan the task
2. Create all necessary files
3. Write the code
4. Run tests
5. Fix errors automatically
6. Report back when done

### 3.5 Web Search (Real-Time Info)

Claude Code can search the internet mid-task:

```bash
claude "What's the latest version of React and what are the breaking changes? Update our package.json"
```

### 3.6 MCP (Model Context Protocol)

MCP lets Claude Code connect to external tools and services:

```bash
# Example MCP servers
- GitHub (read/write repos, PRs, issues)
- Postgres (query databases)
- Slack (send messages)
- Filesystem (advanced file ops)
- Brave Search (web search)
```

Configure MCP servers in your `~/.claude/claude_code_config.json`:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your_token"
      }
    }
  }
}
```

### 3.7 Multi-File Context Window

Claude Code reads your full project — not just one file. When working on a bug, you can say:

```bash
claude "The login is broken. Check auth.js, middleware/session.js, and routes/user.js and fix it"
```

### 3.8 Git Integration

```bash
claude "Commit all my changes with a proper conventional commit message"
claude "Review the diff and write a PR description"
claude "Check the git log and summarize what changed in the last week"
```

---

## 💬 Chapter 4: How to Write Great Prompts

Prompting Claude Code is different from prompting a chatbot. Because it has **agency** (it can take actions), clarity and structure matter more.

### The Golden Rules

#### ✅ Rule 1: Be Specific About What You Want

**Bad:**
```
fix the bug
```

**Good:**
```
The login form throws "Cannot read property 'id' of undefined" when the user submits with an empty email. Fix it in src/components/LoginForm.tsx
```

---

#### ✅ Rule 2: Provide Context

**Bad:**
```
add authentication
```

**Good:**
```
Add JWT-based authentication to this Express app. Use the existing User model in models/User.js. Store tokens in HTTP-only cookies. Protect all routes under /api/dashboard
```

---

#### ✅ Rule 3: Define Constraints

```
Refactor the database queries in db/queries.js to use prepared statements.
Constraints:
- Do NOT change the function signatures (they're used in 20+ places)
- Keep backward compatibility
- Use the existing `pg` library, don't add new deps
```

---

#### ✅ Rule 4: Specify Output Format

```
Analyze the performance issues in this React app and give me:
1. A list of the top 3 bottlenecks
2. The specific files and line numbers
3. Code snippets showing the fix for each
```

---

#### ✅ Rule 5: Use Step-by-Step for Complex Tasks

```
Do the following in order:
1. Read package.json and identify outdated dependencies
2. Check the changelog for any breaking changes
3. Update only the safe ones (patch and minor versions)
4. Run npm test to confirm nothing broke
5. Show me a summary of what was updated
```

---

### Prompt Templates

#### 🔧 Bug Fix Template
```
Bug: [Describe the bug and the error message]
File(s): [Which files are involved]
Expected behavior: [What should happen]
Actual behavior: [What is happening]

Please find the root cause and fix it.
```

#### 🏗️ Feature Build Template
```
Feature: [Name of the feature]
Stack: [Your tech stack]
Requirements:
- [Requirement 1]
- [Requirement 2]
Constraints:
- [Don't change X]
- [Must integrate with Y]
Tests: Yes/No
```

#### 🔍 Code Review Template
```
Review the code in [file/folder] and check for:
- Security vulnerabilities
- Performance issues
- Code smells or anti-patterns
- Missing error handling
Output: Bullet list with file + line number + recommendation
```

#### 📝 Documentation Template
```
Generate JSDoc comments for all exported functions in [file].
Use this format:
- @param with types
- @returns with type and description
- @example with a real usage example
```

---

### Anti-Patterns to Avoid

| ❌ Don't Do This | ✅ Do This Instead |
|-----------------|------------------|
| "Fix my code" | "Fix the null pointer error in auth.js line 42" |
| "Make it faster" | "Optimize the SQL query in getUserOrders() — it's causing 3s load times" |
| "Add tests" | "Add Jest unit tests for all functions in utils/validation.js" |
| Vague scope | Specify exact files, functions, and expected outcomes |

---

## 🦙 Chapter 5: Claude Code + Ollama

> Run **local AI models** with Claude Code for privacy, offline use, or cost savings.

### What is Ollama?

[Ollama](https://ollama.com) is a tool that lets you run large language models (LLMs) locally on your machine. Combined with Claude Code, you can route requests to local models like **Llama 3**, **Mistral**, **DeepSeek**, and more.

### Why Use Ollama with Claude Code?

- 🔒 **Privacy**: Code never leaves your machine
- 💸 **Cost**: No API credits used
- ✈️ **Offline**: Works without internet
- 🧪 **Experimentation**: Test different open-source models

---

### Step 1: Install Ollama

**macOS / Linux:**
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Windows:**
Download the installer from [ollama.com/download](https://ollama.com/download)

Verify:
```bash
ollama --version
```

### Step 2: Pull a Model

```bash
# Recommended models for coding tasks
ollama pull llama3.1        # General purpose, strong coding
ollama pull deepseek-coder  # Specialized for code
ollama pull mistral         # Fast and efficient
ollama pull codellama       # Meta's coding model
```

Check available models:
```bash
ollama list
```

### Step 3: Start Ollama Server

```bash
ollama serve
```

The server runs at `http://localhost:11434` by default.

### Step 4: Configure Claude Code to Use Ollama

Set these environment variables before launching Claude Code:

```bash
export ANTHROPIC_BASE_URL=http://localhost:11434/v1
export ANTHROPIC_API_KEY=ollama   # Any non-empty string works
```

Then launch Claude Code and specify the model:

```bash
claude --model llama3.1
```

Or set a permanent default in your config:

```json
// ~/.claude/claude_code_config.json
{
  "model": "llama3.1",
  "baseURL": "http://localhost:11434/v1"
}
```

### Step 5: Verify It's Working

```bash
claude "What model are you running on?"
```

---

### Model Recommendations by Task

| Task | Recommended Model |
|------|-----------------|
| General coding | `llama3.1:8b` or `llama3.1:70b` |
| Code generation | `deepseek-coder:6.7b` |
| Fast responses | `mistral:7b` |
| Code completion | `codellama:13b` |
| Complex reasoning | `llama3.1:70b` (needs 48GB+ RAM) |

---

### Switching Between Anthropic and Ollama

Create shell aliases for easy switching:

```bash
# Add to ~/.bashrc or ~/.zshrc

# Use Anthropic Claude (cloud)
alias claude-cloud='unset ANTHROPIC_BASE_URL && claude'

# Use Ollama (local)
alias claude-local='ANTHROPIC_BASE_URL=http://localhost:11434/v1 ANTHROPIC_API_KEY=ollama claude --model llama3.1'
```

---

### Full Ollama + Claude Code Repo

For a complete working setup with more configuration options, see my dedicated repo:

> 🔗 **[abubakarzohaib141/ollama_with_claude_code](https://github.com/abubakarzohaib141/ollama_with_claude_code)**

---

## 🏗️ Chapter 6: Real-World Workflows

### Workflow 1: Build a Full-Stack App

```bash
cd ~/projects
mkdir my-app && cd my-app
claude "Build a full-stack todo app with:
- Backend: Node.js + Express + SQLite
- Frontend: Vanilla HTML/CSS/JS
- Features: Add, complete, delete todos
- Include a README with setup instructions"
```

### Workflow 2: Automated Code Review

```bash
# Before every PR
claude "Review all changes in the current git diff.
Check for: security issues, missing error handling, bad variable names, missing tests.
Format output as a markdown table with: File | Line | Issue | Severity | Suggested Fix"
```

### Workflow 3: Legacy Codebase Modernization

```bash
claude "This codebase uses callbacks everywhere. 
Refactor all async operations in src/ to use async/await.
Do it file by file, run the tests after each file, and stop if tests fail."
```

### Workflow 4: Auto-Documentation

```bash
claude "Go through every .js file in src/ and:
1. Add JSDoc comments to all exported functions
2. Generate a DOCS.md file with a full API reference
3. Add usage examples for each function"
```

### Workflow 5: Debugging Session

```bash
claude "The app crashes with: 'TypeError: Cannot read properties of null (reading map)' 
when I visit /dashboard after logging in as a new user.
Trace the issue through the codebase and fix it."
```

---

## 💡 Chapter 7: Tips, Tricks & Best Practices

### 🧠 Power User Tips

**1. Use CLAUDE.md as Your Project Brain**
```markdown
# CLAUDE.md
- Never use `var`, always `const`/`let`
- All API responses must be typed with TypeScript interfaces
- Write tests in Vitest, not Jest
- Database: PostgreSQL via Prisma ORM
```

**2. Interrupt and Redirect**
Press `Ctrl+C` to stop Claude mid-task and give new instructions. Claude remembers the context.

**3. Ask Claude to Explain Its Plan First**
```bash
claude "Before doing anything, show me your plan for adding OAuth to this app"
```

**4. Use `/clear` to Reset Context**
When switching tasks:
```bash
/clear
```

**5. Keep Sessions Focused**
One task per session works better than mixing unrelated requests.

**6. Trust but Verify**
Always review file changes before committing:
```bash
git diff
```

---

### 🚫 Common Mistakes

| Mistake | Fix |
|---------|-----|
| Letting Claude run without reviewing | Use `--no-auto-approve` for sensitive tasks |
| No `CLAUDE.md` | Add project conventions file |
| Vague prompts | Be specific: files, functions, expected behavior |
| Not using git | Always have a clean git state before big tasks |
| Mixing tasks in one session | `/clear` between unrelated tasks |

---

### ⚡ Useful Commands Reference

```bash
claude                        # Start interactive session
claude "your prompt"          # One-shot command
claude --model claude-opus-4  # Specify model
claude --no-auto-approve      # Manual approval mode
/clear                        # Clear context
/help                         # Show available commands
/status                       # Check connection status
```

---

## 📦 Chapter 8: Resources & Community

### Official Resources

- 📖 [Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code)
- 🔑 [Anthropic Console](https://console.anthropic.com)
- 🤖 [Claude.ai](https://claude.ai)
- 📦 [npm: @anthropic-ai/claude-code](https://www.npmjs.com/package/@anthropic-ai/claude-code)

### Related Repos

- 🦙 **[ollama_with_claude_code](https://github.com/abubakarzohaib141/ollama_with_claude_code)** — Full guide on running Claude Code with local Ollama models
- 🔧 [MCP Servers](https://github.com/modelcontextprotocol/servers) — Official MCP server implementations

### Ollama Resources

- 🦙 [Ollama Official Site](https://ollama.com)
- 📦 [Ollama Model Library](https://ollama.com/library)
- 💻 [Ollama GitHub](https://github.com/ollama/ollama)

---

## 🤝 Contributing

Contributions are welcome! If you have:

- Better prompt templates
- New workflow examples
- Bug fixes or corrections
- Translations

Please open a PR or Issue. Let's make this the best Claude Code resource out there.

```bash
# To contribute:
git clone https://github.com/your-username/claude-code-complete-course
cd claude-code-complete-course
# Make your changes
git checkout -b feature/your-improvement
git commit -m "feat: add X example"
git push origin feature/your-improvement
# Open a PR!
```

---

## 📄 License

MIT License — free to use, share, and modify.

---

<div align="center">

**Made with ❤️ by [Abubakar Zohaib](https://github.com/abubakarzohaib141)**

*If this helped you, give it a ⭐ on GitHub!*

</div>
