# gh-remote

> **GitHub Repository**: https://github.com/georgeharker/gh-remote

A GitHub CLI extension that simplifies repository creation and git remote management with subcommands.

## Features

- **Create new repositories** with `gh remote new` - automatic remote setup
- **Set existing repositories** with `gh remote set` - supports user/repo format and full URLs
- **Automatic fork detection** - sets up both `origin` and `upstream` remotes for forks
- **Smart git initialization** - creates a git repo if one doesn't exist
- **SSH URL support** - uses SSH URLs for secure git operations
- **Multiple repository formats** - accepts user/repo, HTTPS URLs, and SSH URLs

## Installation

### Prerequisites

- [GitHub CLI (`gh`)](https://cli.github.com/) - version 2.0 or higher
- Git

### Install the extension

```bash
gh extension install georgeharker/gh-remote
```

### Install from local directory (for development)

```bash
git clone https://github.com/georgeharker/gh-remote.git
cd gh-remote
gh extension install .
```

### Uninstall

```bash
gh extension remove remote
```

## Usage

### Create a new repository

```bash
# Create a new private repository (default)
gh remote new my-project

# Create a new public repository
gh remote new my-project --public

# Create in a different directory
gh remote new my-project --directory ~/projects/my-app
```

### Set an existing repository as origin

```bash
# Using user/repo format
gh remote set octocat/hello-world

# Using HTTPS URL
gh remote set https://github.com/octocat/hello-world

# Using SSH URL
gh remote set git@github.com:octocat/hello-world.git

# Work in a different directory
gh remote set octocat/hello-world --directory ~/projects/existing-app
```

### Show help

```bash
gh remote --help
gh remote -h
```

### Show version

```bash
gh remote --version
gh remote -v
```

## Command Reference

### `gh remote new <repo>`

Creates a new GitHub repository and sets it as the git remote origin.

**Arguments:**
- `<repo>` - Name for the new repository (will be created under your account)

**Options:**
- `--public` - Create a public repository
- `--private` - Create a private repository (default)
- `--directory <path>` - Work in the specified directory

**Examples:**
```bash
gh remote new awesome-project
gh remote new awesome-project --public
gh remote new awesome-project --directory ~/dev/projects
```

### `gh remote set <repo>`

Sets an existing GitHub repository as the git remote origin. Automatically detects forks and sets upstream.

**Arguments:**
- `<repo>` - Repository identifier in one of these formats:
  - `user/repo` - GitHub user/repo format
  - `https://github.com/user/repo` - HTTPS URL
  - `git@github.com:user/repo.git` - SSH URL

**Options:**
- `--directory <path>` - Work in the specified directory

**Examples:**
```bash
# Regular repository
gh remote set octocat/hello-world

# Forked repository (automatically sets upstream)
gh remote set myusername/forked-repo

# Using full URL
gh remote set https://github.com/octocat/Spoon-Knife

# In different directory
gh remote set octocat/hello-world --directory ~/projects/test
```

## How It Works

### Creating a New Repository (`gh remote new`)

1. Creates the repository using `gh repo create`
2. Retrieves the SSH URL for the new repository
3. Initializes git if needed
4. Sets the git remote `origin` to the new repository

### Setting an Existing Repository (`gh remote set`)

1. Parses the repository identifier (supports multiple formats)
2. Fetches repository information using `gh repo view`
3. Detects if the repository is a fork
4. Initializes git if needed
5. Sets `origin` to your selected repository
6. If it's a fork, also sets `upstream` to the parent repository

## Examples

### Example 1: Create a new private repository

```bash
$ gh remote new my-awesome-project
ℹ Creating repository: my-awesome-project
ℹ Creating repository...
✓ Created repository: myusername/my-awesome-project
ℹ Not a git repository. Initializing...
✓ Initialized git repository in .
✓ Set remote 'origin' to git@github.com:myusername/my-awesome-project.git

ℹ Current remotes:
origin  git@github.com:myusername/my-awesome-project.git (fetch)
origin  git@github.com:myusername/my-awesome-project.git (push)

✓ Done!
```

### Example 2: Set an existing forked repository

```bash
$ gh remote set myusername/open-source-project
ℹ Setting remote for repository: myusername/open-source-project
ℹ This is a fork of original-owner/open-source-project
ℹ Git repository already exists
✓ Set remote 'origin' to git@github.com:myusername/open-source-project.git
✓ Set remote 'upstream' to git@github.com:original-owner/open-source-project.git

ℹ Current remotes:
origin    git@github.com:myusername/open-source-project.git (fetch)
origin    git@github.com:myusername/open-source-project.git (push)
upstream  git@github.com:original-owner/open-source-project.git (fetch)
upstream  git@github.com:original-owner/open-source-project.git (push)

✓ Done!
```

### Example 3: Set repository using full URL

```bash
$ gh remote set https://github.com/octocat/Hello-World
ℹ Setting remote for repository: octocat/Hello-World
ℹ Not a git repository. Initializing...
✓ Initialized git repository in .
✓ Set remote 'origin' to git@github.com:octocat/Hello-World.git

ℹ Current remotes:
origin  git@github.com:octocat/Hello-World.git (fetch)
origin  git@github.com:octocat/Hello-World.git (push)

✓ Done!
```

## Requirements

- **gh CLI**: The GitHub command-line tool must be installed and authenticated
  ```bash
  gh auth login
  ```

- **git**: Must be installed for repository operations

## Troubleshooting

### "gh: command not found"

Install the GitHub CLI from https://cli.github.com/

### "Not authenticated with GitHub"

Run `gh auth login` to authenticate with your GitHub account.

### Remote already exists

If a remote named `origin` or `upstream` already exists, you'll be prompted whether to replace it.

### "Failed to get repository information"

Make sure:
- The repository exists
- You have access to the repository
- The repository identifier is in the correct format

## Development

### Structure

```
gh-remote/
├── gh-remote           # Main executable script
├── README.md           # This file
├── INSTALL.md          # Installation guide
├── LICENSE             # MIT License
└── .gitignore          # Git ignores
```

### Testing locally

```bash
# Install the extension locally
cd gh-remote
gh extension install .

# Test commands
gh remote --help
gh remote new test-repo
gh remote set octocat/hello-world
```

### Uninstalling

```bash
gh extension remove remote
```

## Uninstallation

To completely remove the extension:

```bash
gh extension remove remote
```

This will remove the extension from your system. Your git repositories and remotes will not be affected.

## License

MIT License - See LICENSE file for details

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Roadmap

Future features to consider:

- [ ] Support for multiple remote names (not just origin/upstream)
- [ ] Clone repository after setting up remotes
- [ ] Support for repository templates
- [ ] Interactive mode for selecting from user's repositories
- [ ] Configuration file for default settings
- [ ] Support for GitHub Enterprise

## Author

Created with ❤️ for the GitHub CLI community
