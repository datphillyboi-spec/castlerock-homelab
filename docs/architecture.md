# Architecture and operating principles

High-level network architecture.

```mermaid
flowchart TD
  Internet["Internet / Verizon Fios"] --> ONT["Fios ONT"]
  ONT --> Gateway["UniFi Dream Machine Pro"]
  Gateway --> Switch["UniFi switching"]
  Switch --> Trusted["Trusted clients"]
  Switch --> IoT["IoT devices"]
  Switch --> Compute["CastleRock compute"]
  Switch --> Wireless["Wireless access points"]
```

## DNS availability

The existing portfolio documents a primary Pi-hole on a Raspberry Pi and a backup instance, using Keepalived and VRRP for a shared DNS endpoint. DNS response health checks provide a more useful signal than ping alone. DHCP remains a gateway responsibility.

## Monitoring independence

The main Uptime Kuma instance monitors services. A separate Raspberry Pi instance monitors CastleRock availability. This reduces dependence on the host being monitored, but it does not remove shared dependencies such as household power, switching, or the internet connection.

## Planned node expansion

| Planned node | Purpose |
| --- | --- |
| Plex media server | A dedicated node for media-server workloads |
| Proxmox backup server | A separate node for Proxmox backups |

The expansion will be built and configured from scratch, applying existing networking and systems knowledge to network configuration, storage, service deployment, monitoring, and recovery.
