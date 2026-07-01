# Media server setup guide

## Service ports

| Host         | Port                           | Role                              |
| ------------ | ------------------------------ | --------------------------------- |
| Jellyfin     | 8096                           | Media server                      |
| Radarr       | 7878                           | Fetch movies                      |
| Sonarr       | 8989                           | Fetch shows                       |
| Lidarr       | 8686                           | Fetch music                       |
| Prowlarr     | 9696                           | Indexer manager                   |
| Flaresolverr | 8191                           | Proxy for Cloudflare challenges   |
| Qbittorrent  | 6880 (HTTP), 6681 (bittorrent) | Bittorrent client                 |

## Paths

In order to make sure the managers know how to hardlink downloads to the correct directories, a specific layout is used:

```
data/mediaserver
├── torrents
│   ├── books
│   ├── movies
│   ├── music
│   └── tv
├── usenet
│   ├── incomplete
│   └── complete
│       ├── books
│       ├── movies
│       ├── music
│       └── tv
└── media
    ├── books
    ├── movies
    ├── music
    └── tv
```

## Installation guide

### Set up accounts

Set up accounts on each service started.

### Configure Prowlarr

Go to Settings > Indexers and add Flamesolverr:

- Tags: flaresolverr
- Host: http://flaresolverr:8181/

> NOTE: Since all of the containers are in the same Docker network, they can be addressed by their container name.

For each app, you'll need to obtain the API key. In each app, to Settings > General > Security and copy the key.

Next, go back to Prowlarr and add the app in Settings > Apps:

- Prowlarr: http://prowlarr:9696
- Radarr: http://radarr:7878
- Sonarr: http://sonarr:8989
- Lidarr: http://lidarr:8686

### Configure the arrs

For each app, add qBittorrent as a download client. Go to Settings > Download Clients:

- Host: qbittorrent
- Port: 6880
- Same username and password as for logging in to qBittorrent

### Add an indexer

In Prowlarr, go to Indexers > Add indexer and add your indexers.

- If behind Cloudflare Challenge, apply the `flaresolverr` tag.
- Test the connection

> NOTE: If the domain cannot be resolved, try changing the host machine's DNS server and point to Cloudflare or Google.

You should be able to see the indexer in Settings > Indexers in each app.

### Configure paths

For each app, set the appropiate path to store content. Go to Settings > Media Management > Root Folders and select the correct path:

- Radarr: /data/media/movies
- Sonarr: /data/media/tv
- Lidarr: /data/media/music

In qBittorrent, go to Settings (gear icon) > Downloads and change Default Save Path to /data/torrents. Also set Default Torrent Management Mode to Automatic.

For each category in the left-side ribbon (should appear lidarr, radarr and sonarr), left click > Edit category...,  and set the proper subdirectory (it will already be relative to the root)

Now everything should work automagically!

### Verifications

Verify that:

- Torrents are downloaded into `/data/torrents/<media_type>/` and then hardlinked to `/data/media/<media_type>` with an appropiate name.
