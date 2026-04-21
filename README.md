# PowerGuardian Connector OS — Docker

Docker image for the PowerGuardian Connector agent. Runs on any machine with a UPS connected and reports to your PowerGuardian Controller over WebSocket.

**Image:** `ghcr.io/powerguardianos/connectoros-docker:latest`  
**Platforms:** `linux/amd64` · `linux/arm64` · `linux/arm/v7`

---

## Quick start

```bash
cp .env.example .env
# Edit .env — set PG_CONTROLLER_URL and PG_AGENT_KEY
docker compose up -d
```

Web GUI available at `http://<host-ip>:8090`

---

## Configuration

| Variable | Description |
|---|---|
| `PG_CONTROLLER_URL` | WebSocket URL of your controller, e.g. `ws://10.0.0.40:8181/agent` |
| `PG_AGENT_KEY` | Agent token from the controller adoption page |
| `PG_WATCHTOWER_URL` | Set automatically by docker-compose — do not change |
| `PG_WATCHTOWER_TOKEN` | Shared secret between connector and Watchtower |

> Use the controller's **IP address**, not `powerguardian.local` — mDNS does not resolve inside Docker.

---

## OTA updates

The `docker-compose.yml` includes a [Watchtower](https://containrrr.dev/watchtower/) sidecar. It checks for a new image every 24 hours automatically. You can also trigger an update immediately from the controller UI:

**Controller → Connectors → select connector → Command → UPDATE_DOCKER**

---

## NUT (Network UPS Tools)

The container includes `nut-client`. To use an existing NUT daemon on the host, mount the config:

```yaml
volumes:
  - /etc/nut:/etc/nut
```

This is already included in the provided `docker-compose.yml`.

---

## Volumes

| Path | Description |
|---|---|
| `/data` | Agent config and persistent state |

---

## Source

Built automatically from [powerguardian-connector-os](https://github.com/powerguardianOS/powerguardian-connector-os) on every push to `master`.
