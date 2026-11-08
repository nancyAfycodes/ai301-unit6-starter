# Reproduction Report: Block Playlists Feature (youtube#4348)

## Environment

- Browser: Chrome 131.0.6778.86
- OS: Windows 11
- Extension version: Latest from repo
- Date: 2026-11-08

## Steps to Reproduce

1. Clone the repository: `git clone https://github.com/<your-fork>/youtube.git`
2. Load the extension in Chrome: Follow the steps in walkthrough.md (load unpacked from repo root)
3. Navigate to YouTube home feed
4. Find a playlist tile (e.g., "My Mix" or "Podcasts")
5. Click the block button on a playlist tile
6. Check the blocklist settings menu to see if the playlist is blocked

## Current Behavior

When you click the block button on a "My Mix" or "Podcasts" tile, the first video in the playlist gets blocked (not the playlist itself). The blocklist settings menu shows two lists: "Channels" and "Videos" (in `menu/skeleton-parts/blocklist.js`). There is no "Playlists" list, so users cannot block entire playlist types from appearing.

## Observed

The blocklist settings menu (menu/skeleton-parts/blocklist.js) displays only two lists:
- Channels (blocked channels)
- Videos (blocked videos)

There is no "Playlists" option.

When I clicked the block button on a "My Mix" playlist tile, it blocked that single video, not the entire "My Mix" playlist. The next time I refreshed the home feed, other videos from "My Mix" still appeared.

The content script (js&css/web-accessible/www.youtube.com/blocklist.js, line 12) only processes nodes with a video ID: `if (!video) return;`. Playlist items don't have video IDs in the same way, so they bypass the blocking logic. The storage object structure has `blocklist.channels` and `blocklist.videos`, but no `blocklist.playlists` field to store playlist blocks.

## Desired Behavior

Users should be able to block entire playlist types (Mixes, Podcasts, Watch Later, etc.) from appearing in search results and home feed recommendations. The blocklist menu should have a third list for "Playlists" alongside Channels and Videos.

## Evidence

The blocklist logic in `js&css/web-accessible/www.youtube.com/blocklist.js` and `menu/skeleton-parts/blocklist.js` currently handles only channels and videos:
- The UI (skeleton-parts/blocklist.js) defines only two storage sections: `blocklist.channels` and `blocklist.videos`
- The content script (blocklist.js line 12) checks `if (!video) return;`, skipping any node without a video ID
- There is no handling for playlist type identification or blocking