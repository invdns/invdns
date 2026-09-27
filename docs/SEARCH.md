# Search hosts from Terminal

Available in InvDNS 1.4.0. Keep InvDNS running and synchronize a source first.
Search reads the daemon's last completed in-memory snapshot. It does not scan
files, call GLPI/Zabbix, enable DNS or change conflict decisions.

First launch from `/Applications` attempts to install `invdns` in
`/usr/local/bin`. Complete native helper approval and check **Settings → Terminal
command**. No alias or shell-file changes are needed with the standard macOS PATH.

```bash
invdns search
invdns search web
invdns search group:nginx
invdns search group:nginx source:prod
invdns search ip:192.0.2.
invdns search status:conflict
invdns search --regex '^web-[0-9]+$'
invdns search group:nginx --output json
invdns search group:nginx --output csv
invdns search group:nginx --fields host,ip
invdns search --help
```

## Filters and output

- Plain text matches part of a host name/FQDN, case-insensitively.
- `group:` matches an exact, case-sensitive Ansible group name.
- `ip:` matches an address substring, not a CIDR range.
- `source:` matches part of the source display name or file basename.
- `status:` accepts `active`, `conflict`, `ignored` or `shadowed`.
- Multiple terms combine with AND. `--regex` instead uses the entire query as
  an explicit Go regular expression over host name/FQDN.

Default output is a table. `--output plain|json|csv` selects another format;
`--fields host,ip,source,groups,status` selects fields. Additional fields are
`hostname`, `source_id` and `source_path`. `--fields` alone defaults to plain text.

An active row contributes the chosen address to the loaded snapshot; it does
not mean the global Resolver switch is ON. Conflict rows are unresolved,
ignored rows are suppressed by a saved decision, and shadowed rows lost to
another selected address. Different source provenances may produce multiple rows.

## Groups 

Static INI groups and parent `:children` memberships, and structurally nested
YAML groups, are retained as metadata. The built-in `all` group is omitted.
Group-only references enrich an existing valid host; they never invent an IP.
This is not full Ansible variable inheritance or dynamic inventory execution.
GLPI/Zabbix records are searchable but have no Ansible group memberships.
After cache restore, host/IP rows may lack groups/source metadata until a
successful sync. A failed scan keeps the previous completed search snapshot.

Output can contain private hostnames, addresses, groups and source paths. Review
it before sharing. The examples above use documentation-only addresses.
