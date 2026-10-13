# Per-responder weekly pings, for the conversation with Ravi

Source: rook-database `pings`, 29 Jun to 31 Aug 2026 (no rows for the week of 7 Sep). Weeks start Monday, by `sent_at`.
4.2 shipped Wed 12 Aug, so it falls inside the week starting 10 Aug.
This is my own query, not Ravi's numbers. Ravi owns the weekly acceptance figures; use this to ask him to check and extend it.

Each cell is **pings (taken / missed)**. Turned-down pings are the remainder (pings minus taken minus missed).

| Responder | 29 Jun | 6 Jul | 13 Jul | 20 Jul | 27 Jul | 3 Aug | **10 Aug** | 17 Aug | 24 Aug | 31 Aug |
|---|---|---|---|---|---|---|---|---|---|---|
| **Farlight** | 12 (9/0) | 12 (9/0) | 11 (8/1) | 12 (9/1) | 13 (10/0) | 12 (8/1) | 10 (4/4) | 3 (0/2) | 1 (0/1) | 0 |
| **Meteor Mite** | 11 (7/0) | 12 (9/0) | 10 (6/0) | 11 (7/1) | 12 (9/1) | 11 (8/0) | 10 (4/4) | 4 (1/2) | 2 (0/1) | 1 (0/1) |
| **The Undertow** | 12 (9/0) | 11 (9/0) | 12 (9/1) | 13 (10/0) | 12 (10/0) | 12 (9/0) | 11 (4/5) | 4 (1/2) | 1 (0/1) | 1 (0/1) |
| **Vesper** | 14 (11/0) | 13 (10/1) | 15 (13/1) | 14 (11/0) | 13 (11/1) | 14 (12/0) | 12 (6/4) | 5 (1/3) | 2 (0/1) | 1 (0/1) |
| Corporal Ashgrove | 10 (8/0) | 11 (9/0) | 10 (7/1) | 9 (7/0) | 10 (8/0) | 10 (8/0) | 10 (6/1) | 8 (5/1) | 7 (5/1) | 7 (5/1) |
| Halfmoon | 11 (8/0) | 10 (7/0) | 11 (8/0) | 12 (8/0) | 11 (9/0) | 11 (8/0) | 11 (6/2) | 9 (5/2) | 8 (5/1) | 8 (7/0) |
| Captain Vantage | 12 (10/0) | 13 (10/1) | 12 (8/0) | 11 (7/1) | 12 (9/0) | 12 (9/0) | 13 (8/1) | 15 (11/2) | 17 (13/1) | 18 (13/2) |
| Cindermark | 9 (7/0) | 9 (8/0) | 8 (6/1) | 10 (7/0) | 9 (7/0) | 9 (8/0) | 10 (6/1) | 11 (8/1) | 12 (8/2) | 12 (9/1) |
| Ironvale | 8 (6/0) | 8 (5/0) | 9 (8/0) | 8 (6/0) | 7 (5/1) | 8 (7/0) | 9 (5/1) | 10 (6/2) | 11 (8/2) | 12 (9/2) |
| Nightwell | 15 (11/1) | 14 (10/0) | 15 (12/1) | 16 (12/1) | 15 (11/0) | 15 (12/0) | 16 (9/2) | 18 (14/2) | 20 (13/2) | 21 (15/2) |
| Sgt. Bulwark | 9 (7/0) | 9 (7/0) | 10 (8/0) | 9 (7/0) | 8 (5/0) | 9 (7/0) | 10 (5/2) | 10 (8/1) | 11 (7/2) | 11 (8/2) |
| Sgt. Falkirk | 10 (9/1) | 10 (8/1) | 11 (8/0) | 10 (8/0) | 9 (7/0) | 10 (8/0) | 11 (7/2) | 13 (9/2) | 15 (11/2) | 16 (11/2) |
| Stormwrack | 13 (10/0) | 13 (11/0) | 12 (9/0) | 14 (12/0) | 13 (10/0) | 13 (10/0) | 14 (8/3) | 16 (12/2) | 18 (13/2) | 19 (15/2) |
| The Drift | 6 (5/0) | 6 (5/0) | 7 (6/0) | 6 (5/0) | 6 (5/0) | 6 (5/1) | 7 (4/2) | 7 (5/1) | 8 (6/1) | 8 (5/1) |
| The Gale | 13 (10/1) | 12 (9/0) | 13 (10/0) | 14 (11/1) | 13 (11/1) | 13 (10/0) | 15 (9/3) | 17 (12/2) | 20 (14/2) | 21 (16/2) |
| The Longcast | 7 (5/0) | 7 (5/1) | 8 (7/0) | 7 (5/0) | 7 (5/0) | 7 (5/0) | 8 (5/1) | 8 (6/1) | 9 (5/2) | 9 (7/1) |

## What it shows

- **Four responders collapsed** (Farlight, Meteor Mite, The Undertow, Vesper). Each had 0 or 1 misses a week before 4.2, then 4 or 5 in the week of 10 Aug, then almost no pings. Farlight has none in the week of 31 Aug.
- **Corporal Ashgrove and Halfmoon** are milder: about 30% fewer pings, with 1 or 2 misses a week.
- **Everyone else gained pings** (The Gale and Nightwell 13/15 to 21; Stormwrack, Captain Vantage and Sgt. Falkirk up about 6) and missed more than before, 1 to 3 a week.
- **Misses rose across the board after 4.2.** Consistent with the 60 s ping wait. Only the four dropped out of the rotation.
- **Why these four is not shown here.** No response-time data. The weights and ping wait shipped together, so this table cannot separate them.

## Questions for Ravi

1. Can you rerun this on your side and confirm it matches?
2. Acceptance by week split by responder, including turned-down, and the weeks of 7 Sep onward.
3. Do you have response times (ping sent to answer) per responder? That would show whether the four were slower to answer before 4.2.
4. Is there a source for capability tags or location by responder, so we can rule those out?

## Cautions

- Counts are pings, not unique callouts.
- The week of 7 Sep has no rows in this table, so any "recovery" after 31 Aug is unknown.
- Related files: `support-ticket-groups.md`, `weekly-ticket-counts-for-ravi.md`.
