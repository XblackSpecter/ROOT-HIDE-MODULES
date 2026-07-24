# 🧩 TrickyStore Auto Filler

> *Automatically adds newly installed apps to TrickyStore's `target.txt` – zero manual work, zero duplicates.*

A lightweight module for Magisk / KernelSU / all forks that instantly detects new app installs and keeps your TrickyStore target list always up‑to‑date.

---

## ✨ Features

- **Real‑time monitoring** – detects new app installations within 3 seconds and appends the package name to `target.txt`.
- **No duplicates** – skips package names already present in the file.
- **Auto‑cleanup** – deletes `target.txt.bak` after each addition to force TrickyStore to reload.
- **Log rotation** – keeps log size under 100KB to prevent bloat.
- **Works on all Android versions** (tested on Android 16+).
- **Fully compatible with**:
  - Magisk
  - KernelSU
  - Wild KSU
  - ResukiSU Ultra
  - Sukisu
  - Flok Patch
  - All other KernelSU forks and derivatives.

---

## 📦 Requirements

- A rooted device with **Magisk**, **KernelSU**, or any compatible root manager.
- **TrickyStore** installed and configured (this module only auto‑fills `target.txt`; it does not install TrickyStore).

---

## 🚀 Installation

1. Download the latest `TrickyAutoFiller.zip` from the [Releases]](https://github.com/XblackSpecter/Android-root-hide/releases/tag/android-root-hide) page.
2. Open your root manager (Magisk / KernelSU / etc.).
3. Select **Install from storage** and choose the zip file.
4. Flash it and **reboot** your device.
5. Wait **30 seconds** after boot for the background service to start.

---

## ⚙️ How It Works

- After boot, a background service runs continuously and monitors the `/data/data/` directory for new app folders.
- When a new app is installed, the service:
  - Extracts the package name.
  - Checks if it already exists in `target.txt`.
  - If not, appends it and immediately deletes `target.txt.bak` to trigger TrickyStore's reload.
- Logs are written to `/data/adb/tricky_store/tricky.log` and automatically rotated.

> **Note:** This module does **not** scan or modify existing apps in `target.txt`. It only adds packages when they are first installed.

---

## 📁 File Locations

| File | Purpose |
|------|---------|
| `/data/adb/tricky_store/target.txt` | TrickyStore's target list (auto‑filled for new apps) |
| `/data/adb/tricky_store/tricky.log` | Service logs (rotated) |
| `/data/adb/tricky_store/.scanned` | Internal marker (for initial setup) |

---

## 🛠️ Troubleshooting

- **New apps not appearing** – Check the log:
  ```bash
  cat /data/adb/tricky_store/tricky.log
