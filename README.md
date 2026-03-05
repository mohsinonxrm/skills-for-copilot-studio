# Copilot Studio Plugin for Claude Code

A **Claude Code plugin** for Microsoft Copilot Studio YAML authoring. Create, edit, validate, and test Copilot Studio agents using YAML files — from any project directory.

## Installation

### From a local clone (development / testing)

```bash
# One-off session — load the plugin without installing
claude --plugin-dir /path/to/copilot-studio

# Or install persistently (available in every project)
claude plugin install /path/to/copilot-studio --scope user
```

### From a marketplace (when published)

```bash
claude plugin install copilot-studio
```

Once installed, the plugin is available globally — no need to `cd` into this repo.

## Quick Start — End-to-End Example

Suppose you cloned a Copilot Studio agent to `C:\Users\you\CopilotStudio\MyAgent1`:

```bash
# 1. Start Claude Code in your agent's directory
cd C:\Users\you\CopilotStudio\MyAgent1
claude --plugin-dir C:\Users\you\ClaudeCodeProj\agents-build-agents

# 2. Ask the author agent to create a topic
@copilot-studio:author Create a FAQ topic that answers questions about our return policy

# 3. Validate it
/copilot-studio:validate topics/ReturnPolicy.topic.mcs.yml

# 4. List all topics
/copilot-studio:list-topics

# 5. After pushing & publishing in Copilot Studio, test it
/copilot-studio:chat-with-agent What is your return policy?
```

That's it. The plugin auto-discovers your agent's YAML files via `**/agent.mcs.yml`.

## Three Specialized Agents

The plugin provides three named agents so it doesn't interfere with unrelated projects:

| Agent | Use When | Invoke |
|-------|----------|--------|
| **author** | Building or modifying YAML files (topics, actions, knowledge, etc.) | `@copilot-studio:author` |
| **test** | Testing published agents, analyzing failures | `@copilot-studio:test` |
| **troubleshoot** | Debugging issues — wrong topic triggered, validation errors | `@copilot-studio:troubleshoot` |

## Skills (Slash Commands)

All skills are individually invocable via `/copilot-studio:<skill-name>`:

| Skill | Description |
|-------|-------------|
| `/copilot-studio:new-topic` | Create a new topic |
| `/copilot-studio:add-node` | Add or modify nodes in a topic |
| `/copilot-studio:add-action` | Add a connector action (Teams, Outlook, etc.) |
| `/copilot-studio:validate` | Validate YAML structure |
| `/copilot-studio:add-knowledge` | Add knowledge source (public website or SharePoint) |
| `/copilot-studio:list-topics` | List all topics in the agent |
| `/copilot-studio:list-kinds` | List available YAML kind values |
| `/copilot-studio:edit-agent` | Edit agent settings or instructions |
| `/copilot-studio:edit-triggers` | Modify topic triggers |
| `/copilot-studio:add-child-agent` | Add/configure child agents |
| `/copilot-studio:add-generative-answers` | Add generative answer nodes |
| `/copilot-studio:add-global-variable` | Add a global variable |
| `/copilot-studio:run-tests` | Run tests and analyze failures |
| `/copilot-studio:chat-with-agent` | Send a test message to a published agent |
| `/copilot-studio:best-practices` | Best practices (glossary, user context) |
| `/copilot-studio:lookup-schema` | Query schema definitions |

## Prerequisites

- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) installed
- [Python 3.8+](https://www.python.org/) with `pip install pyyaml`
- [VS Code](https://code.visualstudio.com/) with the [Copilot Studio Extension](https://github.com/microsoft/vscode-copilotstudio)

## Workflow

1. **Clone** the agent with the Copilot Studio VS Code Extension into any directory
2. **Start Claude Code** in that directory with the plugin loaded
3. **Author** changes in YAML using the `@copilot-studio:author` agent or skills
4. **Push** changes with the VS Code Extension (creates a draft)
5. **Publish** in Copilot Studio UI (makes changes live)
6. **Test** with `/copilot-studio:chat-with-agent` or `/copilot-studio:run-tests`

## Plugin Management

```bash
# Install persistently (user-wide)
claude plugin install /path/to/copilot-studio --scope user

# Install for a specific project (shared via version control)
claude plugin install /path/to/copilot-studio --scope project

# Check installed plugins
claude plugin list

# Temporarily disable without uninstalling
claude plugin disable copilot-studio

# Re-enable
claude plugin enable copilot-studio

# Uninstall
claude plugin uninstall copilot-studio
```

## Key Resources

- [SETUP_GUIDE.md](SETUP_GUIDE.md) — Detailed step-by-step setup and testing guide
- `skills/_project-context/SKILL.md` — Project conventions
- `skills/_reference/SKILL.md` — YAML reference tables (triggers, actions, variables, Power Fx)
