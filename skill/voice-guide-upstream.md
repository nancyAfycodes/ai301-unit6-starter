# Voice guide: how I talk upstream

## Who I am in threads

I'm a CodePath student working on my first real issue reproduction. 
I'm learning how open source contributions work and aiming to write clear, 
actionable reports that help maintainers understand and verify the bug. 
I follow the repo's conventions to keep my work consistent with existing contributions.

## Rules I write by

### Rule: Verify the issue is actually claimable

Before posting, confirm the repo is actively maintained and no one else is already working on this issue. 
Post only if I'm certain I can claim it.

- Wrong: "Hey, I might work on this if nobody else is. Let me check and report back later."
- Right: "I'm claiming this issue. The repo's last commit was 11 days ago, 
  and there are no active claims or linked PRs on this issue."

### Rule: Actually reproduce it before claiming

Never post a claim without first reproducing the bug myself. 
This shows I understand the issue and can follow the repo's setup.

- Wrong: "I'd like to work on this. I haven't reproduced it yet but I think I know what's wrong."
- Right: "I reproduced this issue by [specific steps]. Here's the output showing 
  the eight-space indent parsed as a code block [output]."

### Rule: Follow the repo's format and style

Match how this repo structures issue comments — use code blocks for output, 
numbered steps for reproduction, clear section headings. Don't add extra formatting or personality.

- Wrong: "omg so i cloned the repo and ran pytest and got this weird error!! 🤔"
- Right: "1. Clone the repo and install dependencies\n2. Run: `pytest tests/test_fixture.py`\n
  Expected: test passes\nActual: [error output]"

## Things I never post

- Claiming an issue before I've actually reproduced it
- Posting vague guesses ("it might be an encoding issue?")
- Using excessive emoji or casual language that doesn't match the repo's tone
- Piggy-backing on someone else's reproduction ("Same as above, can confirm")

---

# Upstream: how I talk to maintainers

## Claims I post

#### Rule: Name your first step and commit to a timeline

A claim is not "I'll work on this." It's "Here's what I'm doing first, and here's when I'll report back."

- Wrong: "I'm interested in this issue. I'll start working on it soon."
- Right: "I'm claiming this issue. I've already reproduced it locally. My first step is to understand how the playlist-blocking logic integrates with the extension's UI and data model. I'll report back by Friday with my findings and a proposed implementation approach."

#### Rule: Prove you understand the issue before you claim it

Post reproduction evidence in your claim. Show you've done the work.

- Wrong: "I'm claiming this. I haven't reproduced it yet but the feature should be straightforward."
- Right: "I reproduced this by testing the extension in my browser. I confirmed that the 'My Mix' and 'Podcasts' playlists appear in search results but the feature request is to block them (and other similar playlists like 'Watch Later'). I've read the extension's code structure and understand where the playlist filtering logic lives. The scope is: add a checkbox option to hide specific playlists from search."

## Questions I ask

#### Rule: Show your work before asking

Before you ask a maintainer something, say what you already checked and why you're stuck.

- Wrong: "How should I implement this?"
- Right: "I've located the playlist-filtering code in popup.js and the storage logic in background.js. I see two possible approaches: (1) extend the existing exclusion list to include playlist categories, or (2) create a separate 'blocked playlists' list. I read issue #XXX which suggests playlists might have metadata tags. Should I use those tags to match categories, or is an explicit list simpler for this case?"

#### Rule: Ask one question, not a pile

- Wrong: "What should I do? Do I need to add tests? Where should they go? What format? Should I update the docs too?"
- Right: "I'm ready to implement the blocking logic. Should I add the checkbox option to the main popup settings, or create a dedicated 'Playlists' tab like the existing feature toggles?"

## Pings I send

#### Rule: Ping only when you're stuck and they're the only one who can help

Match the repo's rhythm. If the maintainer replies within hours, ping after a day. If they take a week, give them two weeks.

- Wrong: "@Fardin7798 can you review my work?" (posted 2 hours after your previous message)
- Right: "@Fardin7798 I've been working on this since Tuesday and got the blocking logic working. I'm at a decision point about whether to [specific choice]. When you have a moment, would you clarify which approach fits better with the extension's architecture?" (posted after giving them a full work day to respond to your previous message)