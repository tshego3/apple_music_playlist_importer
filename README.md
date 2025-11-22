# Apple Music Playlist Importer

[#Complete Postman Guide: How to Use the Spotify API to Get a User's Playlists (With OAuth 2.0 Authentication)](https://gist.github.com/tshego3/d663545db6489c1b1119d07818ce3990)

A utility to extract and convert Apple Music playlists to Spotify format.

## Usage

### Extract Spotify Playlist

Extract songs from an Apple Music JSON playlist export:

```bash
/Downloads/extract_spotify.sh "/Downloads/spotify_playlist.json" > "/Downloads/spotify_playlist_output.txt"
```

### Verify Output

Check the number of lines and preview the first 10 entries:

```bash
wc -l "/Downloads/spotify_playlist_output.txt" && echo "---" && head -10 "/Downloads/spotify_playlist_output.txt"
```

This will output something like:

```
76 "/Downloads/spotify_playlist_output.txt"
---
[first 10 lines of playlist data]
```

## Files

- `extract_spotify.sh` - Main script to extract and format playlist data
- `*.json` - Apple Music playlist JSON exports
- `apple_music_playlist_importer.html` - Web interface (optional)
