# Draft messages: confirm the ping penalty behaviour against production

Not sent. Drafted in Sandi's voice. Evidence: `responder-weekly-pings-for-ravi-conversation.md`, code in `00-rook/code/dispatch-routing` (`config.py` 18-19, `history.py` 30-39, `routing.py` 18-27).

## To Wen Li (DM)

Hi Wen,

I'm the new PM for Dispatch. I took over from Priya in August. Marcus said you're the person to talk to about how we decide who gets pinged.

I've read the routing code in the repo, but it looks like a stub, so I don't want to assume it matches what's live. Could we find 20 minutes this week?

These are the things I'd like to check:

- Is a missed ping penalised the same as a turn-down, and is it still 0.12 against 0.08 for a take?
- Is there any decay or reset on the acceptance score, or does the 2019 TODO still stand?
- Did 4.2 reset or rescale anyone's score?
- Could you show me the current scores for Farlight, Meteor Mite, The Undertow and Vesper, and for The Gale and Nightwell?

Marcus also asked on 14 Aug whether the new weighting should treat low-acceptance responders differently, and I haven't found an answer. I'd like to know whether that was a decision or fell out that way.

Happy to work around your time zone.

Thanks.

## To Marcus

Hi Marcus,

Thanks for offering to regroup on 4.2 once I'd had a week. I've had a bit more than that, so I'd like to get it on the calendar.

I pulled per-responder pings from the database. Four responders (Farlight, Meteor Mite, The Undertow and Vesper) were getting 10 to 14 pings a week before 4.2. They each missed 4 or 5 in the week of 12 Aug and are now down to about one a week. The others went up. I think the penalty and no-decay logic is involved, but I haven't confirmed it, and I know the repo is a stub.

Three questions:

- Can eng pull the current recent-acceptance scores per responder, so I can see whether those four are at the floor?
- Can we tell whether the 60 s ping wait or the weights caused this? The two shipped together. I don't know if a replay under the old and new values is practical.
- If the logic does turn out to be the cause, is a small fix something eng would consider, or do you want a one-pager first?

I'm going to talk to Wen as well, so I'll share what I learn.

Thanks.
