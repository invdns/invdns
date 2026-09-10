# Troubleshooting

## No icon after copying the app

Launch InvDNS from Applications. Copying it out of the DMG does not launch it.
InvDNS appears in the menu bar rather than the Dock. For later logins, check
**Settings → Launch InvDNS at Login** and any macOS approval request.

## Resolver needs attention, unavailable, or will not turn off

Open Settings and read the specific error. Orange is not a successful OFF state.
Check the InvDNS background-item approval in macOS System Settings and ensure
you are running the current official app from Applications, not the DMG or a
second copy. Retry the action after addressing the reported problem.

Do not manually delete system resolver files or broadly reset macOS service
registrations. If it persists, report the exact error and reproduction steps
without disclosing private configuration or credentials.

## Save Resolver Settings is disabled

Saving requires a connected daemon, a confirmed OFF state with the system route
removed, valid fields, and no resolver operation in progress. Successfully use
**Disable Resolver** first. If it fails, resolve the displayed error before saving.

## A host does not resolve

Check that Resolver is ON, the source is enabled/readable and **Sync Now** succeeds.
The entry must have a valid IPv4 `ansible_host`; dynamic expressions are not
executed. Check Conflicts: an unresolved conflicting hostname is not published.
In Free, only one configured local source contributes records.

For a host named `server01` in the default `.inv` zone, inspect the answer directly:

```bash
dig @127.0.0.1 -p 53535 server01.inv A
```

This queries InvDNS directly, not macOS split-DNS routing. Substitute your actual
port and suffix if changed. A direct answer alone does not prove system routing
is configured. `ping server01.inv` uses system resolution, though hosts may block
ICMP replies. VPN or network reachability is separate from DNS resolution.

## Changes are not visible immediately

In Free, run **Sync Now**. During Trial/Pro, enable watching or periodic
reconciliation if desired. Downstream applications may retain DNS answers until
their cache expires; TTL and synchronization interval are different settings.

## Verify the download

Put the official DMG and `SHA256SUMS` together in a folder, open Terminal in that
folder and run:

```bash
shasum -a 256 -c SHA256SUMS
```

The DMG must report `OK`. If the hash differs, do not install it; download again
from the official release. A checksum checks file integrity; the Developer ID
signature and notarization are separate macOS security checks.

## Reporting a bug

Use [Issues](https://github.com/invdns/invdns/issues) for non-sensitive reports.
Include version/build, macOS version, Apple Silicon or Intel, exact steps,
expected behavior and the displayed error. Review screenshots and logs before
posting. Remove real hostnames, IPs, usernames, inventory paths and secrets;
never post a license token or password. Do not disclose sensitive vulnerability
details in a public issue.
