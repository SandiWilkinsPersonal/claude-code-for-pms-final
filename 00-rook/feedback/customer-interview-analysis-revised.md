# Customer interview analysis: revised after re-checking against the data

Re-check of my earlier interviews-versus-tickets analysis against the per-responder pings, the ticket text and the code.
Sources: wiki Customer interviews (4 calls, 2 to 5 Sep 2026), rook-database `support_tickets` and `pings`, `00-rook/feedback/` files.
Nothing here has been posted anywhere.

## Summary

The interviews and tickets agree on 4.2 but neither leads with it. Handlers describe pings vanishing before they can answer (Ambrose, Dot, Halloran) and responders going quiet (Kip, Dot). The pings data shows both: misses rose for all 16 responders after 4.2, and four (Farlight, Meteor Mite, The Undertow, Vesper) fell to about one ping a week. Console polish asks (dark mode, alert sounds, badge size) appear in both piles at about two tickets each.

Not yet confirmed: whether the penalty and no-decay logic caused the drop, and Ambrose's timeline. Both depend on production scores from Wen Li and Marcus.

## What held up

- The 4.2 problem shows up in both piles and is the main complaint in neither.
- The quiet side is under-ticketed: Meteor Mite and Vesper have zero tickets.
- Interviewees and ticket filers barely overlap. Ambrose is the only handler in both (ticket 3043).

## Corrections to the earlier version

1. **Console polish is in both piles.** Dark mode (3029, 3105), alert sounds (3031, 3127) and status badge size (3013, 3142) are each 2 tickets. My earlier "text size, about 4" count included two filter-badge tickets (3061, 3124). Each pair has identical opening text from different handlers, so the distinct-complaint count may be lower than it looks. Dot's ask for a handler-side alert still has no ticket.
2. **Halloran and Sgt. Bulwark are not a null case.** Bulwark's misses went from 0 a week to 1 or 2 from the week of 10 Aug, and his pings stayed at 10 or 11. He is in the group that missed more but stayed in rotation, which matches his August comment. Do not use him as evidence of uneven impact.
3. **Priority needs a qualifier.** The quiet half is still the most severe. But the "gone" half touches all 16 responders and has the better-supported explanation (the 60 s ping wait). The compounding story rests on a stub, and `routing.py` only reorders and never removes anyone, so it is the leading hypothesis, not a finding.
4. **Ambrose's timeline is inconsistent.** Ticket 3043 (filed 13 Aug) says "yesterday evening", which is 12 Aug, the day 4.2 shipped. His 2 Sep interview says "two weeks ago", about 19 Aug. It could be one event told loosely, or two. Ask him.

## One addition

The Undertow and Farlight account for 21 and 19 of the 147 tickets (40 combined). Some are likely on other topics, since both have tickets from early July. So "ticket volume understates the problem" holds for Meteor Mite and Vesper only.

## Provenance cautions (carried over)

- Interviews are published excerpts from a console-redesign study, with four handlers chosen by the designer (how, unknown).
- The seven ticket groups are my own reading of each ticket, formed after I had a view of the 4.2 problem.
- The pings table is the only source with no selection step.

Related files: `support-ticket-groups.md`, `weekly-ticket-counts-for-ravi.md`, `responder-weekly-pings-for-ravi-conversation.md`, `drafts-wen-li-and-marcus.md`.
