# Ford Fight Lab — Project Plan & Ownership Record
_Created 2026-08-23 (the night it was built). Owner-to-be: Patrick's nephew ("JP"). Custodian: Patrick Boyd._

## What this is
A fight-breakdown site + podcast home for Patrick's nephew: fighting-style breakdowns,
fighter profiles, fight history with video, and podcast episodes. Built in one evening,
2026-08-22 → 23.

## Architecture (deliberately zero-cost, zero-server)
| Piece | Where | Cost |
|---|---|---|
| Domain fordfightlab.com | Namecheap (Patrick's account, registered 2026-08-23) | ~$12/yr — the ONLY cost |
| Site hosting | GitHub Pages, repo `UncleDumpyMusic/fordfightlab`, branch `main` | free |
| HTTPS | GitHub-managed Let's Encrypt, enforced (http 301s to https) | free |
| DNS | Namecheap: 4× A @ → 185.199.108-111.153, CNAME www → uncledumpymusic.github.io | free |
| Podcast audio | Spotify for Creators (creators.spotify.com) — NOT our storage; embeds on podcast.html | free |
| Videos | YouTube embeds/links only — never upload fight footage (copyright) | free |

**This is intentionally NOT on the MTVK platform** — family project, isolated from the
money codebase, no Railway, no Supabase. If it ever migrates to MTVK (after 10 paying
accounts), treat as a normal brand onboarding.

## Site structure
- `index.html` — hero with logo, section tiles
- `styles.html` — 8 fighting-style breakdowns · `fighters.html` — 6 starter profiles (facts verified)
- `fights.html` — 6 legendary fights; "Watch on YouTube" = search links by design (no
  guessed video IDs); nephew pastes real VIDEO IDs for inline players (template in page comment)
- `podcast.html` — episode-card pattern awaiting Spotify embeds; setup note on page
- `README.md` — the owner's editing guide (displays on repo front page = his command center)
- `css/style.css` — theme tokens in `:root`; brand green `#42f305` sampled from the logo
- `assets/` — logo-source-original.jpg (Grok generation, via Patrick 2026-08-22),
  logo-ford.png (transparent via border flood-fill — silhouettes inside letters survive),
  icon-512/192, apple-touch-icon (full wordmark on black), og-image.jpg (1200×630).
  **All variants cropped from the ONE source** — regenerating any size separately is forbidden
  (style drift). Background: inline SVG fight-area pattern (ring/octagon/circle/triangle) in CSS.

## Editing model ("his command center")
GitHub repo page = command center. Pencil-icon edit → commit → live in ~1 min.
Guide is the README. Works from phone; `.` opens web VS Code. History = undo for everything.

## Ownership & transfer plan (the point of the whole setup)
Goal: nephew FULLY owns everything. Two moves when ready:
1. **Repo transfer** — GitHub Settings → Transfer ownership → his account (free, keeps history;
   Pages custom domain may need re-save + cert re-issue after — 10-min job).
2. **Domain push** — Namecheap → Change Ownership → push to HIS Namecheap account (free,
   instant, no 60-day lock). ⚠️ **Namecheap requires 18+.** If he's a minor: transfer the repo
   now, Patrick stays domain custodian until 18, then push. (GitHub allows 13+.)
3. Podcast: his Spotify account from day one — never anyone else's.

## Pending (blocking items)
- [ ] Nephew's GitHub username → Patrick tells CC → add as collaborator (Settings → Collaborators)
- [ ] Nephew signs up at creators.spotify.com, uploads ep. 1, pastes Share→Embed iframe into podcast.html
- [ ] Nephew's first edit session: replace fight search-buttons with his picked YouTube video IDs
- [ ] Decide repo-transfer timing (and confirm his age for the domain question)

## Ops notes (hard-won, 2026-08-22/23)
- **GitHub Pages cert stuck at state None** despite green `/pages/health` → unstick with
  remove/re-add: `PUT /repos/{o}/{r}/pages {"cname":null}` then re-set cname → state moves to
  `authorization_pending` → issued in minutes → then PUT `https_enforced:true`.
- Changing the Pages cname via API makes **GitHub auto-commit CNAME changes** to the repo —
  `git pull --rebase` before pushing local work.
- Namecheap `setHosts` REPLACES ALL records (getHosts first). API requires whitelisted source
  IP — Patrick's entry "New Home" = 192.198.57.219 (added 2026-08-23).
- iMessage link previews are built+cached per-URL on the SENDER's phone — a link sent before
  DNS/cert settled shows a blob card forever; resend with `?v=2` to rebuild. Site unaffected.
- A stale local DNS cache serving Namecheap parking gives a content-type-less 404 that
  browsers treat as a DOWNLOAD — flush with `dscacheutil -flushcache` + `sudo killall -HUP mDNSResponder`.
- Facts rule (from MTVK): fighter records/dates get verified before publish, never guessed.
