# New macOS Machine Setup

This guide walks through setting up a new Mac with my dotfiles and preferred tools.

## First Boot

When macOS first starts, you'll be greeted by Setup Assistant.

When creating the first account, use a [strong password](https://www.eff.org/dice)
without a hint.

If you enter your real name at the account setup process, be aware that your
computer's name and local hostname will comprise that name (e.g., John Appleseed's
MacBook) and thus will appear on local networks and in various preference files.

Both should be verified and updated as needed in System Settings > About or with the
following commands after installation:

```bash
sudo scutil --set ComputerName MacBook
sudo scutil --set LocalHostName MacBook
```

## Install Apple's Command-line Tools

```bash
xcode-select -p
```

If you get a path back (like `/Applications/Xcode.app/Contents/Developer`) then
you're good to go. Otherwise:

```bash
xcode-select --install
```

## Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then add Homebrew to your PATH:

```bash
echo >> ~/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verify:

```bash
brew doctor
```

## Clone Dotfiles with yadm

[yadm](https://yadm.io/) manages dotfiles using Git without turning your home
directory into a repository.

```bash
brew install yadm
yadm clone https://github.com/michellepellon/dotfiles.git
```

This pulls down all configuration files including the Brewfile at
`~/.config/brewfile/Brewfile`.

## Install Everything with Brewfile

Once dotfiles are cloned, install all packages at once:

```bash
brew bundle --file=~/.config/brewfile/Brewfile
```

This installs:

**CLI tools:**
- `git` - Version control
- `gh` - GitHub CLI
- `nvm` - Node version manager
- `yadm` - Dotfiles manager
- `speedtest` - Ookla speed test (requires tap)
- `htop` - Interactive process viewer

**Applications:**
- [Ghostty](https://ghostty.org/) - GPU-accelerated terminal
- [Docker](https://www.docker.com/) - Container platform
- [Pareto Security](https://paretosecurity.com/) - Security checklist
- [Google Chrome](https://www.google.com/chrome/) - Browser
- [Beekeeper Studio](https://www.beekeeperstudio.io/) - SQL client
- [Zoom](https://zoom.us/) - Video conferencing
- [Granola](https://www.granola.ai/) - AI meeting notes
- [Bitwarden](https://bitwarden.com/) - Password manager

## Post-Install Configuration

### NVM Setup

Create the NVM directory and add to your shell config:

```bash
mkdir ~/.nvm
```

Add to `~/.zshrc`:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"
[ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"
```

Then install Node:

```bash
nvm install --lts
```

### GitHub CLI

```bash
gh auth login
```

### Git Configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Pareto Security

Launch from Applications. Click the menu-bar icon and run checks. For any orange
items, click to see how to fix.

### Ghostty Quick Terminal

Add to `~/Library/Application Support/com.mitchellh.ghostty/config`:

```
keybind = global:cmd+backquote=toggle_quick_terminal
quick-terminal-position = top
```

### Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

### Claude Workbench Plugin

Install the marketplace and workbench plugin for additional skills and commands:

```bash
claude plugin marketplace add https://github.com/michellepellon/claude-marketplace
claude plugin install workbench@claude-marketplace
```
