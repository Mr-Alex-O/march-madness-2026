# March Madness 2026 — Alex vs Greg
## Site: https://mr-alex-o.github.io/march-madness-2026

---

## Teams
**Alex (Green):** Duke, Siena, TCU, South Florida, Michigan St, UCLA, Connecticut, Furman, Florida, PV/LEH (Prairie View), Clemson, Vanderbilt, Nebraska, Troy, VCU, St Marys, Texas A&M, Houston, Villanova, Utah St, High Point, Hawaii, Gonzaga, Missouri, Michigan, UMBC/HOW (Howard), Georgia, Akron, Alabama, Tennessee, Wright St, Kentucky

**Greg (Yellow):** Ohio St, St Johns, Northern Iowa, Kansas, California Baptist, Louisville, N Dak St, UCF, Iowa, McNeese, N Carolina, Illinois, Pennsylvania, Idaho, Arizona, LIU Brooklyn, Wisconsin, Arkansas, BYU, TX/NCST (Texas), Kennesaw St, Miami (FL), Purdue, Queens University, Saint Louis, Texas Tech, Hofstra, MOH/SMU (Miami OH), Virginia, Santa Clara, Iowa St, Tennessee St

---

## Money Scoring
- Elite Eight: $5 per team
- Final Four: $10 per team
- Finals (Championship game): $15 per team
- Champion: $20
- At the end: subtract lower from higher score, display difference (e.g. "Alex won $40")

---

## Changelog

### v1.9 — Fixed team colors + black background
- Each team in the bracket now has a hardcoded `owner` field ('alex'/'greg') — colors no longer rely on name matching
- Fixes Iowa State and Tennessee State wrongly showing as Alex's teams (previously confused with Iowa/Tennessee)
- Background changed to pure black (was dark navy gradient)
- nameMatch threshold tightened (≤3 chars) to prevent short names like "Iowa" from matching "Iowa State"

### v1.6 — Live Games tab + color overhaul
- Added 🔴 Live tab as first tab — shows all currently live games as big cards with score, period, time remaining
- Team colors (green/yellow) now ONLY show on live games — completed games show neutral colors
- Live game status chip shows half/period + clock (e.g. "2nd Half · 5:23")
- Removed hardwood floor background — replaced with easy dark navy gradient

### v1.5 — Auto-refresh
- Scores auto-refresh every 60 seconds
- Pauses when screen/tab is not visible
- Manual refresh button resets the 60s countdown
- Countdown shows in the "Updated X" line

### v1.4 — Hardwood floor + upset label
- Background changed to CSS hardwood basketball floor (wood plank lines + grain)
- Upset tag simplified to just "🔥 UPSET" shown as a red banner below the matchup score box

### v1.3 — Upset banner
- Upset now shown as a dedicated red banner row below the matchup
- Shows full upset info clearly without truncation

### v1.2 — Mobile fit + zoom lock
- Column widths shrunk on mobile so all 4 rounds (R64→R32→S16→E8) fit on screen without scrolling
- Viewport locked so you can zoom IN but not zoom OUT past page load

### v1.1 — Teams remaining + mobile fixes
- "X teams left" counter shown under each player's score
- Title scales to fill header width
- Sticky tab navigation bar (stays at top when scrolling)
- Team colors (green/yellow) now carry through to Round of 32+ on advancement

### v1.0 — Initial launch
- Full bracket with East, West, South, Midwest + Final Four tabs
- Full Bracket tab with All/Alex/Greg filter buttons
- West and Midwest columns reversed (E8 → R64) to mirror real bracket layout
- R64 games grouped in pairs so it's clear who plays who
- Auto-advances winners to next round slots
- Live score update button via ESPN public API
- PWA home screen icon (basketball design, "MM" in gold)
- App manifest + apple-touch-icon for iPhone/Android install
- Version number at bottom of page

---

## Architecture
- Single file: `index.html` (no build tools, no dependencies)
- Hosted on GitHub Pages: repo `Mr-Alex-O/march-madness-2026`
- Icons: `icon.svg` (basketball SVG), `manifest.json` (PWA)
- Live scores: ESPN public API — `site.api.espn.com/apis/site/v2/sports/basketball/mens-college-basketball/scoreboard?dates=YYYYMMDD`
- Bracket data hardcoded in JS `DATA` object — update `status`, `winner`, `score1`, `score2` fields as games complete
- `advanceWinners()` auto-propagates winners through rounds on every render
