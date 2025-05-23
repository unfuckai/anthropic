# Claude Code Summit Tips & Tricks
*May 22, 2025*

Notes from their live streams on YouTube.
https://www.youtube.com/live/6eBSHbLKuN0?si=blXAiSOdbTcpAeq1
https://www.youtube.com/live/nZCy8E5jlok?si=EyUHQBsoYEAZjPjE


## Optimizing Your Claude Code Setup

### Essential Commands
- `/terminal-setup` - Enable shift-enter to insert newlines
- `/theme` - Set light/dark mode; consider vulcanize theme
- `/install-github-app` - Allows you to @claude on Github issues & PRs
- `/allowed-tools` - Customize tool permissions to avoid repeated prompts
- `/config` - Turn on notifications

### macOS Enhancement
Enable macOS dictation for voice-to-text prompting instead of typing.

## Getting Started with Claude Code

### Ask Questions About Your Codebase
- **History exploration:**
  - "Why does `foo` take so many arguments? Look through git history to answer."
  - "Why did we fix issue #123 by adding the if/else in @src/login.ts API?"
  - "Look at PR #456, then carefully verify which app versions were impacted."
  - "What did I ship last week?"

### Built-in Tools
- **bash** - Command execution
- **file search** - Find files and content
- **file listing** - Directory navigation
- **file read and write** - File operations
- **web fetch and search** - Internet access
- **TODOs** - Task management
- **sub-agents** - Parallel processing

## Steering Claude to Use Tools Your Way

### Think First Approach
Ask Claude to brainstorm before jumping into code:
- "Propose a few fixes for issue #123, then implement the one I pick."
- "Identify edge cases that are not covered in @my_test.rb then update the tests to cover these. Think hard."
- "commit, push, pr"
- "use 3 parallel agents to brainstorm ideas for how to clean up @slop.ts"

## Advanced Usage

### Custom Bash Tools
```bash
"Use the blarg CLI to check for error logs in the last test run. Use -h to check how to use it."
```

### MCP Tools Integration
```bash
$ claude mcp add blarg_server -- node myserver
"Use the blarg MCP server to check for error logs in the last test run."
```

## Common Workflows

### Explore → Plan → Confirm → Code → Commit
```
"Figure out the root cause for issue #123, then propose a few fixes. Let me choose an approach before you code. ultrathink"
```

### Write Tests → Commit → Code → Iterate → Commit
```
"Write tests for @utils/foo.ts to make sure links render properly (note the tests won't pass yet, since links aren't yet implemented). Then commit. Then update the code to make the tests pass."
```

### Write Code → Screenshot → Iterate
```
"Implement [mock.png]. Then screenshot it with Puppeteer and iterate until it looks like the mock."
```

> **Note:** When Claude has a way to check its work, it can iterate independently for much better results.

## Providing More Context

### Tips for Better Results
- More context = smarter Claude
- Take time to tune context
- Drag/drop or copy/paste images (multimodal support!)
- Use CLAUDE.md files
- Include files with @ references
- Define custom / commands
- **Pro Tip:** Type `#` to have Claude remember something

### CLAUDE.md File Hierarchy
```
/<enterprise root>/CLAUDE.md          # Shared across all projects
~/.claude/CLAUDE.md                   # Personal global settings
project-root/CLAUDE.md                # Project-specific (checked in)
project-root/CLAUDE.local.md          # Project-specific (not checked in)
project-root/a/CLAUDE.md              # Subdirectory-specific
```

### Custom Slash Commands
```
~/.claude/commands/foo.md             # /user:foo
project-root/.claude/commands/foo.md  # /project:foo
project-root/a/.claude/commands/foo.md # /project:a:foo
```

## Sharing Configs with Your Team

### Enterprise Policy (Shared)
- **Memory:** `/Library/ApplicationSupport/ClaudeCode/CLAUDE.md`
- **Permissions:** `/Library/ApplicationSupport/ClaudeCode/policies.json`

### Global Policy (Personal)
- **Memory:** `~/.claude/CLAUDE.md`
- **Slash Commands:** `~/.claude/commands/`
- **Permissions:** `~/.claude/settings.json`
- **MCP Servers:** `claude mcp`

### Project (Shared)
- **Memory:** `CLAUDE.md`
- **Slash Commands:** `.claude/commands/`
- **Permissions:** `.claude/settings.json`
- **MCP Servers:** `.mcp.json`

### Project (Personal)
- **Memory:** `CLAUDE.local.md`
- **Permissions:** `.claude/settings.local.json`
- **MCP Servers:** `claude mcp`

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Shift+Tab` | Enter auto-accept-edits mode |
| `#` | Create a memory |
| `!` | Enter bash command (Claude sees command + output) |
| `@` | Add file/folder to context |
| `Esc` | Stop Claude's current action |
| `Double-Esc` | Jump back in history (`--resume` to resume) |
| `Ctrl+R` | Verbose output |

### Useful Commands
- `/memory` - View all memory files being pulled in

#### SDK Example
- `claude -p` - Access Claude SDK (JavaScript/Python coming soon)

```bash
$ git status | claude -p "What are my changes?" --output-format=json | jq '.result'
```

## Advanced Tool Usage with Claude 4

### Parallel Tool Calling
> "For maximum efficiency, whenever you need to perform multiple independent operations, invoke all relevant tools simultaneously rather than sequentially."

### Thinking and Tool Use
> "After receiving tool results, carefully reflect on their quality and determine optimal next steps before proceeding. Use your thinking to plan and iterate based on this new information, and then take the best next action."

### Proactive Tool Triggering
> "Call the web search tool when: user asks about current events, factual information after January 2025, or any query requiring real-time data. Be proactive in identifying when searches would enhance your response."
