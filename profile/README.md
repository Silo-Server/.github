# Silo

**Self-hosted media streaming, built on a modern stack.**

Silo is an open-source media server with a Go backend and a React web UI. It
handles direct play, remuxing, and hardware-accelerated transcoding, and speaks
a Jellyfin-compatible API — so existing Jellyfin clients like Findroid and
Infuse work out of the box, alongside first-party native apps for Apple and
Android.

[Website](https://siloserver.org) · [Server & docs](https://github.com/Silo-Server/silo-server)

---

## Why Silo

- **Modern infra** — Go + PostgreSQL + Redis, up and running with one `docker compose up`.
- **Plays your media** — direct play, remux, and hardware-accelerated transcoding via FFmpeg.
- **Jellyfin-compatible** — built-in compatibility layer, plus first-party native apps for Apple and Android.
- **Extensible** — a public plugin SDK with protobuf contracts for metadata providers and more.

## Project map

### Server
| Repo | What it is |
|---|---|
| [silo-server](https://github.com/Silo-Server/silo-server) | The media server — Go backend, React web UI, transcoding, Jellyfin-compatible APIs. |

### Clients
| Repo | Platforms |
|---|---|
| [silo-apple](https://github.com/Silo-Server/silo-apple) | iOS, tvOS, macOS (Swift) |
| [silo-android](https://github.com/Silo-Server/silo-android) | Android phone & Android TV (Kotlin) |

### Plugins
| Repo | What it is |
|---|---|
| [silo-plugin-sdk](https://github.com/Silo-Server/silo-plugin-sdk) | Public Go SDK + protobuf contracts for building plugins. |
| [silo-plugins](https://github.com/Silo-Server/silo-plugins) | Catalog metadata and release helpers for first-party plugins. |
| [silo-plugin-tmdb](https://github.com/Silo-Server/silo-plugin-tmdb) | Metadata from The Movie Database (TMDB). |
| [silo-plugin-tvdb](https://github.com/Silo-Server/silo-plugin-tvdb) | Metadata from TheTVDB. |
### More
| Repo | What it is |
|---|---|
| [siloserver.org](https://github.com/Silo-Server/siloserver.org) | The project website. |
| [silo-push-relay](https://github.com/Silo-Server/silo-push-relay) | The Silo Push Notifiation relay service. |
| [silo-themes](https://github.com/Silo-Server/silo-themes) | Community theme catalog. |
