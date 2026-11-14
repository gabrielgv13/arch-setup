# Arch Linux — Complete Post-Installation Setup

You are a Linux system administrator responsible for configuring my freshly installed minimal Arch Linux system.

Your task is to transform this installation into a lightweight, stable, fully functional development workstation.

**Hardware:** Dell Latitude 7490, Intel CPU and integrated graphics.

**Current state:** Arch Linux installed through archinstall, minimal profile, GRUB bootloader, NetworkManager, and basic development packages. Codex CLI is already installed and authenticated.

**Target environment:** Labwc (Wayland), Firefox, Visual Studio Code, Docker Engine, PostgreSQL 18, Python, UV, Node.js and Git.

## Core operating rules

1. **Actually execute the installation and configuration**, not merely provide instructions.
2. Inspect the existing system before modifying anything.
3. Work through the phases below sequentially.
4. Verify each phase before continuing.
5. Use official Arch Linux repositories whenever possible.
6. Consult current ArchWiki, upstream documentation and installed manual pages when uncertain. Never invent package names, configuration syntax or command options.
7. Do not install unnecessary dependencies or heavyweight desktop environments.
8. Keep the existing Arch installation, bootloader, partitions, encryption and init system intact.
9. Never format disks, overwrite user data or make destructive changes.
10. Back up existing configuration files before modifying them.
11. Request approval for privileged operations, security-sensitive changes and reboots.
12. Never bypass sandbox protections or use unrestricted Codex execution.
13. Maintain a persistent checklist and installation log in `~/system-setup/`.
14. Do not stop after generating a plan. Continue executing each approved phase until the setup is complete or user intervention is genuinely necessary.

---

## Phase 1 — Inspect and prepare the system

Collect and report:

- CPU model, core and thread count.
- Total RAM and available memory.
- Storage devices, partitions, filesystem and free space.
- GPU and graphics drivers.
- Wi-Fi, Bluetooth and Ethernet adapters.
- Current kernel, bootloader and enabled services.
- Installed packages and currently configured swap/zram.
- Active network connection and DNS functionality.

Use standard Linux utilities such as `lscpu`, `free`, `lsblk`, `lspci`, `ip` and `systemctl`.

Check the system for obvious configuration problems.

Create:

- `~/system-setup/README.md` — overall installation status.
- `~/system-setup/checklist.md` — phase-by-phase checklist.
- `~/system-setup/changes.md` — packages, services and configuration changes.

Make a short implementation plan based on the hardware detected.

## Phase 2 — Install Labwc and the graphical environment

Install and configure a lightweight Wayland desktop.

Required components:

| Component | Preferred software |
|---|---|
| Wayland compositor | Labwc |
| Display manager | greetd + tuigreet |
| Status bar | Waybar |
| App launcher | Fuzzel |
| Terminal | Foot |
| File manager | Thunar |
| Wallpaper | swaybg |
| Notifications | mako |
| Screen locking | swaylock or compatible alternative |
| Idle management | swayidle |
| Authentication | Polkit agent |
| Clipboard | wl-clipboard |
| Screenshots | grim + slurp |
| Legacy application support | XWayland |
| Desktop portals | Appropriate XDG desktop portals |

Ensure that session management, D-Bus, Polkit and the Wayland environment work correctly.

**Implementation order:**

1. Install Labwc and a terminal.
2. Configure a working terminal shortcut.
3. Test Labwc directly from the TTY.
4. Configure the application launcher and Waybar.
5. Configure session environment and autostart.
6. Install and configure greetd.
7. Enable the display manager only after confirming that Labwc starts correctly.

Do not leave the system unable to access a working TTY.

Use a clean, minimal dark theme.

## Phase 3 — Configure desktop multitasking

I want a practical desktop optimized for browser-based research, coding and containers.

Configure four workspaces:

- **Workspace 1 — Development:** VS Code and terminal.
- **Workspace 2 — Browser:** Firefox and documentation.
- **Workspace 3 — Containers:** Docker and terminal tools.
- **Workspace 4 — Database:** PostgreSQL administration.

Implement keyboard shortcuts:

| Shortcut | Action |
|---|---|
| Super + Enter | Open Foot |
| Super + D | Open Fuzzel |
| Super + Q | Close focused window |
| Super + 1–4 | Switch workspaces |
| Super + Shift + 1–4 | Move window to workspace |
| Super + Left/Right | Snap window left/right |
| Print Screen | Screenshot |
| Super + L | Lock session |

Verify Labwc's exact supported configuration syntax before writing the bindings.

Configure Waybar to show:

- Workspaces
- CPU usage
- Memory usage
- Network status
- Battery percentage
- Audio volume
- Date and time

Prioritize functionality and readability over decorations or animations.

## Phase 4 — Configure laptop hardware

Configure hardware support specifically for the detected Dell Latitude 7490.

Requirements:

- Intel integrated graphics acceleration.
- Wi-Fi and Bluetooth.
- PipeWire audio.
- Laptop speakers, headphones and microphone.
- Brightness and volume keys.
- Touchpad functionality.
- Battery monitoring.
- Suspend and resume.
- Lid-close behavior.
- CPU thermal and power management.

Use an appropriate power-management solution, avoiding conflicting services.

Enable periodic SSD TRIM where supported.

Inspect existing swap/zram before making changes. Configure memory compression only if necessary and size it according to the detected RAM.

Do not enable aggressive power-saving features that could negatively affect development performance.

Any suspend, resume, lid-close or reboot test that might interrupt this Codex session must be explicitly approved by the user.

## Phase 5 — Install the development environment

Install and configure:

**Programming**
- Python 3 and UV.
- Node.js and npm.
- Git and GitHub CLI.
- pip, if required.
- Build tools and compilers.
- SSH client.
- curl, wget, jq, ripgrep and fd.

**Applications**
- Firefox.
- Visual Studio Code.
- A graphical archive manager if appropriate.

Prefer the official Arch repository's `code` package initially. Explain the differences between Code - OSS and Microsoft's official VS Code build before installing any AUR or third-party package.

Do not install redundant runtimes or version managers without a concrete need.

Configure Git's basic environment, but ask for the user's name and email instead of inventing them.

Ensure Python/UV virtual environments and Node.js projects can be created successfully.

Run simple smoke tests for Python, UV, Node.js, npm and Git.

## Phase 6 — Configure Docker

Install Docker Engine and Docker Compose.

Do not install Docker Desktop.

Requirements:

1. Configure the Docker daemon.
2. Enable appropriate service startup.
3. Verify Docker with a test container.
4. Verify Docker Compose.
5. Check container networking.
6. Check persistent storage.
7. Inspect Docker's memory consumption.

Explain the security implications before adding my user to the `docker` group. Obtain my approval before doing so.

Prefer standard Docker configurations without unnecessary modifications to the daemon.

## Phase 7 — PostgreSQL development environment

Configure PostgreSQL 18 using Docker Compose.

Requirements:

- PostgreSQL 18 container.
- Persistent named volume.
- Dedicated development database and credentials.
- Database accessible only through `127.0.0.1:5432`.
- No publicly exposed database port.
- Restart policy appropriate for a development laptop.
- A local `.env` file for database credentials.
- `.gitignore` excluding credentials and other secrets.

Verify the correct persistent data directory for the PostgreSQL 18 Docker image being used.

Never hardcode passwords in tracked files.

Ask me to provide or generate a database password securely.

Test:

1. Container startup.
2. Connection through `psql`.
3. Table creation.
4. INSERT and SELECT operations.
5. Data persistence after container restart.
6. Clean container shutdown.

Install a lightweight graphical SQL client or configure a VS Code PostgreSQL extension, whichever adds less unnecessary overhead.

Do not install a second PostgreSQL server directly on the host unless there is a demonstrated need.

## Phase 8 — Optimize multitasking and resource usage

The primary workload is:

- Firefox with multiple tabs.
- VS Code.
- Python/Flask/FastAPI development.
- Docker containers.
- PostgreSQL.
- Multiple terminal sessions.

Optimize this environment based on the actual RAM and CPU specifications.

Focus on:

- Low idle resource consumption.
- Reasonable memory management.
- Fast application launching.
- Smooth window switching.
- Stable container operation.
- Responsive browser and editor performance.
- Good laptop battery life.

Avoid unnecessary background daemons.

Do not apply speculative sysctl tweaks, aggressive memory limits or kernel modifications without measurements showing that they help.

Measure memory consumption before and after the installation.

## Phase 9 — Final system verification

Perform a complete validation.

Check that:

- Labwc starts correctly.
- greetd login works.
- Terminal and launcher shortcuts work.
- All four workspaces function.
- Waybar displays useful system information.
- Firefox and VS Code launch.
- Audio and brightness controls work.
- Wi-Fi and networking remain functional.
- Docker runs containers.
- PostgreSQL accepts connections and retains data.
- Python, UV, Node.js and npm work.
- zram/swap is operational as intended.
- No essential system services are failing.

Request permission before performing the final reboot.

After reboot, verify that the login manager, desktop and required background services start correctly.

## Final deliverables

Update the files in `~/system-setup/` with:

1. Complete package installation list.
2. Configurations created or modified.
3. Enabled services.
4. Test results.
5. Known limitations.
6. Recommended future improvements.
7. Instructions for restoring or troubleshooting important components.

Provide a final report comparing the initial and final memory usage.

## Execution instructions

**Start working immediately.**

First inspect the installed system and create the setup files. Then implement the phases in order.

For each phase:

1. State what you are about to change.
2. Request approval when required.
3. Perform the installation and configuration.
4. Execute relevant tests.
5. Record the result.
6. Continue to the next phase.

If an error occurs, diagnose it and attempt a safe correction. Do not blindly retry commands or proceed with broken dependencies.

The final result must be a working Labwc-based Arch Linux development workstation, not just a set of unexecuted setup scripts.
