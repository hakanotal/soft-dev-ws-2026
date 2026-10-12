# Workshop setup

Please finish this **before the workshop**. It takes about 30 to 45 minutes. Every step works on Windows, macOS and Linux; where they differ, follow the line for your system.

When you are done, step 11 shows you how to check that nothing is missing.

## Before you start

You need:

- A computer running Windows 10 or newer, macOS 13 or newer, or Linux (Ubuntu 20.04+, Debian 10+ or similar), with permission to install software.
- A **Claude account that includes Claude Code**: Pro, Max, Team or Enterprise, or a Claude Console (API) account. **The free Claude plan does not include Claude Code.** Plans: https://claude.com/pricing. If the organizers give you an account, use that one.

---

## Part 1: Install Git and Cursor, then get the workshop files

Do this part in your web browser. You can read it on GitHub before you have anything installed.

### Step 1. Create a GitHub account

Sign up at https://github.com/signup (skip this if you already have one). Remember your username and the email you used.

### Step 2. Install Git

- **Windows:** go to https://git-scm.com/downloads/win, click the download link for the 64-bit installer, run it and keep all the default options. This also installs Git Bash, which Claude Code uses.
- **macOS:** open the **Terminal** app (press Cmd+Space, type `Terminal`, press Enter). Paste `xcode-select --install` and press Enter. In the window that appears, click **Install** and wait for it to finish (if it says the tools are already installed, that is fine). Then run `git --version`: it should print a version number. Other options: https://git-scm.com/downloads/mac
- **Linux:** follow https://git-scm.com/downloads/linux, for example `sudo apt install git` on Ubuntu or Debian, or `sudo dnf install git` on Fedora.

### Step 3. Install Cursor

Download Cursor for your system from https://cursor.com/download and install it. Open it and sign in or create a free Cursor account when it asks.

### Step 4. Make your own copy of the workshop repo and open it

1. Go to https://github.com/hakanotal/soft-dev-ws-2026 (log in to GitHub first).
2. Click the green **Use this template** button, then **Create a new repository**.
3. Owner: your username. Repository name: for example `penguin-explorer`. Choose **Public** (GitHub Pages needs this on free accounts). Click **Create repository**.
4. On your new repository's page, click the green **Code** button and copy the HTTPS address (it ends in `.git`).
5. In Cursor, open the Command Palette: **Ctrl+Shift+P** (Windows, Linux) or **Cmd+Shift+P** (macOS). Type `Git: Clone`, press Enter, paste the address and press Enter.
6. Choose a folder to put it in (for example your Documents folder), then click **Open** when Cursor asks.

---

## Part 2: Everything else, from inside Cursor

From here on, work inside Cursor with your repo open.

**Open this guide inside Cursor** so the links are clickable: in the file list on the left, open `docs/install.md`, then press **Ctrl+Shift+V** (Windows, Linux) or **Cmd+Shift+V** (macOS) to see the preview.

**Open a terminal** in Cursor: menu **Terminal > New Terminal**. All the commands below go in this terminal. To run a command, paste it and press Enter.

> **The most common problem:** after installing something, the terminal says *command not found* or *is not recognized*. Cursor only sees new programs after a restart. **Quit Cursor completely** (not just the window) and open it again. On Windows, if that does not help, restart the computer.

### Step 5. Install the recommended extensions

Cursor may show a pop-up asking *Do you want to install the recommended extensions?* Click **Install**.

If you missed it: open the Extensions panel with **Ctrl+Shift+X** (Windows, Linux) or **Cmd+Shift+X** (macOS), type `@recommended` in the search box, and click **Install** on each extension under *Workspace Recommendations*.

<details>
<summary>The list of extensions</summary>

| Extension | What it is for |
|---|---|
| Claude Code for VS Code | Claude Code inside the editor |
| Python, Jupyter | Python editing and notebooks |
| Ruff | Formats Python code and flags common mistakes |
| Rainbow CSV | Readable CSV files |
| Git Graph | See your commit history as a graph |
| YAML | Editing config files such as the deploy workflow |
| Markdown PDF, vscode-pdf | Export and view PDFs |
| Material Icon Theme, One Dark Pro | Icons and a colour theme (optional) |

</details>

### Step 6. Tell Git who you are

Use your own name and the email of your GitHub account:

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Step 7. Install Node.js

Go to https://nodejs.org/en/download, choose the **LTS** version (24 at the time of writing), and download the installer for your system. On Linux, the same page shows the commands to run.

Run the installer with the default options, then **quit and reopen Cursor**.

### Step 8. Install uv (it manages Python for you)

You do not need to install Python separately: uv downloads the right version.

- **Windows** (paste into Cursor's terminal):
  ```
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```
- **macOS and Linux:**
  ```
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

**Quit and reopen Cursor**, then run:

```
uv python install
```

More detail: https://docs.astral.sh/uv/getting-started/installation/

### Step 9. Install the GitHub CLI and log in

This lets you and Claude push code and open pull requests without typing passwords.

- **Windows:** open https://github.com/cli/cli/releases/latest, scroll to *Assets*, download the file ending in `windows_amd64.msi` (or `windows_arm64.msi` on an ARM laptop) and run it.
- **macOS:** open https://github.com/cli/cli/releases/latest, scroll to *Assets*, download the file ending in `macOS_universal.pkg` and open it. macOS will say it cannot verify the developer: click **Done**, then open **System Settings > Privacy & Security**, scroll down, click **Open Anyway** next to the gh message, and run the installer.
- **Linux:** follow https://github.com/cli/cli/blob/trunk/docs/install_linux.md

**Quit and reopen Cursor**, then run:

```
gh auth login
```

Choose **GitHub.com**, then **HTTPS**, answer **Yes** to *Authenticate Git with your GitHub credentials*, then **Login with a web browser**. Copy the code it shows, press Enter, and paste the code in the browser page that opens.

### Step 10. Install Claude Code and log in

- **Windows** (in Cursor's terminal, which is PowerShell):
  ```
  irm https://claude.ai/install.ps1 | iex
  ```
- **macOS and Linux:**
  ```
  curl -fsSL https://claude.ai/install.sh | bash
  ```

**Quit and reopen Cursor**, then in the terminal run:

```
claude
```

1. Pick a theme, then log in with your Claude account in the browser window that opens. (If the browser does not open, press `c` to copy the link and paste it into your browser.)
2. If it asks whether you trust this folder, answer yes.
3. If it asks to use the MCP servers in `.mcp.json` (**context7** and **playwright**), approve them.
4. Type `/terminal-setup` and press Enter. This makes Shift+Enter add a new line in Cursor's terminal.
5. Type `/exit` and press Enter.

Also install **Google Chrome** if you do not have it: https://www.google.com/chrome/. Claude uses it to look at the web page you build.

More detail: https://code.claude.com/docs/en/setup

### Step 11. Check everything

Run each command in Cursor's terminal. If one does not show what the table expects, go back to the step in the last column.

| Command | You should see | If not, see |
|---|---|---|
| `git --version` | `git version 2.` something | Step 2 |
| `git config --global user.email` | Your email | Step 6 |
| `node -v` | `v22.12` or newer (`v24` is ideal) | Step 7 |
| `npm -v` | A version number | Step 7 |
| `uv --version` | `uv` and a version number | Step 8 |
| `uv python find` | A path to a Python program | Step 8 |
| `gh auth status` | `Logged in to github.com` | Step 9 |
| `claude --version` | A version number and `(Claude Code)` | Step 10 |

When every row matches, you are ready. See you at the workshop.

---

## Troubleshooting

**"command not found" or "is not recognized as the name of a cmdlet".** Quit Cursor completely and reopen it. On Windows, restart the computer if that does not help.

**Windows: "running scripts is disabled on this system"** (often when running `npm`). Run this once in Cursor's terminal, then try again:

```
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

**`claude` says you need a subscription or cannot log in.** Check that your Claude account is Pro, Max, Team, Enterprise or Console. The free plan does not include Claude Code.

**`gh auth status` says you are not logged in.** Run `gh auth login` again (step 9).

**Still stuck?** Copy the command you ran and the full error message, and send them to the organizers before the workshop.
