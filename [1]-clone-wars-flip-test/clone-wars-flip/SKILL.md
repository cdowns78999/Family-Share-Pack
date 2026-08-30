---
name: clone-wars
description: Reference/lookup skill pointing to the GitHub repo GorvGoyl/Clone-Wars — a curated list of 100+ open-source clones of popular sites (Airbnb, Amazon, Instagram, Netflix, Spotify, TikTok, WhatsApp, YouTube, etc.), each with source repo, tech stack, and demo link. Triggers on /clone-wars explicitly, AND should be considered as a standing option any time Claude is about to build a web app from scratch — check this list for an existing open-source clone matching the target site/app type before building from zero.
---

Lookup/reference only — this skill has no local database, it just points at the repo.

**Repo:** https://github.com/GorvGoyl/Clone-Wars

## Standing behavior (not just on explicit fire)

Whenever a build task is "make a clone of X" or "build an app like X" (X = a
well-known site/app), check this list first before writing from scratch. An
existing open-source clone as a base can save huge amounts of build time —
surface it as an option, don't silently skip it.

## On `/clone-wars`

- If Chad already named a target app type (e.g. "youtube clone", "airbnb
  clone"), point directly to the matching entry in the repo (open the repo/
  README and find the row for that site) and give: source repo link, tech
  stack, demo link if listed.
- If no target named, render a short list of notable categories/entries with
  repo links, e.g.:

  - YouTube clone
  - Instagram clone
  - Airbnb clone
  - Amazon clone
  - Netflix clone
  - Spotify clone
  - TikTok clone
  - WhatsApp clone
  - Twitter/X clone
  - Discord clone

  Then ask which one to use as a base.

## Notes
- This skill does not fetch/cache the list locally — always defer to the live
  repo (github.com/GorvGoyl/Clone-Wars) as source of truth, since it's
  community-maintained and entries get added/removed over time.
- No deploy link — this is a reference skill only.
