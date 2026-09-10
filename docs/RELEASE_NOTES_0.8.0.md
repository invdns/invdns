# InvDNS 0.8.0

Turn your infrastructure inventory into local DNS.

This release packages **0.8.0** for **macOS 13 or later**, with both
**Apple Silicon (arm64)** and **Intel (x86_64)** support in the same DMG.

## Highlights

- Static local Ansible INI/YAML inventories exposed through `.inv` or a custom suffix.
- Native menu bar ON/OFF control, Sources, Conflicts and editable Settings.
- Local DNS with one file/folder and automatic synchronization upon file changes.
- Launch at login and coordinated GUI/daemon shutdown.
- Correct Quit behavior with Settings, Sources or Conflicts windows open.

## Install

Download `InvDNS-0.8.0-macOS.dmg`, open it, drag InvDNS to Applications and launch
it there. Add a source and enable Resolver; complete macOS helper approval if
requested. For an update, quit the old app first and replace it without uninstalling.

The app and DMG are Developer ID signed, Apple-notarized and stapled. Gatekeeper
accepted this artifact. `SHA256SUMS` accompanies the installer.

```text
9fb042c9729fc3c0e2807cf714e7fbd22aa3846538b25e0e5dc1ad1475256f1d  InvDNS-0.8.0-macOS.dmg
```

Also download `THIRD_PARTY_NOTICES.md` and `InvDNS-0.8.0-third-party-licenses.zip`
for the accompanying dependency notices and license texts.
