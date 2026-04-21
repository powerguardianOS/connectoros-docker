# PowerGuardian Connector OS — Docker

Docker image for the PowerGuardian Connector agent. Runs on any machine with a UPS connected and reports to your PowerGuardian Controller over WebSocket.

**Image:** `ghcr.io/powerguardianos/connectoros-docker:latest`  
**Platforms:** `linux/amd64` · `linux/arm64` · `linux/arm/v7`

---

## Quick start

```bash
docker compose up -d
```

Open `http://<host-ip>:8090` to configure the connector — point it to your controller and go through the adoption flow.

---

## Volumes

| Path | Description |
|---|---|
| `/data` | Agent config and persistent state |
| `/etc/nut` | NUT config (optional, mount from host if NUT daemon is running) |

---

## OTA updates

Trigger an update from the controller UI:  
**Connectors → select connector → Command → UPDATE_DOCKER**

Or pull manually:

```bash
docker compose pull && docker compose up -d
```

---

## Source

Built automatically from [powerguardian-connector-os](https://github.com/powerguardianOS/powerguardian-connector-os) on every push to `master`.
