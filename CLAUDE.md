# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Sources: rook-wiki (About Rook, Glossary, Team directory, Releases, Q3 roadmap,
Product briefs, 4.2 release comments) and `00-rook/company/notes/handoff-from-priya.docx`.
Wiki state as of the Team directory update (2 Sep 2026). I have not yet read the
Customer interviews database or rook-database.

### Me and the job
I'm the new PM for **Rook Dispatch** (started Mon 24 Aug 2026), replacing Priya
Raghunathan, who left 21 Aug after 14 months as sole Dispatch PM. I report to
Helen Achebe (Director of Product).

### Company and products
Rook Industries (fictional, ~241 staff, HQ Site Aleph) sells coordination and
provisioning software to independent masked responders and their handlers.
Subscription, priced per active responder. Monthly release train; point releases are 4.x.
- **Rook Dispatch** (mine): availability, proximity, who gets pinged about a callout,
  whether they take it. Used by handlers (console, desktop-only) and responders (phone).
- **Rook Supply**: requisitions, maintenance, failure reports. Used by handlers and quartermasters.
- **Hard rule:** Rook never stores or can reconstruct a responder's legal identity from
  their cover identity (Security Policy 4.1). Never design for it. Never try to work out who anyone is.

### People (wiki comments use roles, not names)
| Role in comments | Person | Notes |
| --- | --- | --- |
| Engineering manager | Marcus Oyelaran, Site Aleph | Runs Dispatch engineering. Straight talker. Priya's "start here". |
| Staff engineer | Wen Li, Berlin | Built the ping-ranking logic. No written doc; learn it by talking to her. DM her directly. |
| Support lead | Nadia Hoffmann, Berlin | Owns tickets; has the ticket-theme breakdown. Priya recommended a standing 15 min. |
| Product designer | Sofia Marino, Site Aleph | Console and phone app. Ran the September customer interviews. |
| Data analyst | Ravi Menon, Singapore | Owns the weekly responder-acceptance numbers. |
| Director of Product | Helen Achebe, Site Aleph | My director. Owns roadmap and commitments. |
| Priya | Priya Raghunathan | Former Dispatch PM, gone. Her handoff says Marcus's number is the emergency contact. |

### Vocabulary
- **Callout**: request for a responder to attend an incident; Dispatch's unit of work.
- **Ping**: one callout offered to one responder's phone. Outcomes: **taken**, **turned down**,
  **missed** (ping wait expired). Turned down and missed both pass the ping to the next responder, but are recorded separately.
- **Ping wait**: how long a ping stays live before counting as missed. One value for everyone, set per release.
- **Acceptance rate**: share of pings taken. Dispatch's headline metric. **Time-to-accept**: median seconds ping to taken.
- **Coverage gap**: no available responder had the needed capability tags (nobody *could* go), distinct from low acceptance (nobody *would*).
- **Routing priority**: score ranking responders for a callout. Inputs: proximity (travel-time estimate),
  availability, capability match, recent acceptance history. Turning down or missing pings lowers the
  recent-acceptance part, which lowers future ranking.
- **Capability tag**, **Responder Availability Record** (written by Dispatch, read by Supply),
  **Handler**, **Quartermaster**, **Requisition**, **Mutual aid** (unsupported; Q4 exploration).

### Where things stand
**Releases:** 4.0 (7 Apr: console nav, profile redesign, routing-override audit log), 4.1 (16 Jun: travel-time
proximity, bulk callout, push reliability), 4.2 (12 Aug), 4.3 next (Supply requisition approval chains).

**4.2 shipped three things at once:** (1) proximity weighted up relative to recent acceptance;
(2) ping wait cut 90 to 60 s; (3) filter persistence plus three bug fixes. Release went clean technically.

**The open problem, 4.2 fallout.** Since release, callout tickets are ~3x normal (flat, not improving as of 26 Aug).
Split about two-thirds "my phone never goes off" and one-third "gone before I could answer."
- The one-third is explained by the 60 s ping wait.
- The two-thirds is **unexplained**. Unproven hypothesis: the new weighting treats responders with poor
  acceptance history differently, but the config doesn't distinguish them. Marcus asked on 14 Aug whether that was
  a decision or "fell out that way"; Wen Li never answered (away 14-24 Aug, then buried).
- Priya's view (handoff, 19 Aug comment): mostly seasonal, August is always soft, wait for September, don't revert.
  **Nobody has checked this against data.** Treat it as a claim, not a finding. Ravi's weekly numbers are the real test.
  Note Priya said Marcus can pull numbers, but Marcus said his would be rough; Ravi is the owner.
- Marcus agreed (28 Aug) to regroup on the 4.2 picture once I'd had a week. That conversation is due and I have not seen its outcome.
- Don't frame this as "revert 4.2" by default (the change was a long-standing responder ask), but don't rule it out either.

**Roadmap (Q3, last reviewed 30 Jun, stale; all items still list Priya as owner, which needs reassigning):**
| Item | Target | Status | Reality |
| --- | --- | --- | --- |
| Change to who gets pinged | 4.2 | Committed | Shipped |
| Ping timeout tuning | 4.2 | Committed | Shipped as a flat cut to 60 s, not tuning |
| Availability Confidence | 4.2 | Committed | **Not in 4.2 notes; apparently deferred.** Priya says a couple of items were squeezed out. Ask Helen which are still Q3 commitments. |
| Requisition approval chains | 4.3 | Committed | Supply; brief scope-creeped (see below) |
| Handler phone app | Q4 | Exploring | Sofia exploring, unstaffed |
| Shared cover between responders | Q4 | Exploring | |

**Briefs (wiki "Product briefs"):**
- *Routing Override Audit Log* (5 Mar): small, build-ready, eng + Sofia mock exist; already in 4.0 release notes.
- *Bulk Callout* (12 Jan): shipped in 4.1 per Releases, yet the brief still lists it unowned, with no baseline for time-to-full-coverage.
- *Requisition Approval Chains* (14 Jul): real ask is one extra approval over $2,000, buried under four add-ons. Needs scoping down.
- *Handler Phone App* (8 Sep): exploration only; scope is notifications, status view, one-tap contact.

### Open to-dos
1. Get weekly acceptance data from Ravi, split by responder history and by date, before concluding anything about 4.2.
2. Sit with Wen Li to understand ranking, then **write the missing description of how we decide who gets pinged** (Priya's explicit ask).
3. Confirm with Helen which 4.2 deferrals (e.g. Availability Confidence) are still Q3 commitments; refresh the roadmap and owners.
4. Standing 15 min with Nadia; get her ticket-theme breakdown.
5. Read the Customer interviews and rook-database before relying on any numbers.
6. Low priority per Priya: filter-persistence tickets are noise.

### Conventions
Wiki comments name roles, not people: map via the table above. Treat handover claims
and old roadmap status as unverified until checked against data.

### Learned in session 1 (supersedes the above where they conflict)
- **4.2 data check (rook-database, pings/callouts/tickets, 29 Jun to 6/7 Sep):** acceptance fell from ~77% to 54%
  in the week of 12 Aug, then 66, 67, 73. Misses went from 2-6/week to 38, 28, 24, 21. Tickets went from 5-8/week
  to 20-32. Callouts nobody took doubled (5.5% to 11.1%). Callout volume dipped only ~10%, so Priya's
  "seasonal" explanation is at most a small part.
- **Four of 16 responders collapsed after 12 Aug** (Farlight, Meteor Mite, The Undertow, Vesper): 70-86 pings before,
  11-17 after, down to ~1/week by late August, no recovery. Others absorbed the work. Meteor Mite and The Gale share
  Eastgate and went opposite ways, so geography does not explain it. Acceptance "recovering" is partly an
  artifact: the missers stopped being asked.
- **Likely mechanism (still a hypothesis):** in `00-rook/code/dispatch-routing`, a missed ping is penalised like a
  turned-down one (`history.py`, penalty 0.12 vs credit 0.08), scores never decay (2019 TODO from Wen Li), and 4.2
  also cut the ping wait 90 to 60 s and moved weights (acceptance 0.40 to 0.25, proximity 0.45 to 0.60). The code is a
  stub (in-memory scores), so confirm against production. Weights and wait shipped together, so the data cannot
  separate them. No response-time data to show why these four.
- Helen's `05-super-speed/director-request.txt` wants a user-facing one-pager (ideally clickable) before any code
  change, framed around what a handler like Kip would notice. Undated and secondhand; engineering's diagnosis is not
  written in the wiki.
- Acceptance rate is reported weekly in aggregate, which hides this split. `availability.py` record shape is a
  contract with Supply; tell Supply before changing it.
- Briefs are stale: Bulk Callout (shipped 4.1) and Audit Log (shipped 4.0) read as unbuilt. The requisition brief's fix
  (extra approval) conflicts with Halloran's real complaint (queue too slow, priority field ignored).
- Open: Marcus's 14 Aug question (should the new weighting treat low-acceptance responders differently?) is
  unanswered. Nothing known after 7 Sep. Not yet looked at: the 49 untaken post-4.2 callouts.

### Learned in session 2 (interviews vs tickets)
- **Interviews** (wiki Customer interviews, 2-5 Sep, by the designer, console-redesign framing): Aunt Dot (Vesper), Ambrose
  (Captain Vantage), Halloran (Sgt. Bulwark), Kip (Meteor Mite + The Gale). The 4.2 problem shows up in all four but only
  when prompted; handlers see effects, not cause. Console asks (dark mode, alert sounds, badge size) are about 2 tickets
  each. Ambrose's timeline conflicts: ticket 3043 says 12 Aug, interview says about 19 Aug.
- **Per-responder weekly pings** are in `00-rook/feedback/responder-weekly-pings-for-ravi-conversation.md` (my own query,
  data ends 31 Aug). Misses rose for all 16 responders after 4.2, which fits the 60 s wait. Only four dropped out of
  rotation. `routing.py` only reorders, so the penalty alone doesn't explain about 1 ping a week. Sgt. Bulwark is not a
  control: his misses rose too.
- **Bias notes:** the seven ticket groups are my own reading, formed after I had a view of 4.2. The pings table is the only
  source with no selection step. Priya, Wen Li and Marcus each have a stake in the 4.2 story, so ask for production scores,
  not opinions.
- **Drafts not yet sent:** messages to Wen Li and Marcus in `00-rook/feedback/drafts-wen-li-and-marcus.md`, asking for
  current recent-acceptance scores, whether a miss is penalised like a turn-down, and any decay. Also ask Ravi for response
  times and weeks from 7 Sep. Revised analysis: `customer-interview-analysis-revised.md`.

### Learned in session 3 (Vesper case study)
- **Vesper, week by week (pings/taken):** 14/11, 13/10, 15/13, 14/11, 13/11, 14/12 before 4.2, then 12/6 (week of 10 Aug),
  5/1, 2/0, 1/0. About 8 in 10 taken before; 4 misses in the 4.2 week; almost no pings after. The other three quiet
  responders look the same.
- **Why there's no way back in the code:** a score only changes when a ping is answered, nothing decays, a miss costs 0.12
  and a take earns 0.08. A quiet responder is only pinged as a fallback, and a fallback miss digs them deeper. At 4.2
  weights, 0.8 of acceptance gap is worth about 15 minutes of travel time. Code is a stub; production unconfirmed.
- **No response-time data exists:** `pings` has only callout, responder, sent_at, outcome. Gap to the next ping gives only
  the ping wait on a miss (91 s before, 63 s after) and about 22 to 24 s to turn down. Vesper took 70 of 86 pings and missed
  3 at the 90 s wait before 4.2, so we can't tell whether the 60 s cut alone explains it. Still the question for Ravi.

### Learned in session 4 (tickets vs pings, "August is quiet")
- **Tickets and pings agree on timing, not on shape.** Misses jumped on 12 Aug (7 that day, 12 on 13 Aug); tickets lagged about two days (first clear rise 14 Aug). Pings partly recover (misses 38 to 21 a week) but tickets stay about 3x baseline (25 in the week of 31 Aug).
- **Tickets by `about_responder`:** The Undertow (21) and Farlight (19) lead and keep rising as their pings fall to 1-2. Halfmoon and Corporal Ashgrove are up about 5x without losing pings. Meteor Mite, Vesper, Sgt. Bulwark and The Gale have zero tickets at all, so the collapsed four do not all show up in tickets. Eight tickets say a responder is "much quieter than usual" (from 22 Aug).
- **"August is quiet" check:** distinct callouts dipped 10-20% (110 in the week of 10 Aug, back to 127), so a small seasonal dip is real. It does not explain misses up about 6x from release day, pings per callout 1.24 to 1.3-1.6, or tickets up 3-4x. No prior year in the data; Ravi has the history. `callouts` has no outcome column, so "untaken" means no `taken` ping.
- **Missed-ping share:** 2.3% before 12 Aug; 29.4% on 12-16 Aug; 15.1% from 17 Aug; 18.0% across all of 12 Aug onward (110 of 611), which matches the "18%" figure. Peak day 13 Aug was 48%.
- **Session 5, who was hit:** all 16 responders missed more after 12 Aug (about 2% to 10-18% of pings), but The Undertow, Farlight, Meteor Mite and Vesper collapsed (missed 53-64%, pings per day down about 69%, not 80%; the other 12 were pinged about 20% more). Time of day and place in the ping order do not explain it. From 24 Aug those four got 9 pings in total: none taken, 7 missed, 2 turned down. Whole-dataset missed share is 8.0% (135 of 1,696).
- **Session 5, data quality:** `pings` is clean (no nulls or blanks, no gaps in callout numbers 40101-41419, 1,319 callouts, ends 6 Sep; tickets end 7 Sep). 97 callouts were never taken: 48 of 879 before 12 Aug (5.5%), 49 of 440 after (11.1%); the 49 are still unexamined. Callouts per day 20 before, 15.7 in the week of 10 Aug, 18.1 by 31 Aug.
- **Session 5, ticket bodies read (107 from 12 Aug):** 45 are about pings: 30 "quiet or phone never goes off", 13 "gone before I could answer", 2 both. That confirms the two-thirds / one-third split. Expired-ping tickets bunch in the first week; quiet tickets start in the week of 17 Aug. Several match ping rows exactly (Farlight last pinged 23 Aug, then 28 Aug, missed). Handlers do not know the ping wait (#3043, #3047, #3065 ask). Ticket #3043 was filed 13 Aug, not 12.
- **Session 5 chart file:** `00-rook/feedback/ping-analysis-charts.html` has five charts and a per-responder table. Open it in a browser.
- **Session 6, how the code works (`dispatch-routing`, a simplified copy):** find free responders, score them (travel 0.60, yes-rate 0.25, skills 0.15), sort, offer one at a time with a 60 s wait, update the score, stop at the first yes. A yes (+0.08, `record_accepted`) is the only thing that adds points; no decay, reset or manual fix exists, and at zero a further miss costs nothing more. At 4.2 weights a responder at the floor is about 9 min of travel time behind a neutral one (about 20 min at the old weights), so the score slows the climb back more than it locks anyone out.
- **Session 6, the four quiet responders run through the code's scoring:** Farlight, Meteor Mite and The Undertow fall to about 0.5 or lower by 17-19 Aug and near zero by early September. Vesper is still about 0.8 on 17 Aug although pings had already fallen from 12 to 5 that week, so the score alone doesn't explain Vesper. After their last yes (14-19 Aug) the four got about 20 more pings and none were taken. Timer vs score still can't be separated without response times.
- **Session 6, Marcus's 14 Aug question (did it apply to people already turning jobs down?):** the code applies one set of weights to everyone, with no history or "new responder" rule. Data: heavy past decliners weren't hit (Sgt. Bulwark turned down 25% before and was pinged 1.16x as often after; Captain Vantage 24%, 1.31x); the four who collapsed took about 75-80% before. Whether it was a decision is written nowhere; only Wen Li can say.
- **Session 6, nothing written down:** no wiki or code reason for the 90 to 60 s cut or the 0.60/0.25/0.15 weights. Release notes go to handlers and I found no responder notice; tickets #3043, #3047 and #3065 ask what the wait is. The `dispatch-routing` folder has one git commit (2 Oct, "Initial commit"), so the changelog is its only history. Wen Li's wiki page is empty.
- **Session 6, still to ask:** Wen Li or Marcus for production scores for the four, current weights/timer/penalty, any decay or reset, why 60 s, and whether a miss should cost the same as a turn-down. Ravi for response times. Sofia whether the app shows the wait. Nadia whether responders were told.
