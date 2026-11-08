# Reproduction Report: Block Playlists Feature (youtube#4348)

## Environment

- Browser: Chrome 131.0.6778.86
- OS: Windows 11
- Extension version: Latest from repo
- Date: 2026-11-08

## Steps to Reproduce

1. Clone the youtube extension repository
2. Install dependencies: npm install
3. Load the extension in Chrome
4. Navigate to YouTube home feed
5. Open the extension's blocklist settings
6. Attempt to add "My Mix" or "Podcasts" to the blocklist

## Current Behavior

The blocklist feature works for URLs and channels. When you open the blocklist settings, you see options to block specific URLs and channels, but there is no option to block playlist-type items (Mixes, Podcasts, Watch Later) from appearing in search results or recommendations.

## Desired Behavior

Users should be able to toggle a checkbox in the blocklist settings to hide specific playlist types from appearing in search results and the home feed.

## Evidence

The blocklist logic is in `menu/skeleton-parts/blocklist.js` and `js&css/web-accessible/blocklist.js`. Both files currently only handle URL and channel blocking. There is no handling for playlist-type items.