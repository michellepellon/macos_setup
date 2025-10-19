# New macOS Machine Setup

This guide is based on my own experience, but also draws on other guides. It 
is primarily oriented towards those doing code-related stuff.

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

To make sure it's all working correctly, execute:

```bash
brew doctor
```

Finally, just to make sure everything's up-to-date:

```bash
brew update
```

## Browser Installation

You can easily install your Browsers using Homebrew.

### Install Chrome

🍺 Reference https://formulae.brew.sh/cask/google-chrome for the source of truth

1. Run the following command to update homebrew

```bash
brew up
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
