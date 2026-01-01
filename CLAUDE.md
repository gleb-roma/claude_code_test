# CLAUDE.md - AI Assistant Guide

This document provides comprehensive guidance for AI assistants working with this codebase.

## Repository Overview

This is a **Trading Strategy Bot** repository that executes trading logic and logs results. The bot is designed to run via GitHub Actions with manual triggering.

### Purpose
- Test repository for mobile-based code development
- Trading strategy automation framework
- Automated trade execution and logging

## Codebase Structure

```
claude_code_test/
├── .github/
│   └── workflows/
│       └── trading_bot.yml      # GitHub Actions workflow for trading automation
├── trading_strategy.py          # Main trading strategy implementation
├── trade_log.txt               # Trade execution log (auto-updated)
├── requirements.txt            # Python dependencies
└── README.md                   # Project description
```

### Core Files

#### `trading_strategy.py`
- **Purpose**: Main entry point for trading strategy execution
- **Key Function**: `run_trading_strategy()` - Executes trading logic and logs results
- **Output**: Appends trade execution timestamps to `trade_log.txt`
- **Location**: Root directory
- **Line Numbers**: 17 lines total

#### `.github/workflows/trading_bot.yml`
- **Purpose**: GitHub Actions workflow for automated trading
- **Trigger**: Manual dispatch only (`workflow_dispatch`)
- **Python Version**: 3.11
- **Permissions**: `contents: write` (for committing trade logs)
- **Environment Variables**:
  - `ANTHROPIC_API_KEY`: Required for Claude API access
  - Additional trading API keys can be added as needed
- **Workflow Steps**:
  1. Checkout code
  2. Set up Python 3.11
  3. Install dependencies
  4. Run trading strategy
  5. Auto-commit and push trade log updates

#### `trade_log.txt`
- **Purpose**: Persistent log of trade executions
- **Format**: Timestamped entries ("Trade executed at {datetime}")
- **Updates**: Automatically appended by `trading_strategy.py`
- **Commits**: Auto-committed by GitHub Actions workflow

#### `requirements.txt`
- **Status**: Currently empty
- **Purpose**: Python package dependencies
- **Usage**: Install via `pip install -r requirements.txt`

## Development Workflows

### Git Branching Strategy

**Branch Naming Convention:**
- Feature branches MUST start with `claude/`
- Format: `claude/{feature-description}-{session-id}`
- Example: `claude/add-claude-documentation-H8uke`

**Critical Git Rules:**
1. Always develop on designated feature branches
2. Never push to branches without `claude/` prefix (will fail with 403)
3. Use `git push -u origin <branch-name>` for pushing
4. Retry failed pushes up to 4 times with exponential backoff (2s, 4s, 8s, 16s)

### Commit Conventions

- Use clear, descriptive commit messages
- Examples from history:
  - "Update trade log"
  - "fixing error code 128"
  - "added reqs"
  - "added gh action and main file"

### GitHub Actions Usage

**Manual Triggering:**
- Workflow runs only via manual dispatch
- No scheduled or push-based triggers
- Requires GitHub UI or API invocation

**Required Secrets:**
- `ANTHROPIC_API_KEY`: For Claude API integration
- `GITHUB_TOKEN`: Auto-provided by GitHub Actions

## Key Conventions

### Python Development

1. **Style**: Standard Python conventions
2. **Entry Point**: `if __name__ == "__main__":` pattern used
3. **Logging**: File-based logging to `trade_log.txt`
4. **Datetime**: Uses `datetime.now()` for timestamps

### File Operations

1. **Trade Logs**: Always append to `trade_log.txt`, never overwrite
2. **Auto-commits**: GitHub Actions auto-commits trade log updates
3. **File Paths**: Use relative paths for trade_log.txt

### Environment Variables

Required environment variables:
- `ANTHROPIC_API_KEY`: Claude API access (set in GitHub Secrets)
- Add trading API credentials as needed

## Common Tasks

### Running the Trading Strategy Locally

```bash
python trading_strategy.py
```

### Installing Dependencies

```bash
pip install -r requirements.txt
```

### Manual Workflow Trigger

Via GitHub CLI:
```bash
gh workflow run trading_bot.yml
```

Via GitHub UI:
- Navigate to Actions tab
- Select "Trading Strategy Bot"
- Click "Run workflow"

### Viewing Trade Logs

```bash
cat trade_log.txt
```

## Implementation Guidelines for AI Assistants

### When Making Changes

1. **Read Before Editing**: Always read files before modifying them
2. **Test Locally**: Test Python changes before committing
3. **Update Dependencies**: If adding imports, update `requirements.txt`
4. **Maintain Logging**: Ensure all trades are logged to `trade_log.txt`
5. **Git Workflow**:
   - Develop on `claude/` branches
   - Commit with clear messages
   - Push to designated branch

### Code Quality Standards

1. **No Over-Engineering**: Keep solutions simple and focused
2. **Security**: Avoid command injection, validate external inputs
3. **Error Handling**: Add only where necessary (external APIs, user input)
4. **Comments**: Add only where logic isn't self-evident
5. **Backward Compatibility**: Remove unused code completely

### Trading Strategy Development

When extending `trading_strategy.py`:
1. Maintain the logging pattern
2. Use appropriate error handling for API calls
3. Keep datetime format consistent
4. Ensure GitHub Actions can execute the code
5. Test with API keys in environment variables

### Documentation Updates

When making significant changes:
1. Update this CLAUDE.md file
2. Update README.md if user-facing
3. Document new environment variables
4. Update workflow if GitHub Actions changes needed

## Security Considerations

1. **API Keys**: Never commit API keys to repository
2. **Secrets Management**: Use GitHub Secrets for sensitive data
3. **Input Validation**: Validate external data (API responses, user input)
4. **Dependencies**: Keep requirements.txt updated and minimal

## Debugging

### Common Issues

1. **GitHub Actions 403 Error**: Branch name doesn't follow `claude/` convention
2. **Import Errors**: Missing dependencies in `requirements.txt`
3. **API Failures**: Check `ANTHROPIC_API_KEY` in GitHub Secrets
4. **Git Push Failures**: Retry with exponential backoff (network issues)

### Log Locations

- Trade execution: `trade_log.txt`
- GitHub Actions: Actions tab in GitHub UI
- Git operations: Local git logs

## Architecture Decisions

### Why GitHub Actions?
- Serverless execution
- Built-in secrets management
- Auto-commit capabilities
- Manual control over execution

### Why File-Based Logging?
- Simple persistence
- Git-tracked history
- No external database needed
- Easy to review and audit

### Why Manual Workflow Dispatch?
- Controlled execution timing
- Prevents accidental automated trading
- Explicit user intent required

## Current State (2026-01-01)

- **Last Trade**: 2026-01-01 17:05:29
- **Active Branch**: `claude/add-claude-documentation-H8uke`
- **Python Version**: 3.11
- **Dependencies**: None (requirements.txt empty)
- **Recent Changes**: Trade log updates, workflow fixes

## Future Considerations

Areas for potential expansion:
1. Add actual trading logic (currently placeholder)
2. Integrate with trading APIs
3. Add data analysis and reporting
4. Implement backtesting capabilities
5. Add error notifications
6. Expand logging with trade details (prices, quantities, etc.)

---

**Last Updated**: 2026-01-01
**Maintained By**: AI Assistants (Claude)
**Repository**: gleb-roma/claude_code_test
