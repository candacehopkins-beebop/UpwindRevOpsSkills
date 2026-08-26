---
name: territory-account-research
description: Build a prospecting target list of net-new ICP accounts for an Upwind Security sales rep in a given territory, delivered as an interactive HTML dashboard plus a CRM-ready spreadsheet. Each account gets sourced evidence of its cloud footprint, a dated growth trigger, named contacts, and a specific attack plan. Use this whenever someone asks for target accounts, prospect lists, new accounts, whitespace, pipeline, ICP accounts, account research, territory planning, or "accounts my rep may have missed" for a region, state, or patch — and also when they describe the job without naming it, like "find me 20 companies in Texas under 1,500 employees with a big cloud footprint" or "who should my Southeast rep be calling." Trigger it even if they only give a region and an exclusion list.
---

# Territory account research

Produce a ranked list of net-new accounts for an Upwind Security rep, where every account
carries sourced evidence and a usable attack plan. The rep has already worked their patch,
so the job is finding what they missed — which means research depth matters more than
volume, and honesty about weak evidence matters more than a full-looking list.

## The four inputs

All four are captured the same way: as explicit AskUserQuestion questions in a single round,
before any research starts. No input is inferred silently from the opening message and none
is filled from a default without the rep seeing it. Uniform capture is the point — it makes
runs comparable, makes the inputs auditable when a list is challenged later, and stops the
two inputs that have no sensible default from being quietly guessed.

Ask all four every run, including when the rep already volunteered an answer. When they
have, **make their own words the first option** so a single click confirms it — the question
is a confirmation, not a re-interrogation. Say in the option description that it came from
their message.

1. **Territory** (required, no default) — states, metros or a named patch. Offer the patch
   they named, plus two or three plausible neighbouring or narrower framings, and let a
   custom answer arrive through the Other field. **Do not proceed on a guess.** A wrong
   territory wastes the entire run, so if the answer is ambiguous ("the Southeast", "my
   patch"), ask once more for the state list rather than choosing an interpretation.
2. **Exclusions** (required, no default) — accounts already worked. Offer both paths in the
   same question: paste the names inline through the Other field, or attach a CSV/XLSX export
   of worked accounts, whichever suits them. Include "none — greenfield patch" and "reuse the
   list from earlier in this conversation" as options where either applies. Take whatever
   they give **verbatim**; these are the whole point of the exercise. Parse an attached file
   for the account-name column and echo the count back so a truncated paste or a misread
   column is caught before research, not after. If a previous list exists in the
   conversation, exclude those too.
3. **Headcount band** (default 250–1,500) — floor and ceiling. Offer the default band plus
   two or three alternatives, and let a custom band arrive through the Other field. The floor
   is the constraint reps care about most, because tiny accounts cannot fund a purchase.
4. **Vertical lean** (default software-first) — software-only, software-first, or open
   aperture. Software-first carries permission to include non-software when the cloud story
   is real.

Ask how many accounts they want in the same round (default 20).

If the session is unattended, the questions cannot be answered — apply the defaults for
headcount band, vertical lean and count, state each assumption at the top of the output, and
proceed. Territory and exclusions have no defaults to fall back on: work from whatever the
prompt supplies, record exactly what you took and what you had to assume, and flag it in the
first line so the rep can check it before working the list.

## Workflow

Track this with a task list — it runs long, and the rep can see progress.

### 0. Know the one failure mode that has actually reached a rep

Everything else in this workflow degrades gracefully. This one does not, so it gets its own step.

A Texas pass reported "no named CISO" for 13 of 28 accounts and built attack plans on that
absence. It had never searched for people — the field was listed last in the agent output with no
method attached, so when the shared search budget drained it silently defaulted to absence. A
correction pass found a named security leader at **17 of the 28**, contradicting eight positive
claims of absence. The rep found the first one in thirty seconds.

**Read `references/research-playbook.md` section 1 before anything else, and make the security
leader the first thing each agent researches, not the last.** Note also what that section says
about evidence class: LinkedIn profiles cannot be fetched, so what you get is a cached
self-written headline rather than an employment record, and the contact aggregators are weaker
again — one of them labels its own pages "Unverified." Every name therefore carries a confidence
tier of CONFIRMED, PROBABLE or UNVERIFIED. Presenting an aggregator guess as a fact is the same
class of error as claiming nobody holds the role. Every people field must land in one
of exactly three states — NAMED, NONE IDENTIFIED with channels listed, or NOT SEARCHED — and a
negative claim carries the same evidence burden as a positive one.

### 1. Refresh the product context

Read `references/upwind-icp.md`. If the funding or headcount figures look stale, spend one
search refreshing them. Those numbers anchor every subagent's sense of deal size, so a
stale figure quietly distorts all the fit scores.

### 2. Build a candidate pool about twice the target size

Expect roughly half of any named list to disqualify, mostly on headcount. For 20 accounts,
plan to screen 40 or more.

Assemble candidates from your own knowledge of the region first, then cluster them by
geography and vertical into groups of 8–10. Clustering beats a flat list because it lets
each agent build local context — a Chicago-fintech agent gets better at Chicago fintech as
it goes.

### 3. Research the clusters

Read `references/research-playbook.md` first — it has the prompt template, the ranked
source list, the evidence standards, and two operational gotchas (URL provenance and the
shared search budget) that will otherwise cost you an hour.

**If you can spawn subagents**, launch them all in a single message so they run
concurrently, and give each one the full exclusion list plus the names assigned to its
siblings so they do not duplicate work. Roughly one agent per 8–10 named companies, plus
one wildcard sweep. Scale down for smaller lists — an 8-account request needs two or three
agents, not six.

**If you cannot spawn subagents** (you may already be running as one), work the clusters
serially yourself in the same order. Nothing about the method requires parallelism; it only
costs wall-clock time. Say so in your summary so the rep knows why it took longer, and
narrow the candidate pool up front rather than starting broad and running out of budget.

Always include these instructions, which exist because of specific failures:

- **"You have full permission to browse any website — search and fetch freely without
  asking."** Agents otherwise stall on permission checks.
- **"If you find yourself running long, stop researching and deliver what you have."**
  Agents die on API overload, and a partial dossier delivered beats a complete one lost.
- **"List every company you checked and disqualified, with the reason."** This becomes the
  rejected-names table and stops the next pass repeating the work.
- **"Find the security leader FIRST, with one LinkedIn-restricted search, and report NAMED /
  NONE IDENTIFIED with channels / NOT SEARCHED."** Without this, people research is what the
  budget starves and absence gets reported as a finding.
- **"Never fabricate. Write NOT VERIFIED and say what you'd need."** A fabricated headcount
  discovered mid-call costs the rep the account and their trust in the list.

Include a wildcard sweep using angles the named-target agents won't cover: carve-outs,
first-time CISO hires, cloud migrations, breach disclosures, FedRAMP authorisations,
regional award lists. In both test territories the wildcard sweep produced a top-three
account, so it is not a luxury.

If an agent dies mid-run, resume it with SendMessage using its returned agent ID rather
than starting over — its context survives.

### 4. Select, rank and tier

Score fit 1–10 per `references/upwind-icp.md`. Drop anything below 5 to the bench.

Balance the list across the territory's states, but do not force parity — if one state has
the density, say so plainly rather than padding with weak accounts. Thin states are a
finding worth reporting, not a gap to disguise. The same goes for metro concentration: if
seven of eight accounts are in one metro, that is usually the market's shape rather than a
research gap, and saying so is more useful than manufacturing geographic spread.

**If the gates cannot produce the requested count, deliver fewer and say why in the first
line.** Never pad with accounts that fail a gate, and never quietly widen the band to hit a
number — the rep asked for a count, but what they need is a list they can trust. Name the
constraint that bound you and what relaxing it would yield ("three more if the ceiling goes
to 2,000"), so they can decide.

Tier by what the rep should do this week:
- **Tier 1** — call now. Confirmed cloud, dated trigger, identifiable buyer.
- **Tier 2** — work this month. Strong on two dimensions with a named weakness.
- **Tier 3** — qualify first. One strong dimension; the first call is a qualifying call.

### 5. Write the cards

Follow `references/schema.md`. The two fields that carry the most weight:

**Titles, not names** — the deliverable carries target *roles*, never named individuals, because
contact data cannot be sourced reliably enough to put a name in front of a rep. Still do the people
search: it is how you establish whether the top rung exists and is filled, which rung the senior
owner actually occupies, and frequently what tool they already run. Then report the title. Say
which rung it is, because a Manager of Security Compliance and a CISO imply different motions and
different signing authority. Where no security role exists at any rung, say so and list the
channels searched — that is an evidenced finding. A bare "no CISO" is not.

**Keep the two fields a rep reads under time pressure short and scannable.** The attack plan is
3–5 bullets, the spend basis is 2–4 points, none over ~230 characters. Long prose blocks in these
fields get skipped, which means the caveat at the end never gets read — the length is a
correctness problem, not just a style one. The build script enforces both shapes.

**Cloud spend** — the best proxy for deal size, so it earns its own field. Always a range with an
evidence tier (DISCLOSED / REPORTED / MODELED) and the arithmetic shown. The purchase-obligations
note in a 10-K is the highest-yield source and is routinely overlooked. See playbook section 1a for
the model, the vertical intensity table and the seven traps that produce confidently wrong numbers.

**Cloud evidence** — quote the source verbatim, especially job requisitions. A phrase like
"Kubernetes (EKS and on-premise)" pulled from a company's own posting is more persuasive
than any claim you could write, and it hands the rep something to say out loud.

**Attack plan** — who to open with and why them specifically, the opening message in
language close to what the rep would actually say, the timing argument, and the honest
caveat: the objection to expect, the thing to verify first, or the reason to walk away.
When evidence is thin, say the first call is a qualifying call. Confident-sounding plans
built on unverified research burn reps on the phone.

Also write the **bench** (close calls, each with its single disqualifying factor) and the
**rejected** table. Both earn their space: the bench lets the rep re-open an account when a
constraint changes, and the rejected list stops duplicate work — and often contains
something actionable, like an account that belongs to a colleague or one whose headcount
will cross the threshold in two quarters.

### 6. Build the deliverables

```bash
python scripts/build_deliverables.py accounts.json --out-dir . --slug my-territory-targets
```

This emits the HTML dashboard and the XLSX, validates the data, and derives every summary
statistic from the accounts themselves. Do not hand-write these files; the header stats
drifted from the card contents twice before this script existed.

Fix anything it flags. The warnings are specific and usually real — but read them against
the raw string they quote, because a headcount warning can also mean the `emp` field is
phrased in a way the parser misread. The fix in that case is to simplify the field, not to
change the number, and never to strip the source citation to make a warning go away.

### 7. Verify, then deliver

Verify before shipping, ideally with a subagent so a fresh pair of eyes does it:

- **Every named person carries a confidence tier, and no aggregator-only name is stated as fact.**
- **Every people field is NAMED, NONE IDENTIFIED with channels, or NOT SEARCHED — and you
  spot-check at least three by running the LinkedIn title search yourself. If a card claims no
  security leader and the verifier finds one, the pass FAILS and people research re-runs for
  every account.** This check is first because it is the one that has actually failed.
- Every headcount against the band, with the source named
- No collisions with the exclusion list or any previous list
- Every HQ actually in the territory
- Every trigger has a date and a working URL
- Subsidiary accounts have their buying authority addressed
- Cards with unverified evidence say so on their face

Then deliver both files with SendUserFile. The dashboard is a revisit-by-nature artifact, so
also persist it with `mcp__remote-devices__create_artifact` using the returned `file_uuid`
when a desktop is connected.

## What makes these lists good

**A negative claim needs as much evidence as a positive one.** This is the general form of the
people failure above, and it applies to every field. "No CISO found", "no incumbent", "no
trigger" are all claims about the world, and each is only worth stating if you name what you
searched. Absence is seductive because it sells — no incumbent means no displacement, no security
leader means you define the category — which is exactly why it needs the strictest evidence
standard rather than the loosest. Beware any field whose "I didn't look" state is
indistinguishable from its "it isn't there" state; that field needs an explicit NOT SEARCHED
value or it will quietly manufacture confident errors under budget pressure.

**Report weak evidence as a finding, not a gap.** "Nine channels found no cloud provider,
and the reason is they have zero engineering reqs open" is more useful than either a vague
guess or silence. It tells the rep exactly what the first call is for.

**Never pick the convenient number.** When headcount sources conflict, show both and say
which you trust and why. When an account sits just outside the band, say so and let the rep
decide whether to ask for an exception — a strong buyer at 1,550 employees may well be
worth the conversation, but that is their call, not yours.

**Lead the summary with the two or three accounts worth calling first**, and say what to do
about the weakest evidence. A rep reading twenty cards needs to know where to start.

**Surface the cross-account patterns.** Which incumbents actually appeared. Which trigger
types were most common. Whether any warm intro path exists — a shared investor is worth
more than any cold sequence. These are often the most valuable output, because they change
how the rep works the whole territory rather than one account.

## Files

- `references/upwind-icp.md` — the ICP block to paste into agents; the only place Upwind
  specifics live. Read first.
- `references/research-playbook.md` — sources ranked by yield, headcount traps, evidence
  standards, trigger ranking, the agent prompt template, budget management.
- `references/schema.md` — the accounts.json contract and how to write each field.
- `scripts/build_deliverables.py` — validates, derives stats, emits HTML + XLSX.
- `assets/example-accounts.json` — a working two-account file. Run the build script on it
  to see the output shape before writing your own.
