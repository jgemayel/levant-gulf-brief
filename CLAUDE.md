# Levant & Gulf Morning Brief — Operating Rules

These rules apply to every daily brief. The scheduled task `levant-gulf-morning-brief` and any manual refresh must follow them.

## Product naming
The public-facing product is called `Daily news roundup`. Do not write "Built for Jimmy" or any variant in visible output (dashboard, briefs, PWA manifest, share sheets). Internal references to Jimmy as the reader are fine inside this file.

## Audience
Jimmy advises on Syria, Iraq, Kuwait, and the Kurdistan Region of Iraq (KRG) on policy, economy, and government workstreams. Some of the items in the relevance blocks are live engagements, others are future opportunities. Keep the framing flexible.

## Country scope
Four sections every run, in this order: Syria, Iraq, Kuwait, Kurdistan. Kurdistan covers KRG-level government, fiscal and tax, power sector, oil and gas, banking, and major Erbil-level news. Federal Iraq stories stay in the Iraq section, Erbil-originated and KRG-specific stories go under Kurdistan. When a single event has both federal and KRG angles (budget transfers, Development Road, oil export regime), file it where the primary decision-maker sits and cross-reference in the summary.

## Major news rule
Beyond workstream-relevant items, surface any materially major country story from the 24 to 48 hour window even when it does not map neatly to a relevance bucket. Binding political outcomes, senior leadership changes, mass-casualty security events, FX or sovereign-rating moves, headline macro prints, and any story leading the home pages of Reuters, Al Jazeera, BBC, or the country's main local outlets all qualify. Do not let the workstream lens filter out a top-of-the-wire story, a country brief that misses the day's big headline reads as out of touch. Relevance block can be omitted for pure major-news items.

Working test before publishing: scan the Reuters, Al Jazeera, and BBC world sections plus each country's leading local wire one last time. If a story is dominating coverage and is not in the brief, either fit it in or have a concrete reason it does not belong (e.g. already covered in a prior brief, outside the 24-48 hour window, wrong country).

## Source sweep
Every run covers two layers in parallel. Both are mandatory.

Local layer, by country:
- Syria: Reuters, AP, AFP, BBC Arabic, Al Jazeera EN and AR, SANA (sana.sy, translate from AR), Enab Baladi EN and AR, The Syria Report, Syria Direct, Al-Monitor Syria, Chatham House MENA.
- Iraq (federal): Reuters, AP, Al Jazeera, The National, Iraqi News, Shafaq News EN and AR, Al-Sabaah (official, translate from AR), Iraq Oil Report, Al-Monitor Iraq.
- Kuwait: Kuwait News Agency (KUNA) EN and AR, Al-Qabas AR (translate), Al-Rai AR (translate), Kuwait Times, Arab Times, Times Kuwait, AGBI Kuwait, Arab News Kuwait, Gulf News Kuwait, Zawya Kuwait.
- Kurdistan (KRG): Rudaw EN, AR, and Kurdish (translate AR and Kurdish), Kurdistan24, Shafaq News Kurdistan desk, KRG official (gov.krd) press service, Iraq Oil Report (KRG energy), The National KRG file, Al-Monitor Kurdistan. Cover government formation, cabinet decrees, fiscal and tax, Erbil-Baghdad budget transfers, power sector, oil and gas exports, banking, and major security or political news.

Global layer, applied to every run:
- EU institutions: European Commission, Council of the EU, EEAS, European Parliament.
- US government: Treasury / OFAC, State Department, White House.
- IFIs and UN: IMF (Spring and Annual Meetings, Article IV, staff reports), World Bank, UNDP, UN Security Council, OHCHR.
- Energy bodies: OPEC+ decisions, IEA monthly reports.
- Regional security: Iran / US posture, Strait of Hormuz, Red Sea shipping, Turkey / Syria border, Turkey / KRG (PKK, airspace, trade), Israel / Lebanon / Gaza spillover. Only when the link to Syria, Iraq, Kuwait, or Kurdistan is concrete.

Global stories slot into the relevant country section, never a separate bucket.

## Recency
Only include stories published in the last 24 to 48 hours. Assume anything older was caught the day before. Do not reach back further just to pad a section. Light days are fine and preferable to stale content.

## De-duplication
Every run must cross-check against the last 5 daily briefs before drafting. Read the files directly from the local `briefs/` directory (the repo is already checked out at runtime) and extract every `<h3>` headline between `<!-- BRIEF_START -->` and `<!-- BRIEF_END -->`. If fewer than 5 dated briefs exist, check whatever is there. Refuse to publish any story whose core event is already in that set. If an event is still developing, only include it when there is a specifically new fact beyond what the prior brief already stated. When in doubt, skip rather than restate. This check is mandatory, not optional.

## High impact flag
Be calculated. Flag a story `data-priority="high"` with the "High impact" badge only when it genuinely belongs there:
- Moves a project or opportunity bucket in a concrete way (not thematic)
- Binding policy, sanctions, or fiscal action now in force or imminent
- Major geopolitical escalation or de-escalation with direct market effect

Zero high-impact flags is a valid outcome. One or two is typical on a meaningful day. Never force three. Never flag a story "high impact" just to have one in every section.

## Relevance blocks
Label the block `Relevant projects / opportunities`. Buckets by country:
- Syria: Central Bank, Banking sector, Insurance, Capital markets
- Iraq: Central Bank, Banking sector, Fiscal reforms, Economic reforms, Mega projects
- Kuwait: Government, Fiscal agenda (MoF), Economic Agenda, Public sector, Public housing & welfare, Municipality, Sovereign fund
- Kurdistan: Government, Fiscal & tax, Power sector, Oil & gas, Banking sector, Economic reforms

Include a block only when the link is concrete. Empty stories are fine, and major-news items that do not fit a bucket can run without a relevance block.

## Writing style
- No em dashes anywhere
- Minimize colons in prose
- Summaries 1 to 2 crisp sentences with concrete numbers when available
- `a.src` links must resolve to the specific article, never a homepage
- Arabic-only sources get `<span class="lang">AR</span>` in the date tag and a "Translated from [source]" note

## Output format
Write `briefs/YYYY-MM-DD.html` using the shared template. All briefs must use the unified structure so the dashboard and archive render identically. Required:
- Link the shared stylesheet `<link rel="stylesheet" href="../styles/brief.css">`. Do not inline a full stylesheet in the brief file. The shared CSS is the single source of truth for typography, colors, and story layout.
- `<body class="is-archive">`. Standalone brief pages always render with the archive variant, which is what gives them the slightly warmer background tint vs. the dashboard. The dashboard itself is the canonical "Today" view.
- Content markup inside `<!-- BRIEF_START -->` and `<!-- BRIEF_END -->` uses `<section class="country">` wrappers, with the country name in `<h3>` and each story headline in `<h4>`. This matches what the dashboard parser expects, so no tag transformation is needed when the brief is embedded in the dashboard.
- The most recent brief in `briefs/` (e.g. yesterday's file) is the canonical structural template. Copy it for the shell, then rewrite the content. If the prior brief looks like it predates the shared stylesheet (has inline `:root { --bg: #0f172a; ... }`, system-sans font, orange accents, or `<h2>` country headings), do not copy it. Fall further back or use the current day's sibling files as reference.
- Favicon `../favicon.svg` and `../apple-touch-icon.png`
- `<!-- BRIEF_START -->` and `<!-- BRIEF_END -->` markers
- Four sections in order: Syria, Iraq, Kuwait, Kurdistan. No hard cap on stories per country. Soft target is 4 to 6 stories per country on a normal day, with more on busy days and fewer on genuinely light ones. Three-per-country is not a cap, it is the floor before the day is suspiciously thin. Include every item from the 24 to 48 hour window that is genuinely relevant to Jimmy's workstreams plus any headline-level major news, including items sourced from Arabic-only or Kurdish-only local outlets. Do not hold material back to preserve a uniform shape, and do not pad thin days just to bulk up a section.
- Story IDs follow `syria-N`, `iraq-N`, `kuwait-N`, `kurdistan-N` where N runs 1 upward per country, as long as needed
- `<title>` reads `Levant & Gulf Brief · [Month] [Day], [Year]`
- Header meta line reads `[Weekday], [Month] [Day], [Year] · Syria · Iraq · Kuwait · Kurdistan`
- `og:description` meta tag must list all four countries (Syria, Iraq, Kuwait, and Kurdistan). Do not copy the three-country description from older briefs.
- Share button on each story using source URL
- Top back-to-dashboard pill + bottom nav + footer
- Footer text reads exactly `Daily news roundup. Refreshed weekday mornings.`

### Starting from a prior template
When copying structure from the most recent prior brief, do not copy it blindly. Earlier briefs may still use a three-section (Syria / Iraq / Kuwait) shape, a three-country meta line, or a three-country `og:description`. Today's brief must always have four sections and the four-country strings above, regardless of what the last file looked like. Also do not copy the `og:description` wording from the prior brief verbatim, since it is keyed to that date's content mix — write fresh four-country prose.

## Local Arabic and Kurdish coverage
Arabic-only and Kurdish-only local outlets are first-class sources, not afterthoughts. Sweep them on every run (SANA, Enab Baladi AR, BBC Arabic, Al Jazeera AR for Syria; Al-Sabaah, Shafaq AR for Iraq; Al-Qabas AR, Al-Rai AR, KUNA AR for Kuwait; Rudaw AR and Kurdish, Shafaq KRG, KRG gov.krd AR for Kurdistan). When the core fact is strongest in Arabic or Kurdish, lead with that source. Provide a translated English summary in the story body, mark the date tag with `<span class="lang">AR</span>` or `<span class="lang">KU</span>`, and append `Translated from [source].` at the end of the summary.

## Dashboard (PWA)
The root `index.html` is a progressive web app called `Daily news roundup`. It renders today's brief inline (parsing between `<!-- BRIEF_START -->` and `<!-- BRIEF_END -->` from the latest dated file) and lists prior briefs as an archive. Companion files: `manifest.webmanifest`, `service-worker.js`, and `styles/brief.css` (shared stylesheet used by both the dashboard and every standalone brief page). The dashboard pulls today's brief dynamically, so no `index.html` edits are needed per run. If the dashboard chrome, manifest, service worker, or shared stylesheet change, bump the `CACHE` constant in `service-worker.js` to force a clean install for existing users.

## Publish (mandatory final step)
Every run ends with a git commit and push. Without it, the dashboard has nothing to show and the run is incomplete. Never skip this step, even on light days.

Preferred path (the working directory is always a local clone of the repo):
```
git add briefs/YYYY-MM-DD.html
git commit -m "Daily brief YYYY-MM-DD"
git push origin main
```
Confirm `git push` prints a new commit range on `main` before declaring the run done. If push fails, run `git pull --rebase origin main` and retry; do not exit the run on a failed push.

Fallback path (only if the working directory is not a git checkout): PUT to `https://api.github.com/repos/jgemayel/levant-gulf-brief/contents/briefs/YYYY-MM-DD.html` with the GitHub token. If the file exists, include its SHA; if new, omit SHA. Commit message `Daily brief YYYY-MM-DD`. Confirm the PUT response contains a `commit.sha`.

No `index.html` edits needed; the dashboard pulls today's brief dynamically.

## Runtime discipline
The scheduled task has a single responsibility: get the brief written and pushed. A few things that will silently eat a run if ignored:
- Web research tools (WebSearch, WebFetch) may be exposed as deferred tools that need schema loading via ToolSearch. Load them in the first turn, then move straight into the sweep. Do not pause mid-run to explore tooling.
- If a prior run's brief is missing (e.g. the last scheduled fire stopped early), do not assume "yesterday" is today. Always drive the filename from `date +%F` in the working shell, not from the latest file in `briefs/`.
- Do not finish the run with uncommitted files in the working tree. Always verify with `git status` that the working tree is clean after the push. If the scheduled task was interrupted and files are staged or modified, complete the push before starting fresh research.
