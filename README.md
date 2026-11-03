# Plex Genre Playlists

Create a Plex smart playlist for each album style in a music library using
Plex's Python API. Each playlist contains tracks matched by `album.style`.

## Requirements

- [uv](https://docs.astral.sh/uv/)
- A Plex Media Server and a Plex token with permission to manage playlists

The script declares its Python dependencies inline, so no separate environment
setup is needed.

## Configuration

Create the default config directory and copy the example:

```sh
mkdir -p ~/.config/plex-genre-playlists
cp config.example.toml ~/.config/plex-genre-playlists/config.toml
chmod 600 ~/.config/plex-genre-playlists/config.toml
```

Edit `~/.config/plex-genre-playlists/config.toml` with your Plex server URL,
token, and music library name:

```toml
[plex]
base_url = "http://localhost:32400"
token = "your-private-token"
default_library = "Music"
```

Keep the real config and token private; do not commit or share them. You can
choose a different config path with `--config`.

## Usage

Run from the repository root. The default is a **preview only**:

```sh
uv run --script bin/plex-genre-playlists
```

Create the playlists after reviewing the preview:

```sh
uv run --script bin/plex-genre-playlists --apply
```

Override the configured library or config path:

```sh
uv run --script bin/plex-genre-playlists --library "Another Music Library"
uv run --script bin/plex-genre-playlists --config ~/secrets/plex.toml
```

The script discovers album styles, then creates a track smart playlist for each
style using Plex's `album.style` filter. It skips any style whose exact playlist
title already exists anywhere on the Plex server, so rerunning it does not
create duplicates.
