# Setup guide: Installing required tools for the Agentic Coding Workshop

Welcome to the **Agentic Coding Workshop**! Before we start, we’ll make sure all tools are installed. Follow the steps below in order for anything you don’t already have.

---

## 1. Python 3.10+

**macOS / Windows:**

Download and run the installer from https://www.python.org/downloads/

> On Windows: enable **“Add Python to PATH”** during installation!

**Linux:**

Python is often pre-installed. Check the version:

```bash
python3 --version
```

**Verify installation:**

```bash
python3 --version  # Should show 3.10 or higher
```

More info: [Official Python downloads](https://www.python.org/downloads/)

---

## 2. uv (Python package manager)

**macOS / Linux:**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows (PowerShell):**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Alternative (Homebrew):**

```bash
brew install uv
```

**Verify installation:**

```bash
uv --version
```

More info: [Official uv installation guide](https://docs.astral.sh/uv/getting-started/installation/)

---

## 3. Node.js & npm

**Recommended: official installer**

- Download from: https://nodejs.org/
- Choose the LTS (Long Term Support) version
- npm is installed automatically

**Alternative (macOS — Homebrew):**

```bash
brew install node
```

**Alternative (Windows — Chocolatey):**

```bash
choco install nodejs
```

**Verify installation:**

```bash
node --version
npm --version
```

More info: [Official Node.js downloads](https://nodejs.org/en/download/)

---

## 4. AI coding assistant

Install the **AI coding assistant** you will use during the workshop (IDE plugin, desktop app, or CLI)—follow your tool’s official documentation.

**Check** that you can use the assistant from your project folder (or IDE). These exercises do not require a specific vendor CLI.

---

## 5. VS Code (recommended)

**All platforms:**

- Download the installer for your OS: https://code.visualstudio.com/download
- Run the installer
- Follow the setup wizard

**Verify installation:**

```bash
code --version
```

More info: [Official VS Code downloads](https://code.visualstudio.com/download)

---

## 6. Git

**macOS:**

Git is usually installed the first time you run it. In your terminal, type:

```bash
git --version
```

If Git isn’t installed yet, you may get a prompt to install the Xcode Command Line Tools. Alternatively with Homebrew:

```bash
brew install git
```

**Windows:**

- Download from: https://git-scm.com/download/win
- Run the installer

**Linux (Ubuntu / Debian):**

```bash
sudo apt install git-all
```

**Linux (Fedora / RHEL):**

```bash
sudo dnf install git-all
```

**Verify installation:**

```bash
git --version
```

More info: [Official Git installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

---

## Final check

Run all commands to verify everything is installed:

```bash
python3 --version    # Should show 3.10+
uv --version         # Should show a version number
node --version       # Should show a version number
npm --version        # Should show a version number
code --version       # Should show a version number
git --version        # Should show a version number
```

**Do all commands print a version? You’re ready to start.**

**Seeing “command not found”?** Restart your terminal and try again. If it still fails, ask your AI coding assistant for help. Usually the fix is updating your PATH environment variable.

---

## Other AI coding assistants

This workshop teaches patterns that work with **any** AI coding assistant, for example:

- **Cursor**: https://cursor.sh/
- **GitHub Copilot**: https://github.com/features/copilot
- **Aider**: https://aider.chat/

Use whatever you’re comfortable with.

---

## Need help?

- Use the official documentation linked above
- During the workshop, ask **Dennis Claassen** or **Joppe van der Schoot**
