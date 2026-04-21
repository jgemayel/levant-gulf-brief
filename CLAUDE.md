# Levant & Gulf Morning Brief — Operating Rules

These rules apply to every daily brief. The scheduled task `levant-gulf-morning-brief` and any manual refresh must follow them.

## Audience
Jimmy advises on Syria, Iraq, and Kuwait policy, economy, and government workstreams. Some of the items in the relevance blocks are live engagements, others are future opportunities. Keep the framing flexible.

## Source sweep
Every run covers two layers in parallel. Both are mandatory.

Local layer, by country:
- Syria: Reuters, AP, AFP, BBC Arabic, Al Jazeera EN and AR, SANA (sana.sy, translate from AR), Enab Baladi EN and AR, The Syria Report, Syria Direct, Al-Monitor Syria, Chatham House MENA.
- Iraq: Reuters, AP, Al Jazeera, The National, Iraqi News, Rudaw EN and AR and Kurdish, Shafaq News EN and AR, Al-Sabaah (official, translate from AR), Iraq Oil Report, Kurdistan24.
- Kuwait: Kuwait News Agency (KUNA) EN and AR, Al-Qabas AR (translate), Al-Rai AR (translate), Kuwait Times, Arab Times, Times Kuwait, AGBI Kuwait, Arab News Kuwait, Gulf News Kuwait, Zawya Kuwait.

Global layer, applied to every run:
- EU institutions: European Commission, Council of the EU, EEAS, European Parliament.
- US government: Treasury / OFAC, State Department, White House.
- IFIs and UN: IMF (Spring and Annual Meetings, Article IV, staff reports), World Bank, UNDP, UN Security Council, OHCHR.
- Energy bodies: OPEC+ decisions, IEA monthly reports.
- Regional security: Iran / US posture, Strait of Hormuz, Red Sea shipping, Turkey / Syria border, Israel / Lebanon / Gaza spillover. Only when the link to Syria, Iraq, or Kuwait is concrete.

Global stories slot into the relevant country section, never a separate bucket.

## Recency
Only include stories published in the last 24 to 48 hours. Assume anything older was caught the day before. Do not reach back further just to pad a section. Light days are fine and preferable to stale content.

## De-duplication
Every run must cross-check against the last 5 daily briefs. Fetch them from the GitHub contents API, extract all `<h3>` headlines between `<!-- BRIEF_START -->` and `<!-- BRIEF_END -->`, and refuse to publish any story whose core event is already covered. If the event is still developing, advance the angle with a specifically new fact, or skip it.

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

Include a block only when the link is concrete. Empty stories are fine.

## Writing style
- No em dashes anywhere
- Minimize colons in prose
- Summaries 1 to 2 crisp sentences with concrete numbers when available
- `a.src` links must resolve to the specific article, never a homepage
- Arabic-only sources get `<span class="lang">AR</span>` in the date tag and a "Translated from [source]" note

## Output format
Write `briefs/YYYY-MM-DD.html` using the template established by prior briefs. Required:
- Favicon `../favicon.svg` and `../apple-touch-icon.png`
- `<!-- BRIEF_START -->` and `<!-- BRIEF_END -->` markers
- Three sections (Syria, Iraq, Kuwait), up to 3 stories per country, 9 total on a full day
- Story IDs syria-1..3, iraq-1..3, kuwait-1..3
- Share button on each story using source URL
- Top back-to-dashboard pill + bottom nav + footer

## Publish
PUT to `https://api.github.com/repos/jgemayel/levant-gulf-brief/contents/briefs/YYYY-MM-DD.html` with the GitHub token. If the file exists, include its SHA. Commit message `Daily brief YYYY-MM-DD`. No index.html edits needed; the dashboard pulls today's brief dynamically.
