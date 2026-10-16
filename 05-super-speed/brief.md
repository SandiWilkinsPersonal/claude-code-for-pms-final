# Product brief: A way back for quiet responders

One-pager · Product, Dispatch · Draft for Helen Achebe · Owner: Dispatch PM
Status: draft, for discussion before any code changes. Not yet reviewed by engineering.

## Why now
Since 4.2 (12 Aug), 4 of our 16 responders (Farlight, Meteor Mite, The Undertow, Vesper) have almost stopped getting pings: about 70-86 pings before 4.2, down to roughly one a week by late August, and none taken since. Vesper was taking about 8 in 10 pings before. They didn't recover on their own. In the code as we read it, a responder's score only changes when they answer a ping, nothing fades with time, and a missed ping costs more (0.12) than a taken one earns (0.08). Once someone is pinged rarely, there is no way to climb back. Wen Li flagged this years ago; nobody came back to it.

Meanwhile the other responders absorbed the work (about 20% more pings), and handlers see the effect without the cause. Kip has one responder texting "is something broken?" and another who "hasn't stopped, at all", on two cards side by side.

## Who it's for
**Primary: the responder who has gone quiet.** Someone who answered most pings, missed a run of them (often around the 90 to 60 second cut), and now sits at the bottom of the order. Today their phone just doesn't go off, and they have no idea why. Today that's four responders; it will be anyone who has a bad week.

**Secondary: the handler of that responder (Kip, Aunt Dot).** Handlers are the ones who get the texts and tickets. They can't see the difference between "quiet because it's slow" and "quiet because Dispatch has stopped choosing them", and they can't tell their responder anything true.

**Also benefits: the responders who picked up the slack.** The Gale is "exhausted". Spreading load back out helps them without anyone asking.

## What changes for them
**For a quiet responder:**
- They get pinged again. A responder who stops getting pings is brought back into the order after a set period, without needing to take a ping first.
- A single run of missed pings no longer parks them at the bottom indefinitely. A miss is treated as less serious than a deliberate turn-down. (Today they cost the same, or more.)
- If they miss again on their way back, they are not pushed deeper out of rotation.
- **No one is left out.** An available, qualified responder can't go more than N days without a ping (N for engineering to propose; design goal: about a week). This holds whatever the underlying cause turns out to be, which matters because the score alone doesn't explain Vesper.
- **A second miss doesn't quietly drop them again.** If a returning responder misses several pings in a row, the case goes to their handler and Support (Nadia) instead of silently sinking.

**For a handler like Kip:**
- Each responder card says in plain words how that responder is doing in rotation (illustrative wording only, untested: "Pinged 12 times this week"). No scores, no formulas.
- When a responder is quiet because of the ranking and not because the work is quiet, the card says so, so Kip can tell Meteor Mite something true instead of "hang in there". Whether we can know this, and whether handlers should see it, is open (see below).
- Two cards on the same screen stop looking like "two different products".

**What the console does not need handlers to do:** nothing to configure and no new step in the callout flow.

## What it deliberately does not do
- **Not a setting.** No handler-adjustable weight, timer or switch. Routing config still ships with the release (per the Dispatch one-pager). Helen asked for something people notice, not a control.
- **Does not revert 4.2.** Proximity weighting was a long-standing responder ask and stays. The 60 second ping wait is not changed here either; that is its own decision (see open questions).
- **Does not fix "gone before I could answer".** That third of the tickets is explained by the shorter wait and is a separate problem. Not solved by this brief.
- **Does not make turning jobs down cheaper.** The change is about missed pings. Responders who turn jobs down (Sgt. Bulwark and Captain Vantage were about 25% before 4.2) keep the same cost for it, so "recent acceptance" still separates them from everyone else. Whether any fading applies to turn-downs is open; the default here is that it doesn't.
- **Does not guarantee anyone a share of callouts.** No quotas or fairness targets. A responder who keeps missing can still rank low; the change is that it isn't permanent and doesn't compound.
- **Does not expose scores or reasons about individuals to other responders.** Handlers see their own responders only.
- **Does not use or infer legal identity.** Everything works on cover identity and callout history (Security Policy 4.1).
- **Does not change the Responder Availability Record.** Supply reads it; if that ever has to change, Supply hears first.
- **Does not build a handler phone app, dark mode, or per-responder alert sounds.** Those asks came up in the same interviews and stay on their own tracks.

## How we'll know it worked
Baselines are from the pings table (29 Jun to 6 Sep).
- **Rotation:** the four quiet responders are back near their pre-4.2 pings per week (Vesper about 14) within a few weeks of release. Proposed; to agree with Marcus and Ravi.
- **Tickets:** "my phone never goes off" tickets drop from about 20 a week back toward the pre-4.2 level (5 to 8 a week all-in).
- **Untaken callouts:** share of callouts nobody took returns toward 5.5% (it was 11.1% after 4.2).
- **Vesper test (pass/fail):** replaying the real pings table through the new rules, Vesper is back to a stated number of pings a week within two weeks of the change (baseline about 14 a week before 4.2). If Vesper doesn't pass, the design isn't done, whatever the other three do.
- **Recurring check:** a weekly report, owned by Ravi, listing any available responder with no ping for 7 days, so we find the next quiet responder before the tickets do.
- **No one pays for the fix:** no responder who was fine before 4.2 loses more than an agreed share of their pings (share to agree with Marcus and Ravi). Expect The Gale, Nightwell and others who gained after 4.2 to give some back.
- **Guardrail:** overall acceptance and time-to-accept don't get worse. We also report acceptance **per responder**, not only in aggregate, because the aggregate hid this for weeks.

## Open questions
1. **Is the code what production does?** Our copy of `dispatch-routing` is a simplified stub. We need production scores for the four from Wen Li or Marcus before building anything.
2. **Timer or score?** The 60 second wait and the scoring weights shipped together, and we have no response-time data (`pings` has no response time). A responder may be missing because 60 s is too short for them, in which case a score change alone won't bring them back. Ask Ravi for response times. Vesper still scored well on 17 Aug despite falling pings, so the score isn't the whole story.
3. **Was the penalty a decision?** Marcus's 14 Aug question (should the new weighting treat people already turning jobs down differently?) is still unanswered. Only Wen Li can say.
4. **How long is "a set period"?** And should a returning responder get a trial run of easy pings first? Engineering to propose.
5. **Does the app tell responders the wait?** Tickets #3043, #3047 and #3065 ask what the ping wait is. Sofia and Nadia to say whether it's shown or announced; likely a quick separate win.
6. **Handler wording.** Sofia to test the card wording with Kip and Aunt Dot before we commit.

## Before this is buildable
Nothing here should be built until these are closed. Owners are proposed.

**Check the premise**
- [ ] Refresh the data past 6-7 Sep. Have the four recovered, got worse, or been changed by 4.3? (Ravi)
- [ ] Confirm production behaviour: current scores for the four, weights, wait, miss penalty, any decay. Our code copy is a stub. (Wen Li or Marcus)
- [ ] Get response times so we can tell timer from score. Vesper's score doesn't explain their drop, so a score fix alone may not bring them back. (Ravi)
- [ ] Get an answer to Marcus's 14 Aug question: was treating everyone the same a decision? (Wen Li)
- [ ] Diagnose Vesper specifically before choosing a fix; the four may not share one cause. Check: (a) whether Vesper's availability record or capability tags changed around 12 Aug, since that filter runs before scoring; (b) Vesper's travel-time position under the 0.60 proximity weight; (c) whether Vesper's answers land just past 60 s. (Ravi, Wen Li)

**Decide the behaviour**
- [ ] Return period: how long before a quiet responder is brought back, and whether returners get a trial run. (Engineering proposes, Helen approves)
- [ ] How much cheaper a miss is than a turn-down, and whether it should cost anything at the floor. (Wen Li, Marcus)
- [ ] What The Gale and the other responders see when load moves back. (Engineering, Ravi)
- [ ] Whether handlers may see "ranked low" at all, since it reveals routing logic. (Helen)
- [ ] What a returning responder sees on their phone, and whether they're told anything. (Sofia)
- [ ] **Decision for Helen: ping wait for returners.** The wait is the same for everyone and this brief leaves it at 60 s. If Vesper's misses are about the wait, a returning Vesper misses again and nothing improves. Options: keep it fixed; give a returner's first few pings the old 90 s; or move the whole wait back. Not decided here. (Helen, with response-time data)

**Design and wording**
- [ ] A mock of the responder card, tested with Kip and Aunt Dot. The wording above is mine, not theirs; Kip said he wasn't sure what he'd want it to say. (Sofia)

**Test and release**
- [ ] Decide whether any fading applies to turn-downs or only to misses. Default: misses only. (Wen Li, Helen)
- [ ] The replay reports every responder's pings per week before and after, so we see who gives pings up as well as who gets them back, including low-volume responders (The Drift, The Longcast, Ironvale) and heavier decliners (Sgt. Bulwark, Captain Vantage). (Ravi)
- [ ] Replay the real pings table through the new rules: the four return, the other twelve aren't starved, and the Vesper test above passes. Pass/fail criteria written first. (Engineering, Ravi)
- [ ] Agree success targets and the guardrail with Marcus and Ravi. Per-responder acceptance reporting in place before release.
- [ ] Rollout and rollback plan: all at once or staged, what we watch, what triggers a rollback. (Marcus)
- [ ] Confirm no change to the Responder Availability Record; tell Supply if that changes.
- [ ] Communication: handler release note, and a decision on whether responders are told about the 4.2 wait and this change. (Nadia, Sofia)

## Next step
Helen to confirm this is the shape she wants. Then work the checklist above, starting with the data refresh and the conversation with Wen Li, and build a clickable mock for the one-pager.
