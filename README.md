# New macOS Machine Setup

This guide is based on my own experience, but also draws on other guides. It 
is primarily oriented towards those doing code-related stuff.

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

## Verify or Install Apple's Command-line Tools

First, make sure that you have Apple's command-line tools installed by executing:

```bash
xcode-select -p
```

If you get a path back (like `/Applications/Xcode.app/Contents/Developer`) then 
you are good to go. Otherwise:

```bash
xcode-select --install
```

In the dialog that pops up, click **Install** and click **Agree** for the 
license agreement.

**Note**: If you get a message that says "Can't install the software because 
it is not currently available from the Software Update server." then you will 
need to download it from [here](https://developer.apple.com/download/more/) 
(look for **Command Line Tools**...).

## Install :beer: Homebrew

This is the first thing I normally do. As I have said before,
[haters gonna hate](https://applehelpwriter.com/2018/03/21/how-homebrew-invites-users-to-get-pwned/),
but this is the quickest, easiest way to get a commonly-referenced package
manage on the Mac.

To install **Homebrew**, run this command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then update your `~/.zprofile`

```bash
echo >> /Users/mpellon/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/mpellon/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

To make sure it is all working correctly, restart your shell then execute:

```bash
brew doctor
```

Finally, just to make sure everything's up-to-date:

```bash
brew update
```

## Install Ghostty

Why Ghostty over other macOS terminals (in two bites):

1. **Metal-powered rendering + native UI**. Ghostty uses the GPU (Metal on macOS)
   and a platform-native interface, which makes scrolling and redraws feel
   snappy and keeps it visually consistent with macOS.

2. **Modern ergonomics**. Built-in features like the Quick Terminal hotkey let you
   summon a terminal instantly without context-switching, a trick many terminals
   bolt on via third-party tools.

Install (stable):

```bash
brew install --cask ghostty
```

That is the official cask; it installs the signed, notarized macOS app.

Launch it: Spotlight → “Ghostty”, or from Applications.

### Quick setup: add a global “quick terminal” hotkey

Ghostty has a DOOM/quake-style Quick Terminal you can drop down with a single keystroke. 
Ghostty

Create/edit your config file at:

```bash
~/Library/Application Support/com.mitchellh.ghostty/config (macOS native path), or
```

Add:

```bash
# Toggle the drop-down terminal from anywhere on macOS
keybind = global:cmd+backquote=toggle_quick_terminal
quick-terminal-position = top
```

Keybinding + option names are from Ghostty’s docs. If you use a global keybind, 
macOS will prompt for Accessibility permission so the hotkey works when Ghostty 
is not focused.

## Install Pareto Security (and make every check green)

These steps install the macOS app via Homebrew Cask and walk you through resolving 
each built-in security check so the app shows all green.

```bash
brew update
brew install --cask pareto-security
```

Launch it from Applications (or Spotlight). Pareto lives in your menu bar and turns 
green when all checks pass; orange means something needs attention.

### Run the checks

- Click the Pareto Security menu-bar icon.
- Choose Run Checks (or it will run automatically in the background).
- For any item that’s orange, click it—Pareto links to a brief “how to fix” guide for that check.
- You can also disable business-only checks you don’t care about: Pareto Security → Preferences → Checks.

## Browser Installation

You can easily install your Browsers using Homebrew.

### Install Chrome

🍺 Reference https://formulae.brew.sh/cask/google-chrome for the source of truth

1. Run the following command to update homebrew

```bash
brew update
```

Run the following command to install Chrome

```bash
brew install --cask google-chrome
```

## NodeJS Installation

1. First, ensure there is not already a version of [Node](https://node.js.org/) 
installed.

```bash
brew uninstall --ignore-dependencies node
brew uninstall --force node
```

2. Install NVM with Homebrew and create a directory in your home directory:

```bash
brew update
brew install nvm
mkdir ~/.nvm
```

3. Update your ZSH (Z-shell) resource:

```bash
# Add the following line towards the end of your zshrc:

# Node Version Manager
export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"
[ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"
```

4. Now, let's pick the version of NodeJS to install.

```bash
nvm install 22.20.0
```

## Git Minimal Setup

We will use Homebrew:

```bash
brew install git
```

```bash
# Create & Edit the .gitconfig file:
nano .gitconfig

# Add your user info stanza
[user]
    email = youremail@somecompany.com
    name = Your Name
```

## Claude Code Setup

To install Claude Code, run the following command:

```bash
npm install -g @anthropic-ai/claude-code
```
