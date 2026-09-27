# InvDNS

### Inventory-powered local DNS for macOS

Turn hostnames from your static Ansible inventory, or connect GLPI and Zabbix into local DNS names.
Connect with `ssh admin@server01.inv` instead of looking up an IP address —
from Terminal or any application that uses macOS name resolution.

**macOS 13+ · Native menu bar app · Apple Silicon & Intel**

[Download](https://github.com/invdns/invdns/releases) ·
[Installation guide](docs/INSTALLATION.md) ·
[Report an issue](https://github.com/invdns/invdns/issues)

<img width="296" height="446" alt="image" src="https://github.com/user-attachments/assets/a0e7a3d7-24c8-466b-b63a-671f4359136f" />

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
curl server7.inv
```


## Made for your local inventory

- **Read the files you already have.** Static Ansible INI and YAML, including
  nested YAML groups. Select one file or scan a folder recursively, regardless
  of filenames or extensions.
- **Connect remote sources.** Import computers and IPv4 addresses from GLPI,
  or host names and IPv4 interfaces from Zabbix. 
- **Keep your inventory unchanged.** InvDNS reads hostname and IPv4
  `ansible_host` values without modifying the original files.
- **See conflicts before connecting.** If the same hostname has different
  addresses, InvDNS shows the conflict instead of choosing an address at random.
  Unresolved names are withheld from DNS.
- **Control it from the menu bar.** Switch Resolver ON/OFF, sync your sources,
  inspect conflicts and open Settings without leaving your workflow.
- **Choose your local namespace.** Use the default `.inv` suffix or configure
  your own zone, loopback listen address, port and DNS TTL.
- **Search from Terminal.** Find loaded hosts by name, IP, source, status or
  Ansible group. Export selected fields as plain text, JSON or CSV without
  triggering another inventory scan.
No Ansible, Python or separate DNS-server installation is required.

## Install in a few steps

1. Download `InvDNS-1.4.0-macOS.dmg` from
   [Releases](https://github.com/invdns/invdns/releases).
2. Open the DMG and drag **InvDNS.app** to **Applications**.
3. Launch InvDNS from Applications and open its menu bar icon.
4. In **Sources**, add your inventory file or folder, then choose **Sync Now**.
5. Click **Resolver OFF** to enable DNS. If macOS requests background-helper
   approval, complete it and follow the app's instructions to retry.

The installer contains **1.4.0**. The app and DMG are signed with
Apple Developer ID and notarized by Apple. A `SHA256SUMS` file accompanies the
download for integrity checks.

## Find a host without leaving Terminal

With InvDNS running and a source synchronized:

```bash
invdns search server
invdns search group:nginx
invdns search source:prod --output json
invdns search group:nginx --fields host,ip
```

Search uses the last loaded snapshot. It does not contact remote sources or
change DNS settings. [Search guide](docs/SEARCH.md).

## Free, Trial and Pro

**Free** gives you local DNS from one active inventory file or folder, with
recursive scanning, manual sync, caching and conflict detection. It does not expire.

**Pro** adds multiple sources, automatic file watching, scheduled synchronization,
source priorities, saved conflict decisions and GLPI/Zabbix sources.

The **14-day Trial** lets you try Pro capabilities. When it ends, InvDNS returns
to Free and preserves your configuration. Additional sources and Pro settings
remain stored but inactive under Free.

To obtain a license, please write to us by email:[invdnspro@gmail.com](mailto:invdnspro@gmail.com).

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
- [Terminal search](docs/SEARCH.md)
- [1.4.0 release notes](docs/RELEASE_NOTES_1.4.0.md)
- [Changelog](CHANGELOG.md)
- [Issues](https://github.com/invdns/invdns/issues)

When reporting a problem, include the app version, macOS version, processor type
and steps to reproduce. Remove sensitive information from screenshots and logs;
never post credentials, license tokens or private inventory data.

---

[Proprietary notice](LICENSE.md) · [Third-party notices](THIRD_PARTY_NOTICES.md)
