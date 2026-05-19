# MeshChat — Meshtastic client for Kindle & e-ink browsers

A lightweight, zero-dependency web chat client for [Meshtastic](https://meshtastic.org/) mesh networks, designed to work on Kindle browsers and other e-ink devices with limited JavaScript support.

Connects to your local [MeshMonitor (Yeraze)](https://github.com/Yeraze/meshmonitor) instance via its REST API.

---

## Features

- Works on Kindle experimental browser (e-ink optimized)
- No frameworks, no animations — pure HTML + vanilla JS
- Auto-detects your Meshtastic sources and channels
- Send & receive messages
- Polling every 10 seconds with countdown
- Remembers your config across the session

## Requirements

- [MeshMonitor by Yeraze](https://github.com/Yeraze/meshmonitor) running on your local network
- A MeshMonitor API token (generated in MeshMonitor → User Settings → API Token)
- Home Assistant (for the addon install method)

---

## Installation

### Option A — Home Assistant Addon (recommended)

1. In Home Assistant, go to **Settings → Add-ons → Add-on Store**
2. Click the three-dot menu → **Repositories**
3. Add: `https://github.com/alterbarteq/meshchat-ha`
4. Find **MeshChat Kindle** and install it
5. Start the addon
6. Open the Web UI — it runs on port **8765**

On your Kindle, open:
```
http://homeassistant.local:8765
```

### Option B — HA /local/ folder (no addon needed)

1. Copy `mesh-kindle-chat/index.html` to `/config/www/meshchat.html` on your HA instance
2. Open on Kindle:
```
http://homeassistant.local:8123/local/meshchat.html
```

### Option C — Any static file server

Serve `index.html` from any HTTP server on your local network. HTTPS is not recommended (causes mixed-content issues when connecting to a local HTTP MeshMonitor instance).

---

## Configuration

On first open, you'll see a setup screen. Enter:

| Field | Example | Description |
|-------|---------|-------------|
| MeshMonitor URL | `http://homeassistant.local:8099` | Local address of your MeshMonitor |
| API Token | `mm_v1_abc123...` | Generated in MeshMonitor User Settings |
| Callsign / Nick | `SQ5ABC` | Optional — highlights your own messages |

Config is saved in `sessionStorage` — you'll need to re-enter it if you close the browser tab.

---

## Why e-ink optimized?

Kindle and similar e-ink devices have:
- Slow screen refresh (~300-500ms, causes "flash" on full redraw)
- Weak processors (ARM Cortex-A class)
- Outdated WebKit browsers with limited CSS/JS support

This client avoids: animations, transitions, flexbox-heavy layouts, WebSockets (not supported on Kindle), and modern CSS features. It uses simple polling instead of live push.

---

## Compatibility

| Device | Status |
|--------|--------|
| Kindle (experimental browser) | ✅ Tested |
| Desktop browser | ✅ Works |
| Mobile browser | ✅ Works |
| PocketBook | 🔲 Untested |
| Kobo | 🔲 Untested |

---

## MeshMonitor API

This client uses [MeshMonitor v4+ REST API](https://meshmonitor.org/development/api.html):

```
GET  /api/v1/sources
GET  /api/v1/sources/{sourceId}/channels
GET  /api/v1/sources/{sourceId}/messages?limit=50&channel=0
POST /api/v1/sources/{sourceId}/messages
```

Authentication: `Authorization: Bearer mm_v1_<token>`

---

## Contributing

PRs welcome. Key areas for improvement:
- Direct Message support
- Node list view
- Better field name detection across MeshMonitor versions
- MeshCore-specific features

---

## License

MIT

---

*Not affiliated with Meshtastic or MeshMonitor projects.*
