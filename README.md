[README.md](https://github.com/user-attachments/files/29510573/README.md)
# System Performance Monitor

A lightweight **Windows desktop widget** that shows real‑time **CPU / GPU / RAM**
statistics in a small, borderless, always‑on‑top, draggable window. Built with
Rust + [iced](https://github.com/iced-rs/iced).

> ⬇️ **[Download the latest version](https://github.com/Elianazhuk/System-Performance-Monitor/releases/latest)** — run the `DesktopPerfMonitor.msi` installer.

## Features

- **Live metrics** — CPU, GPU and RAM usage, updated every second, with mini
  usage‑history charts.
- **Temperatures & power** — CPU/GPU temperature and power draw, read through a
  bundled headless sensor host.
- **More detail, all toggleable** — per‑core CPU load, GPU memory & clock, RAM
  speed.
- **Always on top**, borderless, **drag the header** to move it anywhere.
- **Adjustable transparency** and a compact **collapsed mini‑bar** mode.
- **15 languages** (English, Русский, 简体中文, 繁體中文, 日本語, 한국어, Deutsch,
  Français, Italiano, Português, Polski, Čeština, Українська, বাংলা, فارسی).
- **Built‑in auto‑update** — install new versions in one click (see below).

## Requirements

- Windows 10 / 11, 64‑bit.
- Administrator rights are requested **once** during installation (the
  temperature/power sensor needs a privileged helper).

## Installation

1. Download `DesktopPerfMonitor.msi` from the
   [latest release](https://github.com/Elianazhuk/System-Performance-Monitor/releases/latest).
2. Run it and approve the **UAC** prompt.
3. Launch **Desktop Performance Monitor** from the Start menu.

The installer puts the widget in `C:\Program Files\Desktop Perf Monitor\`, installs
a small **headless sensor host** (the LibreHardwareMonitor engine, with no window
and no tray icon) that reads CPU/GPU temperature & power, and registers a scheduled
task that starts it at logon.

> **"Unknown publisher" / SmartScreen.** The installer is not yet code‑signed, so
> Windows may show an "unknown publisher" or SmartScreen warning. Choose
> **More info → Run anyway** and approve the UAC prompt to continue.

## Auto‑update

The widget checks for a newer version on startup. When one is available:

1. A green badge appears on the gear icon and a banner **"Update available X.Y.Z"**
   shows on the dashboard.
2. Click **Update now** — the new installer is downloaded and its **SHA‑256** is
   verified.
3. Approve the **UAC** prompt; the widget installs the update and restarts itself
   on the new version automatically.

Auto‑checking can be turned off on the **About** screen.

**How it works:** the app reads [`update.json`](./update.json) from the root of this
repository, compares its `version` with the running build, and downloads the MSI
attached to the matching GitHub release.

## `update.json`

The current release is described by [`update.json`](./update.json) in the
repository root:

```json
{
  "version": "0.1.21",
  "url": "https://github.com/Elianazhuk/System-Performance-Monitor/releases/download/v0.1.21/DesktopPerfMonitor.msi",
  "sha256": "<lowercase SHA-256 of the MSI>",
  "notes": "Short changelog"
}
```

## Releasing a new version (maintainer)

1. Build `DesktopPerfMonitor.msi` from the source project (its version must be
   higher than the previous one) and compute its SHA‑256.
2. **Create a release** `vX.Y.Z` here and attach `DesktopPerfMonitor.msi` as a
   release asset (drag it into *Attach binaries* — do **not** commit the MSI to the
   repository; release assets allow up to 2 GB, repository file uploads only 25 MB).
3. **Edit `update.json`** in the `main` branch root with the new `version`, `url`
   (pointing to the `vX.Y.Z` asset) and `sha256`, then commit.

Order matters: publish the release first, then update `update.json`. The raw
manifest is cached by GitHub's CDN for ~5 minutes, so clients see a new version
shortly after.

## Credits & licenses

- **[LibreHardwareMonitor](https://github.com/LibreHardwareMonitor/LibreHardwareMonitor)**
  — hardware sensor readings (MPL‑2.0).
- **HidSharp** — device access (Apache‑2.0).
- **Rust** + **[iced](https://github.com/iced-rs/iced)** — application and UI.

Third‑party notices ship alongside the installer.

---

Made by **Eliana**.
