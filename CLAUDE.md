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
