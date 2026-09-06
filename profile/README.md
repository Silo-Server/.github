# Silo

**Self-hosted media streaming, built on a modern stack.**

Silo is an open-source media server with a Go backend and a React web UI. It
handles direct play, remuxing, and hardware-accelerated transcoding, and offers
a Jellyfin/Emby-compatible API for clients such as Findroid and Infuse,
alongside first-party native apps for Apple and Android. Client coverage varies.

[Website](https://siloserver.org) · [Server & docs](https://github.com/Silo-Server/silo-server) · [Contributing](https://github.com/Silo-Server/.github/blob/main/CONTRIBUTING.md) · [Brand & trademark](https://siloserver.org/brand) · [Discord](https://discord.gg/siloserver)

---

## Why Silo

- **Modern infra** — Go + PostgreSQL + Redis, with a documented Docker Compose deployment.
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
| [silo-plugin-autoscan-arr](https://github.com/Silo-Server/silo-plugin-autoscan-arr) | Targeted rescans from Sonarr and Radarr history. |
| [silo-plugin-markers-theintrodb](https://github.com/Silo-Server/silo-plugin-markers-theintrodb) | Playback markers from TheIntroDB. |
| [silo-plugin-metadata-audiobook](https://github.com/Silo-Server/silo-plugin-metadata-audiobook) | Metadata and artwork for audiobook libraries. |
| [silo-plugin-metadata-ebook](https://github.com/Silo-Server/silo-plugin-metadata-ebook) | Metadata and artwork for ebook libraries. |
| [silo-plugin-metadata-manga](https://github.com/Silo-Server/silo-plugin-metadata-manga) | Metadata and artwork for manga libraries. |
| [silo-plugin-metadata-tmdb](https://github.com/Silo-Server/silo-plugin-metadata-tmdb) | Metadata from The Movie Database (TMDB). |
| [silo-plugin-metadata-tvdb](https://github.com/Silo-Server/silo-plugin-metadata-tvdb) | Metadata from TheTVDB. |
| [silo-plugin-watchprovider-floppy](https://github.com/Silo-Server/silo-plugin-watchprovider-floppy) | Watch history and progress sync with Floppy. |

### More

| Repo | What it is |
|---|---|
| [siloserver.org](https://github.com/Silo-Server/siloserver.org) | The project website. |
| [silo-push-relay](https://github.com/Silo-Server/silo-push-relay) | Privacy-preserving push delivery for the Silo apps. |
| [silo-themes](https://github.com/Silo-Server/silo-themes) | Community theme catalog. |
| [unraid-templates](https://github.com/Silo-Server/unraid-templates) | Official Unraid Community Applications templates. |
