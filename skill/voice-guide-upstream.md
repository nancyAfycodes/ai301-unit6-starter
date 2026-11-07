# Voice guide, the upstream section: how I talk to maintainers

## Upstream: how I talk to maintainers

### Claims I post

#### Rule: Name your first step and commit to a timeline

A claim is not "I'll work on this." It's "Here's what I'm doing first, and here's when I'll report back."

- Wrong: "I'm interested in this issue. I'll start working on it soon."
- Right: "I'm claiming this issue. I've already reproduced it locally. My first step is to trace the asyncio.run loop lifecycle and identify where lru_cache is keeping the engine alive. I'll report back by Friday with my findings and a proposed fix approach."

#### Rule: Prove you understand the issue before you claim it

Post reproduction evidence in your claim. Show you've done the work.

- Wrong: "I'm claiming this. I haven't reproduced it yet but the fix should be straightforward."
- Right: "I reproduced this with `menagerist --db local:// --query test`. I got RuntimeError: Event loop is closed on the second database command. Here's the traceback: [pasted output]. I understand the issue: asyncio.run creates a new loop each time, but lru_cache keeps the database engine from a previous loop alive."

### Questions I ask

#### Rule: Show your work before asking

Before you ask a maintainer something, say what you already checked and why you're stuck.

- Wrong: "How should I fix this?"
- Right: "I've traced the issue to the engine being cached across asyncio.run calls. I see two possible fixes: (1) clear the lru_cache before each run, or (2) make the engine async-aware. I read [issue #XXX] which suggests approach 2 might be preferred. Should I explore that direction, or is approach 1 simpler for this case?"

#### Rule: Ask one question, not a pile

- Wrong: "What should I do? Do I need to write tests? Where should they go? What format? Should I update the docs too?"
- Right: "I'm ready to write a fix. Should I add tests in tests/unit/test_database.py following the existing pattern, or is there a different test file you prefer for asyncio-related tests?"

### Pings I send

#### Rule: Ping only when you're stuck and they're the only one who can help

Match the repo's rhythm. If the maintainer replies within hours, ping after a day. If they take a week, give them two weeks.

- Wrong: "@samcorky can you review my work?" (posted 2 hours after your previous message)
- Right: "@samcorky I've been working on this since Tuesday and traced it to [specific issue]. I'm at a decision point [explain]. When you have a moment, would you clarify which approach you'd prefer?" (posted after giving them a full work day to respond to your previous message)