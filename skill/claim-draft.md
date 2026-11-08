I'm claiming this issue. I've already reproduced it locally by testing the extension in my browser.

I understand the feature request: add an option to block specific playlists (like "My Mix" and "Podcasts") from appearing in search results and recommendations.

My first step is to:
1. Trace through the extension's data flow to understand how playlists are currently filtered (or not)
2. Identify where the blocking logic should live (popup.js, background.js, or elsewhere)
3. Ask you to clarify the scope: should this block all playlists, specific categories, or user-defined ones? And where should the block apply (search results, home feed, sidebar)?

I'll report back by Monday with my findings and a proposed implementation approach.