# Installing GitHub Copilot CLI with SpecKit on Windows

Step-by-step instructions for setting up a Windows workstation with Python (via uv), the GitHub Copilot CLI, and GitHub Spec Kit. All commands run in PowerShell. No administrator rights are needed unless noted.

## What you'll end up with

| Tool               | Purpose                                    | Command         |
| ------------------ | ------------------------------------------ | --------------- |
| PowerShell 7       | Required shell for Copilot CLI             | `pwsh`          |
| uv                 | Python installer and package/tool manager  | `uv`            |
| Python             | Managed by uv                              | `uv run python` |
| GitHub Copilot CLI | Agentic Copilot in the terminal            | `copilot`       |
| Specify CLI        | Spec Kit's spec-driven development tooling | `specify`       |

## Before you start: corporate network certificates

If your network uses a TLS-inspecting proxy (Zscaler, Netskope, Cisco Umbrella, and similar), tools that ship their own certificate bundle will fail with errors like:

```
invalid peer certificate: UnknownIssuer
```

The proxy's root certificate is already in the Windows certificate store, but uv does not use that store by default. This guide sets `UV_SYSTEM_CERTS` once (Step 3) and also shows `--system-certs` on each network-dependent uv command, so the commands work whether or not the environment variable is set. On a network without a TLS-inspecting proxy, the flag is harmless.

---

## Step 1: Install PowerShell 7

Copilot CLI requires PowerShell 6 or higher. Windows ships with Windows PowerShell 5.1, so check first:

```powershell
$PSVersionTable.PSVersion
```

If the major version is 5, install PowerShell 7:

```powershell
winget install Microsoft.PowerShell
```

Close the window and open **PowerShell 7** (`pwsh`) from the Start menu. Run every remaining step in `pwsh`.

---

## Step 2: Install uv

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Alternative if you prefer WinGet:

```powershell
winget install --id=astral-sh.uv -e
```

Open a **new** PowerShell window so the updated PATH takes effect, then verify:

```powershell
uv --version
```

---

## Step 3: Configure uv to trust the Windows certificate store

Set this once for your user account so every uv command uses the Windows certificate store:

```powershell
[Environment]::SetEnvironmentVariable("UV_SYSTEM_CERTS", "true", "User")
```

Open a new PowerShell window for the variable to take effect.

---

## Step 4: Install Python

Install the latest stable Python:

```powershell
uv python install --system-certs
```

uv stores interpreters under `%LOCALAPPDATA%\uv\python`.

### How to run Python

By default, uv installs versioned executables (for example `python3.13.exe`), not a bare `python.exe`. Typing `python` may still open the Microsoft Store. Pick one approach:

**Option A: uv-managed (recommended).** Let uv find the interpreter:

```powershell
uv run python --version
```

In a project, `uv venv` creates a virtual environment and `uv run` uses it automatically.

**Option B: put `python` on PATH.**

```powershell
uv python install 3.13 --default --system-certs
```

Then disable the Store shortcuts: **Settings > Apps > Advanced app settings > App execution aliases**, and turn off `python.exe` and `python3.exe`.

Verify:

```powershell
uv python list --only-installed
```

---

## Step 5: Install GitHub Copilot CLI

**Prerequisite:** an active Copilot license. If your Copilot seat comes from an organization, an admin must enable the **Copilot CLI** policy. That setting is separate from IDE Copilot, so working Copilot in VS Code does not guarantee the CLI will work.

Install with WinGet (recommended):

```powershell
winget install GitHub.Copilot
```

Open a new `pwsh` window, change into a repository, and launch:

```powershell
copilot
```

On first launch, type `/login` and follow the prompts to authenticate with GitHub.

---

## Step 6: Install the Specify CLI (Spec Kit)

Check the [Spec Kit releases page](https://github.com/github/spec-kit/releases) for the latest tag. At the time of writing it is `v1.0.1`. Keep the leading `v`.

```powershell
uv tool install specify-cli --system-certs --from git+https://github.com/github/spec-kit.git@v1.0.1
```

This requires `git` on your PATH. If you don't have Git, install from the Company Portal:

```powershell
uv tool install specify-cli --system-certs
```

Make sure uv's tool directory is on your PATH:

```powershell
uv tool update-shell
```

Open a new `pwsh` window and verify:

```powershell
specify version
specify check
```

`specify check` reports which AI agents it detects, including Copilot.

---

## Step 7: Initialize a project

New project:

```powershell
specify init my-project --integration copilot
cd my-project
```

Existing repository (run from the repo root):

```powershell
specify init --here --integration copilot
```

Run `specify init --help` to see the full list of integrations. If a Copilot CLI-specific integration appears, use it when you work primarily in the terminal rather than VS Code.

### Spec Kit workflow

Launch `copilot` (or Copilot Chat in VS Code) in the project directory and run these commands in order:

| Order | Command                 | Purpose                                            |
| ----- | ----------------------- | -------------------------------------------------- |
| 1     | `/speckit-constitution` | Set project principles (once per project)          |
| 2     | `/speckit-specify`      | Describe what to build                             |
| 3     | `/speckit-plan`         | Decide how to build it                             |
| 4     | `/speckit-tasks`        | Break the plan into tasks                          |
| 5     | `/speckit-implement`    | Implement the tasks                                |
| 6     | `/speckit-converge`     | Check implementation against spec, plan, and tasks |

Repeat steps 4 and 5 until `/speckit-converge` reports **Converged**.

---

## Keeping things up to date

| Tool        | Command                                                                                                       |
| ----------- | ------------------------------------------------------------------------------------------------------------- |
| uv          | `uv self update --system-certs`                                                                               |
| Python      | `uv python install 3.13 --reinstall --system-certs`                                                           |
| Copilot CLI | `winget upgrade GitHub.Copilot`                                                                               |
| Specify CLI | `uv tool install specify-cli --force --system-certs --from git+https://github.com/github/spec-kit.git@vX.Y.Z` |

---

## References

- uv installation: https://docs.astral.sh/uv/getting-started/installation/
- Installing Python with uv: https://docs.astral.sh/uv/guides/install-python/
- uv TLS certificates: https://docs.astral.sh/uv/concepts/authentication/certificates/
- Installing GitHub Copilot CLI: https://docs.github.com/en/copilot/how-tos/copilot-cli/install-copilot-cli
- Spec Kit releases: https://github.com/github/spec-kit/releases


