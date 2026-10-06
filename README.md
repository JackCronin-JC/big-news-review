# Big News Review

Weekly fantasy football review for the Sleeper league *Dont tell your motha*.

Figures are pulled from the public Sleeper API and computed, not estimated:
positional leaders, optimal lineups, manager efficiency, and the injury list.

Live page: https://jackcronin-jc.github.io/big-news-review/

## Layout

Each week is its own page under a `week-N/` folder. The root page is the
archive index, with the latest week pinned at the top.

```
/                 archive index — every week, newest first
/week-1/          Week 1
/week-2/          Week 2
/week-3/          Week 3
/week-4/          Week 4, plus redzone.mp4: a two-minute whip-around video
                  (stock macOS voice, captions in redzone.vtt)
```

To add a week: copy the most recent `week-N/` to `week-N+1/`, replace the
figures, add a card to the root `index.html`, and extend the week switcher in
the hero and footer of each page.

A player who was dropped before his game is on no roster, so his points are not
in the matchup data. Those come from `/stats/nfl/regular/{season}/{week}`, scored
with the league's own `scoring_settings` (checked to reproduce every rostered
player's matchup points exactly before being trusted).

## Where the numbers come from

League `1389724530838114304`, 10-team PPR, starters
`QB / RB / RB / WR / WR / TE / W-R FLEX / K / DEF`.

| Figure | Endpoint |
| --- | --- |
| Scores, starters, bench | `/league/{id}/matchups/{week}` |
| Records and season points | `/league/{id}/rosters` |
| Team and manager names | `/league/{id}/users` |
| Player names, teams, injuries | `/players/nfl` |
| Adds, drops, waivers | `/league/{id}/transactions/{week}` |

"Best XI" and lineup efficiency are computed, not reported by Sleeper: the
best legal lineup is selected from every player on the roster that week
(starters and bench), and efficiency is `actual / best XI`. Two rules apply
to the best XI and to every "should have started X" line in the copy:

- **Slot eligibility.** The flex is `WRRB_FLEX` — receivers and running backs
  only. A tight end can only ever fill the TE slot, so a WR-for-TE swap is
  never legal.
- **Startability.** A player only counts if he was on the roster before his
  own kickoff and before the kickoff of the player who actually held that
  slot (the slot locks when its incumbent's game starts). Kickoff times come
  from ESPN's scoreboard.

Each week covers that week's games only. Once the next week's Thursday game
has been played, `/league/{id}/rosters` and `/matchups/{week+1}` already carry
its points, so the table is computed from `/matchups/1..N`, never from the
running totals, and injuries or transactions from that Thursday game are left
out.
