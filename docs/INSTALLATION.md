# Installation and usage

## Requirements

- macOS 13 or later, Apple Silicon or Intel.
- A local static Ansible INI or YAML inventory with IPv4 `ansible_host` values.
- Permission to approve the InvDNS background helper when macOS requests it.

No separate runtime or command-line dependencies are needed.

## Install

1. Download the DMG from the [official releases](https://github.com/invdns/invdns/releases).
2. Open it and drag **InvDNS.app** onto **Applications**.
3. Launch `/Applications/InvDNS.app`, then eject the installer volume.
4. Use the menu bar icon to open **Sources** and add a file or folder.
5. Choose **Sync Now**, then click **Resolver OFF** to enable name resolution.

Copying the app does not start a daemon or change system DNS. On first launch,
InvDNS creates its private user directories and starts its bundled user daemon.
Enabling Resolver installs the system DNS route through the privileged helper.

If macOS requests background-service approval, open the indicated System Settings
page (General → Login Items, or Login Items & Extensions on some macOS versions),
allow the InvDNS item and return to the app. Follow its instructions to retry.
Do not disable Gatekeeper or remove quarantine attributes to install the release.

## Resolver states

- **Green — Resolver ON:** runtime answers and the system route are confirmed active.
- **Red — Resolver OFF:** runtime answers are disabled and the system route is absent.
- **Orange — Resolver needs attention:** runtime and system routing are inconsistent;
  inspect the error in Settings.
- **Neutral — Resolver unavailable:** the app cannot confirm daemon availability.

Click the single resolver row to switch ON/OFF. The app waits for confirmation
and blocks repeated clicks during the operation. A failed operation is reported;
the row is not an optimistic indication of success.

## Settings

To change zone, loopback address, port or TTL:

1. Open **Settings** and successfully **Disable Resolver**.
2. Edit the fields and choose **Save Resolver Settings**.
3. Enable Resolver to install the new system route.

Save remains unavailable until OFF and route removal are confirmed. The port
must be 1–65535, TTL 1–86400 seconds, and listen address a loopback address.
TTL controls how long DNS clients may cache an answer; it is not the sync interval.

**Watch inventory changes** refreshes on local file changes.
**Periodic reconciliation** rescans on the selected schedule.
Both are Trial/Pro features; **Sync Now** remains available in Free.

Use **Launch InvDNS at Login** to control startup. The app enables login startup
on its first canonical Applications installation, subject to macOS approval,
and respects later changes. The GUI starts its user-daemon session at launch.

## Quit and update

**Quit InvDNS** safely removes managed DNS routes, stops the user daemon and closes
all InvDNS windows. It preserves configuration, sources, cache and license state.
If cleanup fails, the app stays open and reports the error so you can retry.

To update, quit successfully, copy the new app from its DMG to Applications,
confirm replacement and launch it from Applications. Do not use Uninstall for
an ordinary update: Uninstall deletes InvDNS user data.

## Full uninstall

From the app installed in Applications, choose
**Settings → Uninstall InvDNS…**, read the warning and confirm.

The uninstall flow removes InvDNS-managed DNS routes, unregisters its services
and login item, deletes InvDNS configuration, cache, logs, preferences and local
license activation, then moves the app to Trash. macOS may require approval.
External original inventory files and resolver files owned by other software
are preserved. If a cleanup step fails, the app remains for retry.

Deleted user data is not recoverable through the app; keep any backup you need
before confirming. Retain your Pro license separately before removing activation.
Dragging the app to Trash alone is not a full uninstall.

## Local data

Configuration and supporting state are under:

```text
~/Library/Application Support/InvDNS/
~/Library/Caches/InvDNS/
~/Library/Logs/InvDNS/
```

License/trial state is stored in the current user's macOS Keychain.
Prefer GUI settings changes. To read the config in Terminal, quote its path:

```bash
cat "$HOME/Library/Application Support/InvDNS/config.yaml"
```

Do not upload the output publicly: it may reveal private infrastructure paths.
