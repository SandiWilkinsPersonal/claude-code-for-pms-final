# Weekly support-ticket counts, for comparison with Ravi's acceptance numbers

Source: rook-database `support_tickets`, 29 Jun to 7 Sep 2026, 147 tickets. Grouping is in `support-ticket-groups.md`.
Weeks start on Monday, by `filed_at`. 4.2 shipped Wed 12 Aug, so it falls inside the week starting 10 Aug.

- **Quiet** = group 1, responder has gone quiet (30 tickets).
- **Gone** = group 2, ping gone before they could answer (16 tickets).
- **All other** = groups 3 to 7.

| Week starting | Quiet | Gone | All other | Total |
|---|---|---|---|---|
| 29 Jun | 0 | 0 | 6 | 6 |
| 6 Jul | 0 | 0 | 6 | 6 |
| 13 Jul | 0 | 1 | 7 | 8 |
| 20 Jul | 0 | 0 | 5 | 5 |
| 27 Jul | 0 | 0 | 7 | 7 |
| 3 Aug | 0 | 0 | 7 | 7 |
| **10 Aug (4.2 ships 12 Aug)** | 0 | 7 | 13 | 20 |
| 17 Aug | 8 | 3 | 16 | 27 |
| 24 Aug | 12 | 3 | 17 | 32 |
| 31 Aug | 8 | 2 | 15 | 25 |
| 7 Sep (Monday only, partial) | 2 | 0 | 2 | 4 |

## What the counts show

- **Before 4.2 (29 Jun to 9 Aug):** 5 to 8 tickets a week. One "Gone" ticket (3014, out of signal) and no "Quiet" tickets.
- **"Gone" tickets arrive first.** 7 in the week of 10 Aug, 3, 3, then 2. Fifteen of the 16 are dated 12 Aug or later.
- **"Quiet" tickets lag by about a week.** None until 17 Aug, then 8, 12, 8. A handler needs several days of silence before filing.
- **Not improving.** The 31 Aug week is still 25 tickets, against 5 to 8 before 4.2.
- **"All other" also rose**, from 5 to 7 a week to 13 to 17. I haven't checked why. Some of it is likely the 4.2 filter-persistence follow-ups and possibly more filing overall.

## Cautions

- Tickets count handlers who bothered to write in. Meteor Mite and Vesper collapsed in the ping data but have no tickets.
- The grouping is my judgement from reading each ticket. Ravi's numbers come straight from the pings table.
- The week of 7 Sep holds one day of data. Don't read it as a drop.
- Tickets are filed days after the event, so lines up against Ravi's weeks with a lag.

## Question for Ravi

Acceptance by week split by responder, ideally with misses per responder per week. The Quiet tickets name Farlight, The Undertow, Corporal Ashgrove and Halfmoon. Farlight and The Undertow are the severe ones.
