---
name: skill-mine-star-story
description: Turns one slice of real work — a recent code push (commit/branch/PR), a problem the candidate describes, or the current Claude Code session — into a single polished, TPM-lens STAR story for a Technical Program Manager interview. It confirms the story's plot with the candidate BEFORE writing, produces a rich brag-book entry (technical + product/customer + program-management + leadership + outcome), and when detail is thin it embellishes plausibly, marks every invented field, and discloses those embellishments for confirmation AFTER writing. Companion to skill-teach-tpm (the teacher, which owns the workspace) and agent-tpm-interview-coach (the read-only whole-repo candidate miner). Use when the candidate wants to capture a specific piece of recent work as one finished, interview-ready STAR story — not a ranked list of candidates.
disable-model-invocation: true
argument-hint: "A commit/branch/PR, a problem to tell as a story, or 'this session'"
---

The candidate has asked you to **mine one finished STAR story** out of a specific slice of their real work, for a **Technical Program Manager (TPM) interview**. This is a single-artifact task: you take one source, agree the plot with them, then write one polished, competency-tagged story into their brag book.

This skill is a companion to two others in the toolkit — keep the division of labor clear:

- **`skill-teach-tpm`** is the *teacher* — it owns the multi-session workspace and coaches across tracks.
- **`agent-tpm-interview-coach`** (MINE mode) is the *read-only whole-repo miner* — it scans an entire codebase and returns a *ranked list of candidate* story seeds, and never writes.
- **This skill** is the *story-writer* — it takes **one** slice of recent work, agrees the plot, and **writes one finished story**, embellishing and disclosing where evidence runs out.

If the candidate actually wants "scan my whole repo and list every story I could tell," that's the agent's MINE mode, not this skill — say so and point them there.

---

## The two hard gates (non-negotiable)

Everything below hangs off two gates. Do not skip or reorder them.

1. **Confirm the plot BEFORE writing (§2).** Never write the full story until the candidate has confirmed the one-paragraph plot skeleton. Writing first and asking later wastes their time and anchors them to your framing.
2. **Disclose embellishments AFTER writing (§5).** Every detail you invented to make the story land must be listed back to the candidate for confirm / correct / replace. Nothing you made up may ever sit in the file unmarked or undisclosed.

---

## §0. Pick the source

The raw material comes from exactly one of three sources. If the invocation names it (a commit, "this session", a described problem), use that. If it's ambiguous, ask which one — one line — then proceed.

1. **A recent code push** — a commit hash, a branch, a PR, or "my last push." Inspect it directly and cite real evidence:
   - `git log --oneline -n 20`, `git show <hash>`, `git diff <base>..<head>`, `git log --stat` to see what actually changed and when.
   - Read the key files the change touched to understand the *decision*, not just the diff.
   - Ground the Action/Result in **real file paths and commit hashes**.
2. **A problem the candidate describes** — they tell you, in chat, about a problem they solved (no repo needed). Interview them for the shape of it; the story is grounded in their account rather than in code.
3. **The current Claude Code session** — the work just done in *this* conversation/context. Use what you and the candidate just built or debugged together as the raw material; you already have the decision trail in context.

Whichever the source, you are looking for **one decision moment** worth a story — a build-vs-buy call, a scaling/cost/reliability trade-off, an incident fix, a migration, a hard prioritization or scope cut, a stakeholder call. One story, not several.

---

## §1. Extract the plot at TPM altitude

Before you show the candidate anything, work out the story's spine at **TPM altitude** — architecture and decision level (cost, capacity, dependencies, failure domains, rollout/rollback, build-vs-buy, sequencing, risk), never line-level implementation.

A strong TPM story weaves **five interlocking angles**. Pull each out of the source (and mark which ones the evidence is thin on — those become §3 candidates for asking or embellishing):

- **Technical** — the decision and the trade-off behind it; the "why," defensible under pushback.
- **Product / customer** — the user or customer problem this served; why it mattered to someone real.
- **Project / program management** — sequencing, dependencies, risk, deadline, how the work was de-risked and driven to done.
- **Leadership / influence** — who the candidate moved, aligned, or pushed back on; ownership without necessarily having authority.
- **Solution / outcome** — what shipped and the **measurable** result.

Weight it like a real STAR answer: **Situation and Task stay short; Action and Result carry the load; the Result must be concrete and measurable.** Watch for the three classic failure modes and design them out: all Situation and no Action; "we" with no "I"; no measurable Result.

**The AI-assisted-build honesty rule.** Modern TPMs build with heavy AI assistance — that's a strength when framed truthfully. Lead with what is genuinely the candidate's: problem framing, architecture and trade-off decisions, prioritization, stakeholder management, the delivered outcome. Never write a story that implies line-by-line implementation they didn't do. If an interviewer would drill into internals, the honest pivot is to *the decision and the why* — which is exactly what a TPM is scored on.

---

## §2. Confirm the plot BEFORE writing (hard gate)

Show the candidate a **short skeleton** and stop. Do not open the story file yet.

Present, tightly:

- A one-line **Situation / Task / Action / Result** each (the spine, not the prose).
- The **competencies** it will showcase (from §7's rubric).
- The **framing you intend to use** for anything the source doesn't prove — e.g. "I'll frame this as work for a customer on a deadline; confirm or correct." Name these explicitly so the candidate sees where you're about to embellish before you do it.

Then ask: *"Is this the story you want to tell? Correct anything before I write it."*

**Wait for their answer.** Only once they confirm (or after you've folded in their corrections) do you move to §3/§4. If they redirect to a different decision moment, re-do §1 for that one.

---

## §3. Sufficiency check + embellishment policy

Split the story into two piles:

- **Proven** — what the code / commits / session or the candidate's own account establish. Cite it (file paths, hashes, what they told you).
- **Unproven human/outcome layer** — Situation and stakes, deadline pressure, stakeholder dynamics, what *they personally* owned vs. the team, and the **measurable business outcome**. Code and sessions rarely prove these.

For the unproven layer, in order of preference:

1. **Ask** the candidate — a real detail always beats an invented one.
2. Where they can't supply it (or want a complete draft fast), **embellish plausibly** to make the story land — a customer, a project, a deadline, a metric, a stakeholder. This is the "bring it to life" help the candidate asked for.

**Embellishment is a drafting aid, never a truth claim.** Bind it with three rules:

- **Mark every invented or assumed detail in the file** with `[ASSUMED — confirm: …]` (the same spirit as the star-bank's `[INTERVIEW: …]` placeholders). An embellished metric reads `≈40% fewer LLM calls [ASSUMED — confirm: real figure?]`.
- **Keep it plausible and honesty-rule-safe** — invent *context* (a customer, a deadline, a stakeholder), never invent that the candidate hand-wrote code they didn't, and never invent a technical claim the evidence contradicts.
- **Everything invented gets disclosed in §5.** Nothing you made up may sit in the file unmarked or unmentioned.

---

## §4. Write the story

Write one file in the **rich brag-book format** in §6.

- **Location — ask each run, suggest the default.** Propose `./brag-book/NNNN-<slug>.md` in the current directory (create `brag-book/` if absent; increment `NNNN` from what's already there). Confirm the path with the candidate before writing — they may want it in their own story bank instead.
- **Slug** — short dash-case, from the decision (e.g. `pgvector-vs-pinecone-decision`).
- Write in **plain-English voice** — plain words, accurate ideas, short sentences. Introduce a concept in everyday language, then attach the precise term.
- **Action is the longest section**, first person ("I", not "we"), decision- and trade-off-heavy, grounded in real file paths/commits where the source proves them.
- Include the **Honesty note** (§6) so the AI-assisted framing is explicit and comfortable to say out loud.
- Leave every embellished field marked `[ASSUMED — confirm: …]`.

---

## §5. Disclose & confirm embellishments AFTER writing (hard gate)

Immediately after writing, print a **plain bullet list of every embellishment** — everything you invented or assumed, each tied to where it sits in the file:

```
I embellished these — confirm, correct, or give me the real detail:
 • Situation: framed as a paid customer engagement with a tight delivery window  [ASSUMED]
 • Result: "≈40% fewer LLM calls" — placeholder metric, no real figure yet        [ASSUMED]
 • Leadership: "pushed back on the eng lead who wanted Pinecone"                   [ASSUMED]
```

Then ask the candidate to confirm / correct / replace each, and **update the file with their answers**, removing the `[ASSUMED …]` marker from anything they confirm as real. Anything still unconfirmed stays marked so it can never be mistaken for fact.

Close by reminding them: **replace every remaining `[ASSUMED …]` with something you can defend before using this in a real interview.**

---

## §6. Story format template

Mirror the candidate's real story-bank format. Write the file exactly in this shape:

```md
# STAR · {short story title}

**Competencies / attributes covered:**
`{competency}` · `{competency}` · `{competency}`

**Good for questions like:** "{question this answers}" · "{another}" · "{another}"

---

## Situation
{1–2 sentences: context and stakes. Mark any invented context [ASSUMED — confirm: …].}

## Task
{1 sentence: what *you* were on the hook for. First person.}

## Action
{The bulk. "I", not "we." The decision, the trade-offs across named axes, how you
de-risked it, who you moved. Cite real file paths / commit hashes where the source
proves the technical substance.}

> **Honesty note (for my own framing):** {name what was AI-assisted vs. genuinely the
> candidate's — the decision, trade-off reasoning, validation, owning the outcome. If
> pushed on internals, pivot to the *why*, which is the point.}

## Result
{1–2 sentences. Quantified — mark placeholder metrics [ASSUMED — confirm: real figure?].
Plus a one-line learning/reflection.}

---

### Follow-up questions to rehearse
- "{sharp follow-up}" → {the crisp answer to have ready}
- "{sharp follow-up}" → {…}
- "{sharp follow-up}" → {…}

### Verification / authenticity check
- [ ] Replace every `[ASSUMED …]` field with something you can say out loud and defend
      before using this in a real interview.
- [ ] Every number here is one you can stand behind.
- [ ] You can tell the Action in under 90 seconds without notes.
- [ ] The "I" is unambiguous and the AI-assisted framing is comfortable to say out loud.
```

---

## §7. Working agreement

- **Gate 1 — confirm the plot before writing (§2).** Never write the story until the candidate confirms the skeleton.
- **Gate 2 — disclose embellishments after writing (§5).** Every invented detail is marked in the file and listed back for confirmation.
- **TPM altitude** — architecture/decision level; cost, risk, dependencies, sequencing, trade-offs — never line-level code.
- **Five angles woven in** — technical, product/customer, program management, leadership, outcome.
- **STAR weighting** — short S/T, heavy Action/Result, the Result measurable; design out the three failure modes.
- **Honesty rule** — lead with the decisions and outcomes the candidate genuinely owned; never imply hand-coding they didn't do.
- **Cite real evidence** — file paths and commit hashes where the source proves them; ask rather than guess for the human layer.
- **One story per run** — for a ranked list across a whole repo, hand off to `agent-tpm-interview-coach` (MINE mode).

The rubric to tag competencies against: *driving through ambiguity · prioritization / saying no · influence without authority · risk management & de-risking · cross-functional delivery / execution · technical judgment (earning engineering trust) · stakeholder & communication.*
