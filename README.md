# Apple Music Playlist Importer

A utility to extract Spotify playlist data (via Spotify API) and convert it to Apple Music format.

- [Complete Postman Guide: How to Use the Spotify API to Get a User's Playlists (With OAuth 2.0 Authentication)](https://gist.github.com/tshego3/d663545db6489c1b1119d07818ce3990)

## Usage

### How to Add Songs to Apple Music

Since Apple Music's AppleScript API is limited, use the web interface to search and add songs:

1. Open `index.html` in a web browser
2. Upload your Spotify playlist JSON export file
3. Click "Process Songs" to extract and load the playlist
4. Click the "Search" link for each song
5. Apple Music will open in a new tab and search for the song
6. Click the "+" button to add it to your library or a playlist
7. Alternatively, copy the song/artist names and search manually in Apple Music

## Advanced Usage

### Convert Spotify Playlist to Apple Music Format (Command Line)

Optionally, extract songs from a Spotify API JSON export using the command line script:

```bash
/Downloads/extract_spotify_playlist.sh "/Downloads/spotify_playlist.json" > "/Downloads/apple_music_playlist_output.txt"
```

### Verify Output

Check the number of lines and preview the first 10 entries:

```bash
wc -l "/Downloads/apple_music_playlist_output.txt" && echo "---" && head -10 "/Downloads/apple_music_playlist_output.txt"
```

This will output something like:

```
76 /Downloads/apple_music_playlist_output.txt
---
Song Title 1 - Artist Name 1
Song Title 2 - Artist Name 1, Artist Name 2
Song Title 3 - Artist Name 3
```

## Files

- `extract_spotify_playlist.sh` - Main script to extract Spotify API playlist data and format for Apple Music
- `*.json` - Spotify API playlist JSON exports
- `apple_music_playlist_importer.html` - Web interface for easy playlist import

## Script Code

### extract_spotify_playlist.sh

```bash
#!/bin/bash

# Script to extract artist and song name from Spotify API JSON export for Apple Music import

JSON_FILE="$1"

if [ -z "$JSON_FILE" ]; then
    echo "Usage: $0 <path-to-spotify-json-file>"
    exit 1
fi

if [ ! -f "$JSON_FILE" ]; then
    echo "Error: File '$JSON_FILE' not found"
    exit 1
fi

# Use jq to parse JSON and extract track name and artists (unique per track)
jq -r '.items[] | "\(.track.name) - \(.track.artists | map(.name) | join(", "))"' "$JSON_FILE"
```
