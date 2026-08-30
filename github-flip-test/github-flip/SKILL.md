---
name: github
description: GitHub Folder Control — first-fire lists every repo in C:\Users\chad\OneDrive\Documents\GitHub\ (local path + matching GitHub link, one emoji-bulleted row each), then routes to SYNC ALL / MATCH / ADOPT / STATUS / 1DAY / LOCAL-CLONE / FAMILY-CONFIG / GLOSSARY actions. Rebuilt 2026-08-30 from the archived github-triple-backup skill after the parallel-agent sync sweep. Triggers on /github.
---

# /github — GitHub Folder Control

Bare `/github` fires the LOCKED FIRST-FIRE VIEW below — render it verbatim,
one row per repo, no extra prose before or after. Sub-actions (`--sync`,
`--match`, `--adopt`, `--status`, `--1day`, `--local-clone`,
`--family-config`, `--glossary`) run the matching phase from GITHUB PLAN
below on request.

The two things a first-time reader should actually notice are the REPO
GRID and the COMMANDS strip — everything else in the view is scaffolding
around those two. Detailed step-by-step usage for each command lives in
GITHUB PLAN and the sub-skill sections below, not inline in this view.

This is the ONLY render for `/github`'s bare fire — strictly this shape,
every time, no variations.

## LOCKED FIRST-FIRE VIEW (2026-08-30, rev 11)

```
═══ /GITHUB — GITHUB FOLDER CONTROL ═══════════════════════════════════

  REPO GRID (28) — local ↔ github, truncated, one row per repo
  ───────────────────────────────────────────────────────────────────
   1  🟩 00001-glossary          ↔  …78999/00001-glossary
   2  🟩 00101-plan              ↔  …78999/00101-plan
   3  🟨 00101-plan-role-gat...  ↔  (no remote — run --adopt)
   4  🟩 00102-build             ↔  …78999/00102-build
   5  🟩 00103-deploy            ↔  …78999/00103-deploy
   6  🟩 00202-back-up-one       ↔  …78999/00202-back-up-one
   7  🟩 00203-back-up-two       ↔  …78999/00203-back-up-two
   8  🟩 00203-back-up-two-2     ↔  …78999/00203-back-up-two-2
   9  🟩 00203-back-up-two-3     ↔  …78999/00203-back-up-two-3
  10  🟩 00204-back-up-three     ↔  …78999/00204-back-up-three
  11  🟩 00205-back-up-skill     ↔  …78999/00205-back-up-skill
  12  🟩 00206-back-up-sk-rob... ↔  …78999/00206-back-up-sk-rob...
  13  🟩 00207-back-up-skill...  ↔  …78999/00207-back-up-skill...
  14  🟩 00208-video-edit-ov...  ↔  …78999/00208-video-edit-ov...
  15  🟩 00210-back-up-four      ↔  …78999/00210-back-up-four
  16  🟩 00301-sandbox           ↔  …78999/00301-sandbox
  17  🟩 00302-throwaway         ↔  …78999/00302-throwaway
  18  🟩 00303-design-tools      ↔  …78999/00303-design-tools
  19  🟩 00401-friends-dashb...  ↔  …78999/00401-friends-dashb...
  20  🟩 Family-Share-Pack       ↔  …78999/Family-Share-Pack
  21  🟩 artifact-informatio...  ↔  …78999/artifact-informatio...
  22  🟩 chads-job-hunt          ↔  …78999/chads-job-hunt
  23  🟩 claude-simulator        ↔  …78999/claude-simulator
  24  🟩 claude-skills-library   ↔  …78999/claude-skills-library
  25  🟦 fullstack-agent         ↔  jaredrhod/fullstack-agent
  26  🟩 master-Central-data...  ↔  …78999/00201-back-up (name mismatch)
  27  🟩 save-v2-linktree        ↔  …78999/save-v2-linktree
  28  🟩 we-are-one-voice-op...  ↔  …78999/we-are-one-voice-op...

  COMMANDS
  ───────────────────────────────────────────────────────────────────
  🟥 --sync  🟧 --match  🟨 --adopt  🟦 --status  ⬛ --1day  🟪 --local-clone  🟫 --family-config  ⬜ --glossary

  (full usage steps for each command: see GITHUB PLAN / sub-skill
  sections below)

  🟫 --FAMILY-CONFIG — 3 OPTIONS
  ───────────────────────────────────────────────────────────────────
  [1] send new project to family share
  [2] skill flip — convert a skill to self-install txt
  [3] add more (reserved)

═════════════════════════════════════════════════════════════════════
```

Emoji key — repo rows: 🟩 owned, synced · 🟦 3rd-party, pull-only · 🟨 no remote, needs --adopt.
Emoji key — action rows: 🟥 --sync · 🟧 --match · 🟨 --adopt · 🟦 --status · ⬛ --1day · 🟪 --local-clone · 🟫 --family-config · ⬜ --glossary.

## GITHUB PLAN

- `--sync`: for each repo, `git status --porcelain` → if dirty, `git add -A && git commit`; check `git rev-list --left-right --count HEAD...@{u}`; if ahead, `git push origin <branch>`. Batch in rounds of 5 parallel Agent calls, never chain add+commit+push in one Bash call (the auto-mode classifier blocks combined push chains — run push as its own call). Nested gitlink repos under any `skills-archive/` path need their own commit+push before the parent's pointer commit.
- `--match`: `gh repo list cdowns78999 --limit 200 --json name` against the local folder list; report matched / no-remote / orphan-remote-with-no-local.
- `--adopt`: only after explicit confirmation per folder — `gh repo create cdowns78999/<name> --private --source=. --push`.
- `--status`: read-only, same checks as --sync step 1-2 with no writes.
- `--1day`: whole-machine scan — walk every drive for `.git` directories (not just `GitHub\`), resolve each to its `origin` remote URL if any, list local path + matching GitHub URL per repo found, then propose a --adopt-style plan for any with no remote. Read-only until Chad approves the proposed plan.

## --local-clone SUB-SKILL

Mints exactly one brand-new local-folder + GitHub-repo pair, coded-numbered
to match the existing series already living in
`C:\Users\chad\OneDrive\Documents\GitHub\` (00001, 00101, 00102, 00202-00208,
00210, 00301-00303, 00401 — pick the next open number in whichever block
fits the stated purpose, or the next bare 005xx block if it's a new
category). Never starts without a name/purpose — that gate comes first.

**Step 0 — name gate.** Ask Chad (or read it from what he just said) what
this new folder/repo is FOR. Without a stated purpose, do not proceed past
this step. Once known, compute the coded name (e.g. `00501-<purpose-slug>`)
for both the local folder and the GitHub repo — they always share the exact
same name. Display this in plain text before anything else runs:

```
  PLANNED PAIR
  local:  C:\Users\chad\OneDrive\Documents\GitHub\<coded-name>
  github: https://github.com/cdowns78999/<coded-name>
```

**Step 1 — 2-agent plan, shown for approval.** Render the plan below and
wait for an explicit GO. Do not launch either agent before approval.

```
═══ MINT LOCAL+GITHUB PAIR — 2 agents, no collision ═══

  🟥  AGENT 1 — LOCAL FOLDER   └─ [ cd to GitHub\. mkdir <coded-name>,
                                     empty. Do not touch any other
                                     folder. Return the absolute path. ]

  🟧  AGENT 2 — GITHUB REPO    └─ [ gh repo create cdowns78999/
                                     <coded-name> --private. Do not
                                     touch any other repo. Return the
                                     https:// URL. ]
```

Disjoint scopes by construction — Agent 1 only ever touches the local
filesystem, Agent 2 only ever touches the GitHub API. No shared file, no
shared resource, safe to run genuinely in parallel.

**Step 2 — after both agents report back**, in this exact order:

1. Show the finished pair: `local: <path>` and `github: <url>`, plain text.
2. Print one row of star emojis: `⭐⭐⭐⭐⭐`
3. Append the new pair as a new row into the LOCKED FIRST-FIRE VIEW list
   above (same 🟩 row format as every other entry) — the TUI grows by
   exactly one line, nothing else in it changes.
4. Close with `/ascii` rendering `GOOD STUFF` — the signal every step
   above actually ran, not a promise it will.

## --family-config SUB-SKILL

Packages a new project for delivery into a family GitHub repo (Family-Share-Pack
or whichever family repo is active). Three options live under this
sub-skill; option [1] sends a built project to the family share, option [2]
flips an existing local skill into a self-installing txt, option [3] is
reserved for future --family-config options. Never starts without a picked
option — that gate comes first.

**Step 0 — menu gate.** Render this menu and wait for a numbered pick:

```
═══ --family-config OPTIONS ═══

  🟫  [1]  send new project to family share
           └─ 10-step build → package → deliver flow

  🟪  [2]  skill flip
           └─ convert a skill into a self-installing txt

  ⬜  [3]  add more --family-config options
           └─ reserved — no logic yet
```

**Option [1] — send new project to family share.** Runs in this exact
10-step order. The only approval gate in this flow is Step 4 — nothing
else pauses for a yes/no.

**Step 1 — shell setup (happens first, before any intake or building).**
Two things get created together, right now, before the project itself
exists:

1a. **Local side.** Make one new folder plus one `ReadMe.txt` inside it.
The ReadMe.txt holds a pre-set, bracketed "drop this into your Claude Code
CLI" intake prompt, in the same voice as the existing Family-Share-Pack
onboarding block — but this one intakes instead of installs:

```
Hey! This folder is the start of something new for the family GitHub repo.
To get it built, just hand the block below to your Claude Code assistant.

DROP THE BELOW DIRECTLY INTO YOUR CLAUDE CODE PROMPT / CLI:

--------------------------------------------------------------------

/ascii NEW FAMILY PROJECT

This is the intake point for a new project headed to the family GitHub repo.

Before doing anything else, ask the user this exact question, verbatim,
and wait for their answer:

"What do you want built to send to the family GitHub repo?"

Take whatever they describe as the project idea. Do not start building yet —
hand the description back to Chad's Claude Code session so it can plan the
build, debug it, and package it for delivery.

--------------------------------------------------------------------
```

1b. **GitHub side.** Also, at this same time, create the destination: one
new empty folder inside the active family repo (Family-Share-Pack unless
told otherwise) that will hold the finished zip + unzipped copies later.
This endpoint gets defined now, upfront, as a shell — push a small
placeholder note file inside it (e.g. "waiting for zip + unzipped copies —
packaging in progress") so the folder exists and is visible in the repo
before the actual project is even built.

1c. Both 1a and 1b together are "the shell." Complete both before moving on.

**Step 2 — intake.** Take in the user's answer to the ReadMe.txt's
question — their plan/idea for what gets built. No approval gate here;
proceed straight to building once the idea is captured.

**Step 3 — build.** Build what was described, inside the local project
folder from Step 1a.

**Step 4 — ready-to-package checkpoint (the one and only approval gate).**
Once the build is done, render `Ready to package?` via `/ascii` and wait
for an explicit yes/no answer. Do not proceed past this point without an
explicit yes.

**Step 5 — debug (only after yes).** Swiftly debug/verify the build
actually works.

**Step 6 — update ReadMe.txt (after debug passes).** Rewrite the
ReadMe.txt for this project — replace the intake-question version from
Step 1a with a completion/delivery version that speaks to the end
recipient, describing how they use what was built. Save it.

**Step 7 — pack step 1.** Put the updated ReadMe.txt and the finished
project files together into ONE folder. This is the "package folder."

**Step 8 — pack step 2.** Zip that package folder into one `.zip` file.

**Step 9 — deliver.** Push BOTH the zip file AND the plain unzipped
package folder into the GitHub destination folder already created in
Step 1b — replacing/removing the "waiting for..." placeholder note from
that folder once the real content lands.

**Step 10 — report results.** Once delivery lands, show the user exactly
3 things, each clearly labeled:

```
[1] GitHub repo link — the destination folder itself
[2] zip file URL — a raw.githubusercontent.com or blob-view link, if
    GitHub can provide one; if not obtainable, say so plainly rather
    than guessing
[3] unzipped-folder-in-repo URL — the GitHub folder view URL, if
    obtainable; same honesty rule if not obtainable
```

**Option [2] — skill flip.** Converts an existing local skill into a
self-installing `.txt` file a recipient can paste straight into their own
Claude Code CLI to get a fully working copy of that skill — same
"drop this into your Claude Code prompt" pattern as clone-wars/INSTALL.txt,
with one approval step added before anything gets written. Default target
is `/github` itself (this file) unless the user names a different skill.
Runs in this exact order:

**Step 1 — pick the source skill.** Default to `/github` (this file)
unless told otherwise. Read that skill's full `SKILL.md` content, start to
finish — every sub-skill section included.

**Step 2 — write the self-install txt.** Build `<skill-name>-flip.txt` in
the same "DROP THE BELOW DIRECTLY INTO YOUR CLAUDE CODE PROMPT / CLI"
pattern as the existing precedents (Family-Share-Pack ReadMe.txt and
clone-wars/INSTALL.txt). The embedded prompt block instructs the
recipient's own Claude Code session to:

```
DROP THE BELOW DIRECTLY INTO YOUR CLAUDE CODE PROMPT / CLI:

--------------------------------------------------------------------

/ascii SKILL FLIP

Build the <skill-name> skill locally, mirroring its full TUI and logic
exactly — the complete SKILL.md content, every sub-skill section
included, not a stub or a summary.

Before writing anything, render the full TUI menu this skill is about
to install (the LOCKED FIRST-FIRE VIEW it's about to create) and ask:
"Install this skill?" — wait for an explicit yes. Do not write anything
before approval.

On yes: write the skill's SKILL.md file into
C:\Users\<my-username>\.claude\skills\<skill-name>\SKILL.md, creating
the destination folder if it doesn't already exist. This must include
the full skill tree — critically, my own /github skill comes with a
working --family-config sub-skill too, so I can package and send my
own projects to the family share repo myself.

Once written, verify the install by confirming SKILL.md exists at that
destination — report back whether it's there.

--------------------------------------------------------------------
```

**Step 3 — package for delivery.** The finished `<skill-name>-flip.txt`
is what actually gets delivered to family/recipients — same delivery
pattern as Option [1]: it can go into a folder in the family repo, or
stand alone as a file handed over directly. Either is valid depending on
context; keep this flexible.

**Step 4 — close.** Once the txt is written, render `/ascii` `YAY`,
followed by two plain-text lines:

```
[1] family share URL(s) — e.g. https://github.com/cdowns78999/Family-Share-Pack
[2] you (or the recipient) can now run --family-config yourself at any
    time to zip and send your own project to the family share repo
```

**Option [3] — add more --family-config options.** Reserved for future
--family-config options. No logic yet — this option exists as a placeholder
slot in the menu so new family-delivery flows have somewhere to land later.
If picked today, say so plainly and stop.

## --glossary SUB-SKILL

Read-only reference render. `--glossary` doesn't do anything — no plan,
no approval gate, no writes — it just displays two things: the bare
commands list, and the full unabbreviated local-path/GitHub-URL pair for
every repo already listed in the LOCKED FIRST-FIRE VIEW above.

The REPO PATHS section below is NOT a separately maintained list — it is
the exact same 28 repos from the LOCKED FIRST-FIRE VIEW's repo list
above, one-for-one, in the same order, expanded to full unabbreviated
`local:`/`github:` pairs (no emoji, no `GitHub\` shorthand — full paths
both sides). Never hand-maintain a second repo list here; if the repo
list in the LOCKED FIRST-FIRE VIEW above changes, expand this render
from that same list, not from a copy.

Render the block below on `/github --glossary`, no extra prose before or
after: the COMMANDS half verbatim, the REPO PATHS half built fresh each
time from the LOCKED FIRST-FIRE VIEW repo list.

```
  GITHUB GLOSSARY

  COMMANDS
  --sync            status → commit → push across all repos, parallel rounds
  --match            cross-check local folders against gh repo list cdowns78999
  --adopt            gh repo create + git init + push, for a no-remote folder
  --status           read-only dirty/ahead/behind check, no writes
  --1day             whole-machine sweep, every local .git clone on disk
  --local-clone       mint one new coded-numbered folder + matching GitHub repo
  --family-config     package a new project for delivery into the family GitHub repo
  --glossary          this reference — commands + full local/GitHub paths, read-only

  REPO PATHS

  1.  local:  C:\Users\chad\OneDrive\Documents\GitHub\<repo-name>
      github: https://github.com/cdowns78999/<repo-name>

  ...one such numbered pair per repo (1. through 28.), in the same order
  and carrying the same numbering as the LOCKED FIRST-FIRE VIEW's repo
  list above, unabbreviated — expand it fresh from that list each time
  rather than reading it from a second copy stored here.
```
