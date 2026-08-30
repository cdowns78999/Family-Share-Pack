Hey! Chad set up this repo to share with family. To get your own copy connected, just hand the block below to your Claude Code assistant.

DROP THE BELOW DIRECTLY INTO YOUR CLAUDE CODE PROMPT / CLI:

--------------------------------------------------------------------

/ascii FAMILY SHARE PACK

This came from Chad, sharing a family GitHub repo.

Repo: https://github.com/cdowns78999/Family-Share-Pack

Before doing anything else, ask the user this exact question, verbatim, and wait for their answer:

"Am I allowed to add this to your repo? If so, say yes, and I will check that GitHub CLI is connected and then do that."

Do NOT proceed without an explicit "yes" answer. Do not assume consent. If the answer is anything other than a clear yes, stop and do nothing further.

Only if the user answers "yes", do the following in order:

1. Run `gh auth status` to confirm GitHub CLI is connected. If it is NOT connected, tell the user to run `gh auth login` first, and stop there — do not continue.

2. Create the user's own copy of the Family Share Pack repo in their own GitHub account. Use this exact command:

   gh repo fork cdowns78999/Family-Share-Pack --clone=false

   If the user would rather have a fully independent copy instead of a fork (no link back to the original), use this exact sequence instead:

   gh repo create Family-Share-Pack --public --clone=false
   git clone https://github.com/cdowns78999/Family-Share-Pack.git
   cd Family-Share-Pack
   git remote set-url origin https://github.com/<their-username>/Family-Share-Pack.git
   git push -u origin master

3. Once done, report back the user's own new repo URL directly to them.

--------------------------------------------------------------------

That's it — once your family member's Claude Code confirms the yes/no with them and (if approved) forks or copies the repo, they'll have their own linked copy on their GitHub account, and Claude will hand them the new repo URL directly.
