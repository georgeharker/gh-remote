# gh-remote Installation Guide

## Quick Start

### 1. Install the extension locally

From the `gh-remote` directory:

```bash
cd gh-remote
gh extension install .
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

## Installation from GitHub (after publishing)

Once you publish this extension to GitHub, users can install it with:

```bash
gh extension install <your-username>/gh-remote
```

## Publishing Steps

To publish this extension to GitHub:

1. Create a new repository on GitHub named `gh-remote`

2. Add the remote and push:

```bash
cd gh-remote
git add .
git commit -m "Initial commit: gh-remote extension v1.0.0"
git remote add origin git@github.com:<your-username>/gh-remote.git
git branch -M main
git push -u origin main
```

3. Users can then install with:

```bash
gh extension install <your-username>/gh-remote
```

## Uninstalling

```bash
gh extension remove remotes
```

## Upgrading

```bash
gh extension upgrade remotes
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

# Reinstall
cd gh-remote
gh extension install . --force
```

### Permission denied

```bash
# Ensure the script is executable
chmod +x gh-remote
```

### gh: command not found

Install GitHub CLI from: https://cli.github.com/

