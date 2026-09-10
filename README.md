# InvDNS

### Inventory-powered local DNS for macOS

Turn hostnames from your static Ansible inventory into local DNS names.
Connect with `ssh admin@server01.inv` instead of looking up an IP address —
from Terminal or any application that uses macOS name resolution.

**macOS 13+ · Native menu bar app · Apple Silicon & Intel**

[Download](https://github.com/invdns/invdns/releases) ·
[Installation guide](docs/INSTALLATION.md) ·
[Report an issue](https://github.com/invdns/invdns/issues)

## From inventory to DNS

Add a local inventory file or folder:

```ini
[servers]
server01 ansible_host=192.0.2.10
database01 ansible_host=192.0.2.20
```

Sync it, enable Resolver, and use the names:

```bash
ssh admin@server01.inv
ping database01.inv
```

The addresses above are examples. Use your actual host addresses and connect
to the appropriate network or VPN — InvDNS resolves names; it does not provide
network access.

## Made for your local inventory

- **Read the files you already have.** Static Ansible INI and YAML, including
  nested YAML groups. Select one file or scan a folder recursively, regardless
  of filenames or extensions.
- **Keep your inventory unchanged.** InvDNS reads hostname and IPv4
  `ansible_host` values without modifying the original files.
- **See conflicts before connecting.** If the same hostname has different
  addresses, InvDNS shows the conflict instead of choosing an address at random.
  Unresolved names are withheld from DNS.
- **Control it from the menu bar.** Switch Resolver ON/OFF, sync your sources,
  inspect conflicts and open Settings without leaving your workflow.
- **Choose your local namespace.** Use the default `.inv` suffix or configure
  your own zone, loopback listen address, port and DNS TTL.

No Ansible, Python or separate DNS-server installation is required.

## Install in a few steps

1. Download `InvDNS-0.8.0-macOS.dmg` from
   [Releases](https://github.com/invdns/invdns/releases).
2. Open the DMG and drag **InvDNS.app** to **Applications**.
3. Launch InvDNS from Applications and open its menu bar icon.
4. In **Sources**, add your inventory file or folder, then choose **Sync Now**.
5. Click **Resolver OFF** to enable DNS. If macOS requests background-helper
   approval, complete it and follow the app's instructions to retry.

The installer contains **0.8.0**. The app and DMG are signed with
Apple Developer ID and notarized by Apple. A `SHA256SUMS` file accompanies the
download for integrity checks.

Both Apple Silicon and Intel binaries are included. Physical Intel-Mac testing
has not yet been completed; validation details are in the
[release notes](docs/RELEASE_NOTES_0.8.0.md).

## Local DNS, integrated with macOS

InvDNS serves IPv4 DNS records from memory and keeps a persistent
last-known-good cache. macOS routes queries for your configured suffix to
InvDNS through split DNS; your normal DNS servers remain unchanged.

The default endpoint is `127.0.0.1:53535`, with a 30-second TTL.
The application and DNS daemon run as your user. A narrowly scoped privileged
helper handles the system resolver route.

Enable **Launch InvDNS at Login** in Settings to start with your session.
**Quit InvDNS** removes its managed DNS routes and stops the user daemon before
closing its windows. Your settings remain available for the next launch.

For full removal, use **Settings → Uninstall InvDNS…**. Review the confirmation:
it deletes InvDNS data and local license activation while preserving your
original inventory files.

## Help and documentation

- [Installation, settings, updates and uninstall](docs/INSTALLATION.md)
- [Troubleshooting and download verification](docs/TROUBLESHOOTING.md)
- [Changelog](CHANGELOG.md)
- [Issues](https://github.com/invdns/invdns/issues)

When reporting a problem, include the app version, macOS version, processor type
and steps to reproduce. Remove sensitive information from screenshots and logs;
never post credentials, license tokens or private inventory data.

---

InvDNS is proprietary software. This repository contains public documentation
and release materials, not the application's source code.

[Proprietary notice](LICENSE.md) · [Third-party notices](THIRD_PARTY_NOTICES.md)
