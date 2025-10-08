# Installation Guide

## Overview
This guide provides platform-specific installation and setup instructions for accessing and configuring the CCPR system across different Git platforms and operating systems.

## Prerequisites

### System Requirements
```yaml
Minimum Requirements:
  operating_system: "Windows 10+, macOS 10.14+, Linux (Ubuntu 18.04+)"
  memory: "4GB RAM"
  storage: "2GB available space"
  network: "Stable internet connection"
  
Recommended Requirements:
  operating_system: "Latest stable versions"
  memory: "8GB RAM or more"
  storage: "10GB available space"
  network: "High-speed broadband connection"
```

### Software Prerequisites
```yaml
Required Software:
  git: "2.25.0 or later"
  text_editor: "VS Code, Sublime Text, or similar"
  web_browser: "Chrome, Firefox, Safari, or Edge (latest versions)"
  
Optional but Recommended:
  git_gui: "GitHub Desktop, SourceTree, or similar"
  markdown_editor: "Typora, Mark Text, or editor with markdown support"
  terminal: "Windows Terminal, iTerm2, or enhanced terminal"
```

## Platform-Specific Installation

### GitHub Enterprise Setup

#### Prerequisites
- GitHub Enterprise account with appropriate permissions
- Organization membership with repository access
- Two-factor authentication enabled (if required)

#### Step 1: Install Git and GitHub CLI
```bash
# Windows (using winget)
winget install Git.Git
winget install GitHub.cli

# Windows (using chocolatey)
choco install git
choco install gh

# macOS (using Homebrew)
brew install git
brew install gh

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install git
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

#### Step 2: Authentication Setup
```bash
# Authenticate with GitHub
gh auth login

# Follow the interactive prompts:
# 1. Choose GitHub.com or GitHub Enterprise Server
# 2. Select HTTPS or SSH protocol
# 3. Authenticate via web browser or token
# 4. Choose Git credential helper

# Verify authentication
gh auth status
```

#### Step 3: Repository Access
```bash
# Clone the CCPR repository
gh repo clone organization/ccpr_root

# Or using git directly
git clone https://github.com/organization/ccpr_root.git

# Navigate to repository
cd ccpr_root

# Verify access
git status
gh repo view
```

#### Step 4: Configure Git Settings
```bash
# Set your identity
git config --global user.name "Your Full Name"
git config --global user.email "your.email@company.com"

# Set default branch name
git config --global init.defaultBranch main

# Configure line endings (Windows users)
git config --global core.autocrlf true

# Configure line endings (macOS/Linux users)
git config --global core.autocrlf input

# Set default editor
git config --global core.editor "code --wait"  # For VS Code
```

### Azure DevOps Setup

#### Prerequisites
- Azure DevOps organization access
- Project membership with appropriate permissions
- Azure CLI installation (optional but recommended)

#### Step 1: Install Azure CLI and Git
```bash
# Windows (using winget)
winget install Microsoft.AzureCLI
winget install Git.Git

# Windows (using chocolatey)
choco install azure-cli
choco install git

# macOS (using Homebrew)
brew install azure-cli
brew install git

# Linux (Ubuntu/Debian)
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
sudo apt update
sudo apt install git
```

#### Step 2: Authentication Setup
```bash
# Login to Azure DevOps
az login
az extension add --name azure-devops

# Set default organization
az devops configure --defaults organization=https://dev.azure.com/YourOrganization

# Generate personal access token (if needed)
# Go to: https://dev.azure.com/YourOrganization/_usersSettings/tokens
# Create token with appropriate scopes
```

#### Step 3: Repository Access
```bash
# Clone the repository
git clone https://dev.azure.com/YourOrganization/YourProject/_git/ccpr_root

# Configure credential manager
git config --global credential.helper manager-core

# Navigate to repository
cd ccpr_root

# Verify access
git status
az repos show --repository ccpr_root
```

### GitLab Setup

#### Prerequisites
- GitLab account with project access
- Group membership with appropriate permissions
- GitLab CLI installation (optional)

#### Step 1: Install Git and GitLab CLI
```bash
# Windows (using winget)
winget install Git.Git

# macOS (using Homebrew)
brew install git
brew install glab  # GitLab CLI

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install git

# Install GitLab CLI
curl -s https://raw.githubusercontent.com/profclems/glab/trunk/scripts/install.sh | sudo bash
```

#### Step 2: Authentication Setup
```bash
# Authenticate with GitLab (if using glab CLI)
glab auth login

# Or configure Git with personal access token
# Create token at: https://gitlab.com/-/profile/personal_access_tokens
git config --global credential.helper store
```

#### Step 3: Repository Access
```bash
# Clone the repository
git clone https://gitlab.com/organization/ccpr_root.git

# Or using SSH
git clone git@gitlab.com:organization/ccpr_root.git

# Navigate to repository
cd ccpr_root

# Verify access
git status
glab repo view  # If using GitLab CLI
```

## Development Environment Setup

### Text Editor Configuration

#### Visual Studio Code Setup
```bash
# Install VS Code extensions
code --install-extension ms-vscode.vscode-json
code --install-extension yzhang.markdown-all-in-one
code --install-extension davidanson.vscode-markdownlint
code --install-extension ms-vscode.powershell  # Windows users
code --install-extension mhutchie.git-graph

# Configure workspace settings
# Create .vscode/settings.json in repository root
```

VS Code Workspace Settings:
```json
{
  "files.eol": "\n",
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true,
  "markdown.extension.toc.levels": "2..6",
  "markdown.extension.print.absoluteImgPath": false,
  "markdownlint.config": {
    "MD024": false,
    "MD033": false
  },
  "git.enableCommitSigning": false,
  "editor.rulers": [80, 120],
  "editor.wordWrap": "wordWrapColumn",
  "editor.wordWrapColumn": 80
}
```

#### Alternative Editors
```yaml
Sublime Text:
  packages:
    - MarkdownEditing
    - GitGutter
    - SublimeLinter
    - Package Control
    
Atom:
  packages:
    - markdown-preview-plus
    - git-plus
    - linter-markdownlint
    
Vim/Neovim:
  plugins:
    - vim-markdown
    - vim-gitgutter
    - ale (for linting)
```

### Local Development Tools

#### Markdown Linting Setup
```bash
# Install markdownlint-cli globally
npm install -g markdownlint-cli

# Or use local installation
npm init -y
npm install --save-dev markdownlint-cli

# Create .markdownlint.json configuration
```

Markdownlint Configuration:
```json
{
  "default": true,
  "MD024": false,
  "MD033": {
    "allowed_elements": ["details", "summary", "br"]
  },
  "MD041": false,
  "line-length": {
    "line_length": 120,
    "code_blocks": false,
    "tables": false
  }
}
```

#### Git Hooks Setup (Optional)
```bash
# Navigate to repository
cd ccpr_root

# Set up pre-commit hook for markdown linting
echo '#!/bin/bash
markdownlint docs/**/*.md
if [ $? -ne 0 ]; then
  echo "Markdown linting failed. Please fix the issues before committing."
  exit 1
fi' > .git/hooks/pre-commit

# Make hook executable (macOS/Linux)
chmod +x .git/hooks/pre-commit
```

## Platform-Specific Optimizations

### Windows-Specific Setup

#### Windows Subsystem for Linux (WSL) - Optional
```bash
# Install WSL2 (Windows 10/11)
wsl --install

# Install Ubuntu distribution
wsl --install -d Ubuntu

# Configure Git in WSL
wsl
git config --global user.name "Your Name"
git config --global user.email "your.email@company.com"
```

#### Windows Terminal Configuration
```json
{
  "profiles": {
    "defaults": {
      "fontFace": "Cascadia Code",
      "fontSize": 12,
      "cursorShape": "bar"
    },
    "list": [
      {
        "name": "PowerShell",
        "source": "Windows.Terminal.PowershellCore",
        "startingDirectory": "C:\\Users\\%USERNAME%\\Documents\\GitHub\\ccpr_root"
      }
    ]
  }
}
```

### macOS-Specific Setup

#### Homebrew Package Manager
```bash
# Install Homebrew (if not already installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install development tools
brew install git
brew install node
brew install --cask visual-studio-code
brew install --cask github
```

#### Xcode Command Line Tools
```bash
# Install Xcode command line tools
xcode-select --install
```

### Linux-Specific Setup

#### Development Tools Installation
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install build-essential curl wget git

# CentOS/RHEL/Fedora
sudo yum groupinstall "Development Tools"
sudo yum install curl wget git

# Or for newer versions
sudo dnf groupinstall "Development Tools"
sudo dnf install curl wget git
```

## Network and Security Configuration

### Firewall and Proxy Settings

#### Corporate Firewall Configuration
```bash
# Configure Git to work with corporate proxy
git config --global http.proxy http://proxy.company.com:8080
git config --global https.proxy http://proxy.company.com:8080

# Configure npm proxy (if using Node.js tools)
npm config set proxy http://proxy.company.com:8080
npm config set https-proxy http://proxy.company.com:8080

# Bypass proxy for internal repositories
git config --global http.noproxy "internal.company.com"
```

#### SSL Certificate Issues
```bash
# If encountering SSL certificate issues
git config --global http.sslVerify false  # Use with caution

# Or add corporate certificates
git config --global http.sslCAInfo /path/to/corporate-cert.pem
```

### SSH Key Setup (Recommended)

#### Generate SSH Key
```bash
# Generate new SSH key
ssh-keygen -t ed25519 -C "your.email@company.com"

# Or use RSA if ed25519 is not supported
ssh-keygen -t rsa -b 4096 -C "your.email@company.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add key to SSH agent
ssh-add ~/.ssh/id_ed25519
```

#### Platform-Specific SSH Configuration

**GitHub:**
```bash
# Copy public key to clipboard
# Windows
clip < ~/.ssh/id_ed25519.pub

# macOS
pbcopy < ~/.ssh/id_ed25519.pub

# Linux
xclip -sel clip < ~/.ssh/id_ed25519.pub

# Add to GitHub: Settings > SSH and GPG keys > New SSH key
```

**Azure DevOps:**
```bash
# Add to Azure DevOps: User Settings > SSH public keys > Add
```

**GitLab:**
```bash
# Add to GitLab: Preferences > SSH Keys > Add key
```

## Verification and Testing

### Installation Verification Checklist
```bash
# Verify Git installation
git --version

# Verify platform CLI installation
gh --version          # GitHub
az --version           # Azure DevOps
glab --version         # GitLab

# Test repository access
git clone [repository-url]
cd ccpr_root
git status

# Test authentication
git remote -v
git ls-remote origin

# Test file operations
touch test.txt
git add test.txt
git commit -m "Test commit"
git push origin main  # Only if you have write access
git reset --hard HEAD~1  # Remove test commit
```

### Common Installation Issues

#### Permission Issues
```bash
# Windows: Run as Administrator if needed
# macOS/Linux: Use sudo only when necessary

# Fix file permissions (macOS/Linux)
chmod 755 ~/.ssh
chmod 600 ~/.ssh/id_*
chmod 644 ~/.ssh/id_*.pub
```

#### Path Issues
```bash
# Add Git to PATH (if not automatic)
# Windows: Add C:\Program Files\Git\bin to system PATH
# macOS/Linux: Usually automatic with package managers

# Verify PATH
echo $PATH  # macOS/Linux
echo $env:PATH  # Windows PowerShell
```

#### Network Connectivity Issues
```bash
# Test connectivity
ping github.com
curl -I https://github.com

# Check proxy settings
git config --list | grep proxy

# DNS issues
nslookup github.com
```

## Post-Installation Setup

### Repository Structure Familiarization
```bash
# Navigate to repository
cd ccpr_root

# Explore structure
ls -la                    # List all files and directories
tree                      # Show directory tree (if installed)
find . -name "*.md"       # Find all markdown files

# Read key documentation
cat README.md
cat instructions.md
ls docs/
```

### Initial Configuration
```bash
# Set up branch tracking
git branch --set-upstream-to=origin/main main

# Configure local settings
git config user.name "Your Name"
git config user.email "your.email@company.com"

# Set up aliases (optional)
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.up "pull --rebase"
```

### Team Communication Setup
```yaml
Communication Channels:
  repository_issues: "Use for technical questions and bug reports"
  team_chat: "Slack/Teams channel for quick discussions"
  email_lists: "For formal communications and announcements"
  documentation: "Check docs/ directory for detailed guides"
```

## Troubleshooting Installation Issues

### Common Problems and Solutions

#### Authentication Failures
```bash
# Clear stored credentials
git config --global --unset credential.helper
git config --system --unset credential.helper

# Re-authenticate
gh auth logout
gh auth login  # GitHub
az logout && az login  # Azure DevOps
```

#### Repository Access Issues
```bash
# Verify organization membership
gh api user/orgs  # GitHub
az devops user show  # Azure DevOps

# Check repository permissions
gh repo view organization/ccpr_root
```

#### Network Issues
```bash
# Test different protocols
git clone https://github.com/organization/ccpr_root.git
git clone git@github.com:organization/ccpr_root.git

# Check corporate network restrictions
curl -v https://github.com
```

### Getting Help

#### Internal Support
- **IT Helpdesk**: Technical installation support
- **Repository Administrators**: Access and permission issues
- **Team Leads**: Process and workflow guidance

#### External Resources
- **Platform Documentation**: GitHub, Azure DevOps, GitLab docs
- **Git Documentation**: Official Git documentation and tutorials
- **Community Forums**: Stack Overflow, platform-specific communities

## Success Criteria

### Installation Complete When:
- [ ] Git and platform CLI tools installed and working
- [ ] Authentication configured and tested
- [ ] Repository successfully cloned and accessible
- [ ] Development environment configured
- [ ] Basic Git operations tested
- [ ] Team communication channels set up
- [ ] Documentation reviewed and understood

Your installation is complete when you can successfully clone the repository, make test commits, and access all necessary documentation and resources. Contact your team lead or administrator if you encounter issues that prevent completing these basic operations.