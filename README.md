# DualKernel

**A dual Linux and UNIX workstation simulator in your browser.** DualKernel pairs a modern Arch Linux / Hyprland-inspired desktop with a classic UNIX System V workstation. Switch kernels instantly while keeping one shared virtual filesystem.

**Live demo:** [https://lovemsf.github.io/dual-kernel/](https://lovemsf.github.io/dual-kernel/)

## Start locally

Requires Node.js 22 or later.

```sh
npm install --legacy-peer-deps
npm run dev
```

## The dual-kernel switcher

Use the **KERNEL SWITCH: ARCH LINUX ⇄ UNIX SVR4** control at the top of the desktop. Its short transition represents changing the syscall table and userland. Linux mode presents a dark, dot-grid Wayland desktop with a Waybar-style status strip, workspace indicators, telemetry, and a floating dock. UNIX mode uses a beveled, classic workstation palette, monochrome title bars, a release badge, and a traditional application dock.

The switch changes the simulated environment: shell prompt, system identity, process labels, desktop chrome, and monitor labels. It does not change the underlying VFS.

## Desktop apps

- **Terminal** — simulated zsh in Linux and csh in UNIX. Use Up/Down for command history and `>` / `>>` to write or append output to VFS files. `|` chains commands. Tab completion is available for common commands and paths.
- **Files** — browse shared home, system configuration, logs, and binaries. Open an item to edit it. Double-click directories or use the sidebar shortcuts to navigate.
- **Text Editor** — edit and save plain text files directly to the shared VFS.
- **System Monitor** — live simulated CPU and memory readings, an updating activity graph, a process list, and a recent filesystem syscall.
- **Architecture Diff** — compare Linux and UNIX across kernel design, filesystem families, and shells.

### Terminal commands

`help`, `ls`, `ll`, `cd`, `pwd`, `cat`, `touch`, `mkdir`, `rm`, `echo`, `uname -a`, `neofetch`, `ps`, `top`, `whoami`, `date`, `history`, `man`, `cmatrix`, and `clear`.

Examples:

```sh
mkdir projects
echo "shared across kernels" > projects/hello.txt
cat projects/hello.txt
uname -a
```

The terminal is a safe simulation. It only changes files in DualKernel’s virtual filesystem; it does not run commands on your computer.

## Shared VFS

The VFS is a path-to-text map in React state, persisted in browser `localStorage` under `dualkernel-vfs`. Both OS modes read and write the same map. The initial tree includes sample files under `/home/user`, `/etc`, `/var/log`, `/usr/bin`, and `/tmp`. The **RESET FS** control restores the starter tree. Browser storage must be enabled for changes to persist between page loads.

## Tech stack

React, Vite, TypeScript, Tailwind CSS, Framer Motion, and Lucide icons.

## GitHub Pages deployment

The Vite config uses a relative `base: './'` for project Pages hosting. The workflow in `.github/workflows/deploy.yml` builds with Node 22 and deploys the `dist` directory when changes are pushed to `main` (or when manually started). Enable **GitHub Pages → Build and deployment → GitHub Actions** in repository settings. The configured project URL is `https://lovemsf.github.io/dual-kernel/`.

## Scripts

- `npm run dev` — local Vite development server
- `npm run typecheck` — TypeScript project checks
- `npm run build` — TypeScript checks and production Vite build
- `npm run preview` — preview the production build locally
