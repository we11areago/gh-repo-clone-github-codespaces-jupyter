# GitHub Codespaces ♥️ Jupyter Notebooks

Welcome to your shiny new codespace! We've got everything fired up and running for you to explore Python and Jupyter notebooks.

You've got a blank canvas to work on from a git perspective as well. There's a single initial commit with what you're seeing right now - where you go from here is up to you!

Everything you do here is contained within this one codespace. There is no repository on GitHub yet. If and when you’re ready you can click "Publish Branch" and we’ll create your repository and push up your project. If you were just exploring then and have no further need for this code then you can simply delete your codespace and it's gone forever.

## Connecting to Your Codespace via the CLI

With a GitHub Pro account you can drop into your Codespace directly from the terminal using the [GitHub CLI](https://cli.github.com/):

```bash
gh codespace ssh
```

If you have multiple Codespaces, you can list them first and then connect to a specific one:

```bash
# List your Codespaces
gh codespace list

# SSH into a specific Codespace by name
gh codespace ssh -c <codespace-name>
```

Make sure you have the GitHub CLI installed and are authenticated (`gh auth login`) before running these commands.

## Connecting from Termux (Android)

[Termux](https://termux.dev/) is a terminal emulator for Android that lets you run a full Linux environment on your phone. With your paid GitHub account you can SSH into your Codespace directly from Termux.

### 1. Install the GitHub CLI in Termux

```bash
pkg update && pkg upgrade
pkg install gh
```

### 2. Authenticate with GitHub

```bash
gh auth login
```

Follow the prompts — choose **GitHub.com**, then **SSH**, and authenticate via your browser or a one-time code.

### 3. Connect to your Codespace

```bash
# List your Codespaces
gh codespace list

# SSH into your Codespace
gh codespace ssh -c <codespace-name>
```

Replace `<codespace-name>` with the name shown by `gh codespace list`. If you only have one Codespace, `gh codespace ssh` will connect to it automatically.
