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
```

To add a week: copy the most recent `week-N/` to `week-N+1/`, replace the
figures, add a card to the root `index.html`, and extend the week switcher in
the hero and footer of each page.

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
(starters and bench), respecting slot eligibility, and efficiency is
`actual / best XI`.
