# Windows Server RDS Learning Path 63 — Add a Second RD Session Host

**Level:** Expert · **Module:** 63/70

## Goal
Add `RDSH02` to the RDS deployment and existing collection with matching applications, policy and profile configuration.

## Setup
1. Build, patch, statically address and domain-join RDSH02.
2. Move it to the RDS Servers OU and validate the baseline GPO.
3. Add it to the RDS deployment as an RD Session Host.
4. Add it to `RDS-Lab-Desktop`.
5. Install identical applications and dependencies.
6. Apply certificate, profile and security settings.
7. Test a new session on each host and compare health/performance.

```powershell
Add-RDServer -Server 'RDSH02.corp.lab' -Role RDS-RD-SERVER `
 -ConnectionBroker 'RDS01.corp.lab'
Add-RDSessionHost -CollectionName 'RDS-Lab-Desktop' `
 -SessionHost 'RDSH02.corp.lab' -ConnectionBroker 'RDS01.corp.lab'
Get-RDSessionHost -CollectionName 'RDS-Lab-Desktop' `
 -ConnectionBroker 'RDS01.corp.lab'
```

## Evidence
Store build/patch state, deployment role, collection membership, application parity, sessions on both hosts and performance comparison under `evidence/`.

## Troubleshooting
If addition fails, verify DNS, secure channel, Broker reachability, pending reboot and role-installation state.

## Security
Apply the same hardening, LAPS, auditing and service-account standards before accepting users.

## Rollback
Drain RDSH02, remove it from the collection and deployment, then uninstall the role if required.

## Next
`Windows-Server-RDS-Learning-Path-64-Create-an-RDS-Session-Host-Farm`
