# HGreat's TuneHarbor

Best ever MP3 player and radio ripper – listen to web radio, record it and split it into tracks, and manage and play your music library.

- **Windows app:** download the setup from [Releases](https://github.com/Team-HGreat/tuneharbor/releases) (updates itself automatically) or from [itch.io](https://teamhgreat.itch.io/tuneharbor).
- **Server / NAS:** run it as a Docker container and use it in the browser on any device (see below).

## Docker

The image is available for **x86-64 (amd64)** and **ARM64** (Raspberry Pi 4/5, many NAS):

```
ghcr.io/team-hgreat/tuneharbor:latest
```

### docker compose

```yaml
services:
  tuneharbor:
    image: ghcr.io/team-hgreat/tuneharbor:latest
    container_name: tuneharbor
    restart: unless-stopped
    ports:
      - "8555:8000"                      # web UI: http://<server>:8555
    environment:
      - TZ=Europe/Vienna                 # your time zone (show schedules)
    volumes:
      - ./tuneharbor-data:/data          # database, playlists, statistics, recordings
      - /path/to/your/music:/library     # your music library
```

```
docker compose up -d
```

Then open `http://<your-server>:8555` in the browser.

### docker run

```
docker run -d --name tuneharbor --restart unless-stopped \
  -p 8555:8000 -e TZ=Europe/Vienna \
  -v ./tuneharbor-data:/data \
  -v /path/to/your/music:/library \
  ghcr.io/team-hgreat/tuneharbor:latest
```

### Folders

| Path in the container | What it is |
|---|---|
| `/data` | Database, stations, playlists, play statistics, caches and – by default – recordings (`/data/recordings`). **Keep this folder** to keep your data across updates. |
| `/library` | Your music. It is scanned including all subfolders; the tag editor and the Meta workshop write tags and rename files here, so mount it **read-write**. |

The recording folder and the music folder can be changed in the web UI under *Settings*.

### Update

```
docker compose pull && docker compose up -d
```

### Features

Web radio with metadata and song alarm · recording with automatic track splitting and scheduled shows · music library with tag editor, online tag and cover suggestions · Meta workshop (tag doctor, gaps, duplicates, missing covers, inbox) · smart playlists, USB stick export · statistics and year in review · karaoke with synced lyrics · full-screen visualizer · equalizer, auto DJ and crossfades · skins · backup and restore of all settings.

### Legal notice

Recording radio streams is only allowed for private use, depending on the laws of your country. TuneHarbor shows a notice that has to be confirmed before the recorder can be used.

© 2026 Team HGreat
