# InvDNS 1.4.0

Turn your infrastructure inventory into local DNS — and search it from Terminal.

**Version 1.4.0 · Build 8 · macOS 13+ · Apple Silicon and Intel**

## Highlights

- Static local Ansible INI/YAML files and recursive folders, with configurable
  local DNS, conflict handling and a native menu bar interface.
- GLPI computer names and IPv4 addresses through the GLPI REST API.
- Zabbix host names and IPv4 interfaces. GLPI and Zabbix
  require Trial/Pro and store tokens in macOS Keychain.
- Read-only `invdns search`: host/IP/source/status filters, Ansible groups,
  explicit regular expressions, plain-text, JSON and CSV output.
- First-launch terminal command installation, with approval, status/retry in
  Settings and cleanup during uninstall. No shell startup files are modified.

Free remains usable with one active local source and manual synchronization.
The 14-day Trial enables Pro capabilities; expiration preserves configuration.

## Install or update

Download `InvDNS-1.4.0-macOS.dmg`, open it, drag **InvDNS.app** to **Applications**
and launch it there. Complete macOS helper approval if requested. Configure a
source, synchronize it and enable Resolver.

For an update, **Quit InvDNS** first, replace the app and relaunch. Do not
uninstall for an ordinary update: uninstall deletes InvDNS user data.

With the app running and a source synchronized.
