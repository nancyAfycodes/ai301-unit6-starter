I'm claiming this issue for a CodePath AI301 contribution.

## Reproduction

I've confirmed the issue locally following the steps in the issue:
1. Started menagerist interactive shell (`menagerist` with no arguments)
2. Ran `media cleanup` — succeeded ✓
3. Ran `media cleanup` again — got `RuntimeError: Event loop is closed` ✓

The error occurs in `repos.assets.list_expired`, exactly as the issue describes.

## What I understand

The bug: each command runs under a new `asyncio.run()` loop that closes after the command finishes. The database engine and session factory are cached with `@lru_cache` in `platform/database.py`, so when the second command starts, it reuses pooled asyncpg connections from the *closed* first loop — hence "Event loop is closed."

## My first step

I'm going to trace the asyncio.run loop lifecycle in `media_app.py` and map exactly where the engine persists across loop boundaries. Then I'll examine both proposed fixes to understand their trade-offs.

## Design question

I see two candidate approaches in the issue:
1. **run_async() helper**: dispose the engine and clear caches after each command (preserves pooling, but requires changes in multiple files)
2. **NullPool for CLI**: simpler implementation, but trades pooling for correctness

Which approach fits menagerist's design philosophy better? I want to pursue the right direction before opening a PR.

## Timeline

I'll report back by **November 8** with my findings and a proposed fix approach.