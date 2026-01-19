# gh-remote Installation Guide

> **GitHub Repository**: https://github.com/georgeharker/gh-remote

## Quick Start

### 1. Install from GitHub (Recommended)

```bash
gh extension install georgeharker/gh-remote
```

### 2. Verify installation

```bash
gh remote --version
# Should output: gh-remote v1.0.0

gh remote --help
# Shows full help text
```

### 3. Test it out

```bash
# Create a new private repository
gh remote new my-project --private

# Or set an existing repository as origin
gh remote set octocat/hello-world
```

## Installation from Local Directory (for development)

### 1. Clone the repository

```bash
git clone https://github.com/georgeharker/gh-remote.git
cd gh-remote
```

### 2. Install locally

```bash
gh extension install .
```

## Uninstalling

```bash
gh extension remove remote
```

## Upgrading

```bash
gh extension upgrade georgeharker/gh-remote
# Or upgrade all extensions:
gh extension upgrade --all
```

## Development Workflow

### Making changes

1. Edit the `gh-remote` script
2. Test changes:
   ```bash
   ./gh-remote --help
   ```
3. Reinstall to test as extension:
   ```bash
   gh extension install . --force
   gh remote --help
   ```

### Debugging

Add `set -x` at the top of the `gh-remote` script to enable debug output:

```bash
#!/usr/bin/env bash
set -x  # Debug mode
set -e
```

## Requirements Check

Before using, ensure you have:

```bash
# Check gh CLI
gh --version
# Should be >= 2.0.0

# Check authentication
gh auth status
# Should show: Logged in to github.com

# Check git
git --version
```

## Troubleshooting

### Extension not found after installation

```bash
# List installed extensions
gh extension list

# Reinstall from GitHub
gh extension remove remote
gh extension install georgeharker/gh-remote
```

### Permission denied

```bash
# Ensure the script is executable
chmod +x gh-remote
```

### gh: command not found

Install GitHub CLI from: https://cli.github.com/

