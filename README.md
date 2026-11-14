# Dell Latitude 7490 — Minimal Arch to Labwc development workstation

A reusable setup prompt for Codex CLI. It takes an installed, network-connected **minimal Arch Linux** system and configures Labwc, desktop utilities, Firefox, VS Code/Code - OSS, Docker Engine, a PostgreSQL 18 development container, Python/UV, Node.js/npm, and laptop power/peripheral support.

## Files

- `SETUP_PROMPT.md` — full nine-phase post-installation instruction set.
- `AGENTS.md` — short repository-level instructions that Codex automatically loads when run here.
- `README.md` — usage and publishing instructions.

## On the fresh Arch installation

Prerequisites: `git` and `codex` installed, logged in to Codex, and a working network connection.

```bash
git clone https://github.com/gabrielgv13/arch-latitude-7490-codex-setup.git
cd arch-latitude-7490-codex-setup
codex
```

Then type:

```text
Follow SETUP_PROMPT.md and begin Phase 1. Inspect the system first, then perform the setup phase by phase with the required approvals.
```

Codex reads `AGENTS.md` automatically from the working directory. Keep the repository in your user home directory or another user-writable location, and **launch Codex as a normal user, not root**.

## Publish this package to GitHub for the first time

Create a **new empty repository** named `arch-latitude-7490-codex-setup` under your GitHub account (leave README, license, and `.gitignore` uninitialized). From the directory containing these three files, run:

```bash
git init -b main
git add README.md AGENTS.md SETUP_PROMPT.md
git commit -m "Add Dell Latitude Arch post-install Codex plan"
git remote add origin https://github.com/gabrielgv13/arch-latitude-7490-codex-setup.git
git push -u origin main
```

Alternatively, with an authenticated GitHub CLI (`gh`), after `git init` and `git commit`, you can create and push a private repository:

```bash
gh repo create arch-latitude-7490-codex-setup --private --source=. --remote=origin --push
```

The GitHub clone URL above is **a proposed destination**; it won't work until that repository has actually been created and the files pushed.

## Safety

This repository contains **instructions only**. Nothing runs when you clone it. Codex should review system state and obtain approval for privileged operations. A standard Arch installation retains systemd as PID 1; GRUB does not replace systemd.
