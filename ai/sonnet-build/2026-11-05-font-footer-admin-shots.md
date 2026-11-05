# Fix font, use GitHub handle in footer, add admin screenshots

## Request
1. Fix the font problem.
2. Remove the owner's name from the footer and from git commit history. Use the GitHub handle @mrlinnth instead, linked to the GitHub profile.
3. Show 2 screenshots of admin features: the users and branding pages.

## Decisions
- Font: `src/input.css` declares Figtree 600 at `fonts/figtree-latin-600-normal.woff2`, but that file is missing from `public/fonts/`. Copy it from the app repo's installed package (same version family as the 400 file already here): `/home/claude/work/yan/quest-board/node_modules/@fontsource/figtree/files/figtree-latin-600-normal.woff2` (@fontsource/figtree 5.3.0). Same OFL license as the existing Figtree file; `public/fonts/LICENSE-figtree.txt` already covers it.
- Footer (`public/index.html`, the `<footer>`): the copyright span becomes `© 2026 <a href="https://github.com/mrlinnth">@mrlinnth</a>`. Style the link like the existing Credits link (`text-accent hover:underline`).
- `LICENSE` line 3 becomes `Copyright (c) 2026 mrlinnth`.
- History rewrite: only the name inside files changes; commit author name `yan` stays. Done by the planner after merge (not by the builder). Out of scope for the builder.
- Screenshots are already captured (1920x965 webp, the same size as the existing 4) at:
  - `/tmp/claude-1001/-home-claude-work-yan-quest-board-landing/e9e69057-212f-4db2-90b4-0b078caf36f8/scratchpad/shots/users.webp`
  - `/tmp/claude-1001/-home-claude-work-yan-quest-board-landing/e9e69057-212f-4db2-90b4-0b078caf36f8/scratchpad/shots/branding.webp`
  The app calls the users page "Members".

## Assumptions
- Screenshot files are named `public/media/members.webp` and `public/media/branding.webp`.
- They become cards 5 and 6 in the existing 2-column grid in the `#screenshots` section, copying the existing card markup exactly (same `<a>` wrapper, classes, `width="1280" height="720"`, `loading="lazy"`).
  - members: alt "The Members admin page: a table of people with their role, level and access"; caption "Members: add people, set roles and access."
  - branding: alt "The Branding admin page with fields for the app name, tagline, logo and header image"; caption "Branding: your team's name, logo and colours."
- Do not write the owner's full name anywhere new (this file, commits, CLAUDE.md), so the history rewrite stays clean.
- `CLAUDE.md` exists untracked in the repo root; commit it as is unless a fact in it is now wrong.

## Plan
Use the Edit/Write tools for text files. Copy binary files with `cp`. Commit each step with `git-workflow-commit "<message>"` (message must start with `fix:`, `feat:`, `docs:` or `chore:`).

1. Copy the Figtree 600 woff2 to `public/fonts/figtree-latin-600-normal.woff2`. Commit: `fix: add missing Figtree 600 font file`.
2. Update the footer in `public/index.html` and line 3 of `LICENSE` as in Decisions. Commit: `fix: use GitHub handle in footer and license`.
3. Copy the two screenshots to `public/media/members.webp` and `public/media/branding.webp` (`users.webp` is renamed to `members.webp`). Add the 2 cards after the status-window card in `public/index.html`. Commit: `feat: show Members and Branding admin screenshots`.
4. Review `CLAUDE.md`, adjust anything now inaccurate, and commit it: `docs: add CLAUDE.md`.

## Done criteria
- `npm run build` succeeds. Every `url(...)` in `public/style.css` points to a file that exists under `public/`.
- `grep -rn "2026" LICENSE public/index.html` shows only `mrlinnth` / `@mrlinnth` as the copyright holder.
- `public/index.html` has 6 screenshot cards; both new images exist and are referenced.
- The footer link points to https://github.com/mrlinnth and shows `@mrlinnth`.
- No files changed outside: `public/fonts/`, `public/media/`, `public/index.html`, `LICENSE`, `CLAUDE.md`.

## Result
<Filled in after review>
