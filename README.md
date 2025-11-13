# CommitAgent

AI-powered Git commit message generator using Claude AI.

## Overview

CommitAgent is a CLI tool that uses Claude AI to generate intelligent, context-aware commit messages based on your staged changes. It analyzes your git status and diff, generates a commit message, and lets you edit it before committing.

## Features

- 🤖 AI-generated commit messages using Claude
- ✏️ Interactive editing before committing
- 📝 Custom commit specifications/guidelines
- ✍️ Optional automatic Signed-off-by line
- ⚙️ Simple configuration management

## Installation

### Prerequisites

1. **Python 3.8+**
2. **Git** - Must be installed and in PATH
3. **Claude CLI** - Install from [Claude Code documentation](https://docs.claude.com/en/docs/claude-code)

### Install CommitAgent

```bash
pip install commitagent
```

Or install from source:

```bash
git clone https://github.com/yourusername/commitagent.git
cd commitagent
pip install -e .
```

## Usage

### Generate a Commit Message

Navigate to your git repository and run:

```bash
commitagent
```

This will:
1. Check if you're in a git repository
2. Verify Claude CLI is installed
3. Install the `/commitagent` command if needed
4. Generate a commit message using Claude AI
5. Open your editor to review/edit the message
6. Create the git commit

### Configuration

#### Set Commit Specification

Define custom guidelines for how Claude should generate commit messages:

```bash
commitagent config set commit-spec "Use conventional commits format with type(scope): description"
```

#### Enable Auto Sign-off

Automatically add a `Signed-off-by` line to commits:

```bash
commitagent config set auto-signoff enabled
```

To disable:

```bash
commitagent config set auto-signoff disabled
```

#### View Configuration

View all configuration:

```bash
commitagent config view
```

View specific configuration:

```bash
commitagent config view commit-spec
```

### Help

Display help information:

```bash
commitagent help
```

## Configuration Keys

| Key | Type | Description |
|-----|------|-------------|
| `commit-spec` | string | Custom commit message specification/guidelines for Claude |
| `auto-signoff` | enabled/disabled | Automatically add Signed-off-by line to commits |

## How It Works

1. **Validation**: CommitAgent checks that you're in a git repository and that required tools (git, claude) are installed

2. **Command Installation**: If the `/commitagent` Claude command doesn't exist, it's automatically downloaded and installed to `~/.claude/commands/`

3. **AI Generation**: Claude analyzes your git status and diff to generate a contextual commit message, using your custom `commit-spec` if configured

4. **Interactive Editing**: The generated message opens in your preferred editor (`$EDITOR` or `$VISUAL`, defaults to vim)

5. **Commit**: After you save and close the editor, CommitAgent creates the git commit with your message (and optional sign-off)

## Environment Variables

- `EDITOR` or `VISUAL` - Preferred text editor (defaults to vim)
- `COMMITAGENT_SPEC` - Commit specification (set automatically from config)

## File Locations

- Configuration: `~/.config/commitagent/config.json`
- Claude command: `~/.claude/commands/commitagent.md`
- Temporary edit file: `.git/COMMIT_EDITMSG_*.txt`

## Examples

### Basic Usage

```bash
# Stage your changes
git add .

# Generate and create commit
commitagent
```

### With Custom Specification

```bash
# Set your commit style
commitagent config set commit-spec "
- Use conventional commits (feat:, fix:, docs:, etc.)
- Keep first line under 72 characters
- Include ticket number if available
- Add detailed explanation in commit body
"

# Generate commits following your specification
commitagent
```

### With Auto Sign-off

```bash
# Enable sign-off
commitagent config set auto-signoff enabled

# All commits will include Signed-off-by line
commitagent
```

## Troubleshooting

### Claude CLI not found

Install Claude CLI from the [official documentation](https://docs.claude.com/en/docs/claude-code).

### Not in a git repository

Ensure you're running `commitagent` from within a git repository:

```bash
git rev-parse --git-dir
```

### Editor not opening

Set your preferred editor:

```bash
export EDITOR=nano  # or vim, emacs, code --wait, etc.
```

## Development

### Setup Development Environment

```bash
# Clone repository
git clone https://github.com/yourusername/commitagent.git
cd commitagent

# Install in editable mode
pip install -e .
```

### Project Structure

```
commitagent/
├── src/
│   └── commitagent/
│       ├── __init__.py      # Package initialization
│       ├── cli.py           # CLI entry point and argument parsing
│       ├── config.py        # Configuration management
│       └── workflow.py      # Main workflow logic
├── pyproject.toml           # Package configuration
└── README.md               # This file
```

## License

MIT License - See LICENSE file for details

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- Built with [Claude AI](https://claude.ai)
- Powered by [Claude CLI](https://docs.claude.com/en/docs/claude-code)
