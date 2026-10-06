# Setup

Clone this repository onto your own native filesystem and open its root in Codex or Claude Code. Each person authenticates to business systems using their own account. No credentials ship with this repository.

Codex uses the canonical `.agents/skills/` files. Claude Code uses the generated `.claude/skills/` files and CLAUDE.md. These are repository skill folders, not a claim that this repo is already a packaged plugin for every Claude or Codex interface. Verify skill discovery in the client you use.

## Install tools on a Lumenis work laptop

You need Git, Node.js 22 or newer for the helpers, and GitHub CLI (`gh`) for pull requests. Work laptops might block administrator prompts, so the steps below install for your account only. Run them in PowerShell, then open a **new** PowerShell window so the updated PATH takes effect..

**Git.** Git for Windows can install for your own account:

```powershell
winget install --id Git.Git -e --source winget
```

**Node.js and GitHub CLI.** Try `winget install --id OpenJS.NodeJS.LTS -e` and `winget install --id GitHub.cli -e` first. If either says `You cancelled the installation` (exit code 1602) when you did not decline a prompt, the laptop is blocking administrator installs. Use the official portable zips instead. Set the versions to the current Node.js LTS (22 or newer) and the latest [GitHub CLI release](https://github.com/cli/cli/releases):

```powershell
$node = "24.19.0"; $gh = "2.102.0"
$tools = "$env:USERPROFILE\tools"; New-Item -ItemType Directory -Force $tools | Out-Null
$nodeZip = "node-v$node-win-x64.zip"; $ghZip = "gh_${gh}_windows_amd64.zip"
Invoke-WebRequest "https://nodejs.org/dist/v$node/$nodeZip" -OutFile "$tools\$nodeZip" -UseBasicParsing
Invoke-WebRequest "https://github.com/cli/cli/releases/download/v$gh/$ghZip" -OutFile "$tools\$ghZip" -UseBasicParsing
Get-FileHash "$tools\$nodeZip", "$tools\$ghZip"
```

Compare each hash with the matching line in `https://nodejs.org/dist/v<version>/SHASUMS256.txt` and the `gh_<version>_checksums.txt` file on the GitHub CLI release page. Stop if either differs. Then extract and add both to your user PATH:

```powershell
Expand-Archive "$tools\$nodeZip" $tools -Force; Rename-Item "$tools\node-v$node-win-x64" node
Expand-Archive "$tools\$ghZip" "$tools\gh" -Force; Remove-Item "$tools\*.zip"
$path = [Environment]::GetEnvironmentVariable('Path', 'User')
[Environment]::SetEnvironmentVariable('Path', "$path;$tools\node;$tools\gh\bin", 'User')
```

**Sign in to GitHub.** In a new window, run the commands below. The first shows a one-time code and opens github.com to approve it. The second lets Git push with the same login. Never paste tokens or passwords into an AI chat or this repository.

```powershell
gh auth login --web --git-protocol https
gh auth setup-git
```

**Check.** `git --version`, `node --version` (22 or newer) and `gh auth status` should all succeed.

## Clone

Clone into C:\Users\[User Name].

## Verify

From the repository root:

```sh
node scripts/validate.mjs
node scripts/name.mjs VIS "Example Webinar" "Q1 2030" US
```

Image lookup defaults to `assets/image-library/catalog.json` in this repository. To override it with another reviewed catalog:

```sh
export LUMENIS_ASSET_CATALOG="/path/to/reviewed/catalog.json"
node .agents/skills/lumenis-image-search/find-images.mjs --brand OptiLIFT --json
```

See [image-library setup and maintenance](../assets/image-library/README.md) for intake, resizing and HubSpot uploads. Missing rights metadata stays unverified. Image bytes need not be local when the catalog provides hosted URLs. Do not put personal paths or the catalog's confidential approval evidence in Git.

Supply an output folder outside the repository. A fresh-clone pilot must verify both clients, each relevant division, asset access and missing-input behavior before production use.

## Daily use and updates

The technical helper sets up each teammate's own account and verifies skill discovery in their chosen client. A first task can be a webinar outline for the writer, a form-field audit for operations, or a KBYG draft for events. State division and desired output; the assistant uses the relevant skill rather than requiring a giant pasted prompt.

Before a new task, fetch reviewed updates with `git pull --ff-only` from the repository root. If local edits or divergent history prevent it, preserve them and ask the maintainer to reconcile; do not discard contributions. Updates do not arrive automatically just because a change was merged. Record `git rev-parse --short HEAD` in the external handoff when version traceability matters. Update between tasks, not silently mid-task.

Search metadata with `node scripts/discover.mjs --query forms --limit 5`. A teammate should be able to explain what files and live systems the assistant actually accessed. See [the foundations plan](ai-foundations.md) for the small first pilot.
