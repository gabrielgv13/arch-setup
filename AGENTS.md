# Codex repository instructions

This repository is an installation plan, not a software project. It is meant to be cloned onto a **fresh minimal Arch Linux installation on a Dell Latitude 7490**.

When the user asks you to configure this machine, **read `SETUP_PROMPT.md`** and follow its phase-by-phase execution instructions. Run a read-only system inspection before changes, execute actual installation steps after appropriate approvals, test each stage, and log results in `~/system-setup/`.

Never assume the machine matches the expected hardware, install state, memory, firmware, filesystem, network, or service configuration. Verify facts locally. Use current ArchWiki and upstream documentation to confirm package names, service units, and syntax.

Do not modify or replace the bootloader, init system, disk layout, or encryption. Do not run unattended privileged/destructive commands. Preserve TTY recovery access and request approval before reboots or other disruptive actions. Do not commit secrets, passwords, or host-specific credentials to Git.

**Do not claim configuration is complete until the tests in `SETUP_PROMPT.md` pass.**
