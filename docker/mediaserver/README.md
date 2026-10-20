# Mediaserver stack

Docker Compose project that sets up a fully-featured media stack that
fetches, downloads and plays back music, shows and movies.

It consists of:

- **Jellyfin**: media server.
- **Navidrome**: music streaming.
- **Radarr**: Search and download movies.
- **Sonarr**: Search and download shows.
- **Lidarr**: Search and download music.
- **Prowlarr**: Indexer manager for the *arrs.
- **Qbittorrent**: Bittorrent client.

## Requirements

**Docker** is required to be installed. It can be installed using the `docker`
role.

## Tags

No tags exist for this project.

## Variables

- `version_tags`: Dictionary with the versions for each service.
- `media_directory`: Path to the media directory.
- `render_group`: ID of the `render` group. This is needed to allow the
    container to use hardware acceleration.

## Dependencies

The `docker` task must be run at least once before running the playbook.

## Example Playbook

```yaml
- hosts: all
  become: true
  vars:
    service: mediaserver
  tasks:
    - name: Deploy service
      ansible.builtin.import_role:
        name: docker
        tasks_from: deploy.yml
```

## Annex

### Service ports

| Host         | Port                           | Role                              |
| ------------ | ------------------------------ | --------------------------------- |
| Jellyfin     | 8096                           | Media server                      |
| Radarr       | 7878                           | Fetch movies                      |
| Sonarr       | 8989                           | Fetch shows                       |
| Lidarr       | 8686                           | Fetch music                       |
| Prowlarr     | 9696                           | Indexer manager                   |
| Flaresolverr | 8191                           | Proxy for Cloudflare challenges   |
| Qbittorrent  | 6880 (Web UI)                  | Bittorrent client                 |
|              | 6881 (bittorrent)              |                                   |

### Paths

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

### Setup guide

#### Set up accounts

The first time you enter the web of each service, you should be prompted to
create a user.

Qbittorrent starts with an admin account with a random password. Check logs
for the password and change it.

#### Link Prowlarr to apps

Go to Settings > Indexers and add **Flamesolverr**:

- Tags: flaresolverr
- Host: `http://flaresolverr:8181/`

For each app, you'll need to obtain the API key. In each app, to Settings >
General > Security and copy the key.

Next, go back to Prowlarr and add the app in Settings > Apps:

- Prowlarr: `http://prowlarr:9696`
- Radarr: `http://radarr:7878`
- Sonarr: `http://sonarr:8989`
- Lidarr: `http://lidarr:8686`

#### Configure the download client

For each app, add qBittorrent as a download client. Go to Settings > Download
Clients:

- Host: `qbittorrent`
- Port: 6880
- Same username and password as for logging in to qBittorrent

#### Add an indexer

In Prowlarr, go to Indexers > Add indexer and add your indexers.

- If behind Cloudflare Challenge, apply the `flaresolverr` tag.
- Add the login info and/or API token if required.
- Test the connection

> NOTE: If the domain cannot be resolved, try changing the host machine's DNS
server and point to Cloudflare or Google.

You should be able to see the indexer in Settings > Indexers in each app.

#### Configure paths

For each app, set the appropiate path to store content. Go to Settings > Media
Management > Root Folders and select the correct path:

- Radarr: `/data/media/movies`
- Sonarr: `/data/media/tv`
- Lidarr: `/data/media/music`

In qBittorrent, go to Settings (gear icon) > Downloads and change Default Save
Path to /data/torrents. Also set Default Torrent Management Mode to Automatic.

For each category in the left-side ribbon (should appear lidarr, radarr and
sonarr), left click > Edit category...,  and set the proper subdirectory (it
will already be relative to the root)

Finally, enable "Copy .torrent files to:" and set it to
`/data/torrents/metadata` in order to store torrent files for safekeeping.

Now everything should work automagically! (mostly)
