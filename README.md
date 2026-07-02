# 🎯 TPM Skills & Agents

> A portable toolkit of [Claude Code](https://claude.com/claude-code) **skills** and **agents** that turns Claude into your personal **Technical Program Manager (TPM) interview coach** — grounded in your *real* shipped work, not generic theory.

---

## 🤔 What is this, in one breath?

Three tools that work as a team:

- 🧑‍🏫 **`skill-teach-tpm`** — the **teacher**. A patient, multi-session coach that builds you a personalized study course (system design, technical/domain knowledge, and behavioral STAR stories) and remembers where you left off.
- 🕵️ **`agent-tpm-interview-coach`** — the **analyst**. A read-only specialist the teacher (or you) calls on to do two heavy-lifting jobs: **mine your whole codebase for a ranked list of interview stories**, and **grade your practice answers** like a tough interviewer.
- ✍️ **`skill-mine-star-story`** — the **story-writer**. Takes **one** slice of recent work — a code push, a problem you describe, or the current Claude Code session — confirms the plot with you, then **writes one finished STAR story**, embellishing the thin parts and disclosing exactly what it made up.

```
        YOU (the candidate)
              │
              ▼
   ┌───────────────────────┐        delegates to        ┌──────────────────────────┐
   │   🧑‍🏫 skill-teach-tpm   │ ─────────────────────────▶ │ 🕵️ agent-tpm-interview-   │
   │   "the teacher"        │                            │     coach "the analyst"  │
   │                        │ ◀───────────────────────── │                          │
   │  • plans your course   │     returns an artifact     │  • MINE: repo → stories  │
   │  • writes lessons      │                            │  • GRADE: answer → score │
   │  • tracks your progress│                            │     + tough follow-ups   │
   └───────────────────────┘                            └──────────────────────────┘
```

---

## 💡 Why does this matter?

TPM interviews are **not** coding contests. They test whether you can **reason about systems, make trade-offs, manage risk, and tell credible stories about driving real outcomes through other people.** Most prep material is generic — and generic answers sound generic.

This toolkit fixes that with three ideas:

| Principle | Plain English |
|---|---|
| 🛰️ **Teach at "TPM altitude"** | Not *"write the code"* — but *"what will it cost, what could break, and in what order do we build it?"* |
| 🏗️ **Ground everything in YOUR work** | Your real projects become both system-design case studies **and** behavioral stories. Real beats hypothetical, every time. |
| 🧠 **Build durable recall, not cramming** | Short lessons + quizzes + spaced practice, so you remember it cold weeks later — when the interview actually happens. |

> **The honesty rule baked in:** built something with heavy AI assistance? That's a *strength* — when framed truthfully. The toolkit always leads with what's genuinely yours (the decisions, trade-offs, and outcomes), never fake hand-coding. 🤝

---

## ⚙️ How it works (plain English)

### 🧑‍🏫 The teacher: `skill-teach-tpm`

Think of it as a course that builds itself around you. When you start, it **interviews you first** — what company, what level, which project to ground in — then sets up a study workspace and teaches across three tracks:

```
   THE THREE TRACKS
   ═══════════════════════════════════════════════════

   1️⃣  SYSTEM DESIGN        "Sketch it. Now reason about scale, cost & risk."
       (TPM lens)            📚 grounded in the System Design Primer
                                + Hello Interview

   2️⃣  DOMAIN KNOWLEDGE     "Know enough to earn engineers' trust &
       (role-related)         ask the right questions."

   3️⃣  BEHAVIORAL / STAR    "Tell the story of a decision you owned —
       (the brag book)        with a measurable result."

   ═══════════════════════════════════════════════════
   ...and they interlock: one real project feeds all three. 🔗
```

It keeps state in plain files in your workspace, so it **remembers across sessions**:

```
   your-study-workspace/
   ├── 📌 MISSION.md            ← why you're prepping (company, level, goal)
   ├── 📖 lessons/*.html        ← short, beautiful, visual lessons + quizzes
   ├── 🃏 reference/*.html      ← cheat-sheets you reread before the interview
   ├── 💪 brag-book/*.md        ← your STAR stories (the "brag book")
   ├── ❓ behavioral-questions.md← common questions → which story answers each
   ├── 🧾 learning-records/*.md  ← what you've mastered (so it won't re-teach it)
   └── 📚 GLOSSARY.md / RESOURCES.md / NOTES.md
```

### 🕵️ The analyst: `agent-tpm-interview-coach`

A **read-only** helper (it looks, it never edits) with two modes:

```
   MODE: MINE 🪏                          MODE: GRADE 🎓
   ─────────────────────────             ─────────────────────────
   INPUT:  a code repo                   INPUT:  your practice answer
   ▼                                     ▼
   scans architecture, files,            scores it vs. the TPM rubric,
   & git history for                     finds the gaps, and writes the
   "decision moments"                    3–5 tough follow-up questions
   ▼                                     a real interviewer would ask
   OUTPUT: ranked STAR                   ▼
   story candidates 💪                   OUTPUT: a scorecard + fixes 📊
```

Because it's read-only, there's a clean division of labor: **the analyst figures things out; the teacher writes them into your workspace.** 🧩

---

## 📦 What's in this repo

```
TPM skills and agents/
├── README.md
├── skill-teach-tpm/
│   └── SKILL.md                       ← the teaching skill
├── skill-mine-star-story/
│   └── SKILL.md                       ← the story-writer skill
└── agent-tpm-interview-coach/
    └── agent-tpm-interview-coach.md   ← the analyst agent
```

> 🏷️ **Naming convention:** the `skill-` / `agent-` prefixes make the repo self-documenting. A **skill** is a folder with a `SKILL.md` (it runs *in* your conversation, statefully). An **agent** is a single `.md` definition (it runs in its *own* isolated context and reports back).

> 🧩 **Miner vs. story-writer:** the agent's **MINE** mode scans a *whole repo* and returns a *ranked list of candidates* (read-only, never writes). **`skill-mine-star-story`** takes *one* slice of recent work and *writes one finished story*. Use MINE to find what's worth telling; use the skill to actually write one up.

---

## 🚀 Install & use

Claude Code discovers these from specific folders. Copy them where Claude looks:

```bash
# Skills → user-level (available everywhere) or a project's .claude/skills/
cp -r skill-teach-tpm ~/.claude/skills/
cp -r skill-mine-star-story ~/.claude/skills/

# Agent → user-level or a project's .claude/agents/
cp agent-tpm-interview-coach/agent-tpm-interview-coach.md ~/.claude/agents/
```

Then, in Claude Code:

```
/skill-teach-tpm   ← starts (or resumes) your coaching session
```

The teacher will call the analyst automatically when it needs to mine stories or grade an answer — or you can ask for it by name.

---

## 🧪 Sample examples

### Example 1 — 🏁 Kicking off your prep
```
You:  /skill-teach-tpm  I'm interviewing for a Senior TPM role at Google (L5).

Claude (teacher):
  Before we dive in, let me set the mission so every lesson is aimed right:
   1. Target: Google, L5 — got it. I'll calibrate to Google's hiring attributes.
   2. Which rounds are in your loop? (system design / behavioral / domain / HM?)
   3. Point me at a real project to ground in — a repo path works best.
  ...then writes MISSION.md and proposes your first lesson. 🎯
```

### Example 2 — 🪏 Mining your codebase for stories (MINE mode)
```
You:  Use agent-tpm-interview-coach to mine ~/projects/vectorcache for brag-book stories.

Agent returns:
  # Story candidates — vectorcache

  ### S1 — Chose pgvector over a dedicated vector DB
  - Decision moment: build-vs-buy on the vector store
  - Competencies: technical judgment, cost ownership, risk management
  - Evidence (code can prove): migrations/000_*.sql (HNSW + cosine),
    commit a1b2c3d "swap Pinecone client for pgvector"
  - ASK CANDIDATE: the deadline pressure, who pushed back, the $ saved
  - Strength: STRONG 💪
  ...
  ## Coverage note: strong on technical trade-offs;
     ❌ gap — no "stakeholder conflict" story yet.
```

### Example 3 — 🎓 Grading a practice answer (GRADE mode)
```
You:  Grade this STAR answer for "Tell me about driving through ambiguity": <your answer>

Agent returns:
  # Grade — "driving through ambiguity"
  Verdict: Borderline — strong decision, but the Result isn't measurable yet.

  Scorecard:
   Structure ............... ✅
   "I" vs "we" ............. ⚠️  drifts into "we" in the Action
   Measurable Result ....... ❌  "it went well" — needs a number
   Honesty-rule risk ....... ✅

  Adversarial follow-ups (what they'll ask next):
   1. What did YOU personally decide vs. the team?
   2. How did you measure that it worked?
   3. What would you do differently at 10× the scale?

  One thing to change first: replace the last line with a metric. 📈
```

### Example 4 — 🔁 The two working together
```
You:  Build my next behavioral lesson.

Teacher: (reads your learning-records, spots the "stakeholder conflict" gap)
  → delegates a MINE pass to the analyst to find a candidate story
  → interviews you for the human details code can't show
  → writes a new brag-book entry + a lesson that drills it
  → maps it into behavioral-questions.md so the gap is now ✅
```

### Example 5 — ✍️ Writing one story from a recent push (`skill-mine-star-story`)
```
You:  /skill-mine-star-story  my last push

Claude (story-writer):
  Here's the plot I'd tell — confirm before I write it:
   S: you owned a semantic-cache build for a paid customer on a tight window
   T: choose the vector-search foundation and own the consequences
   A: framed it build-vs-buy (pgvector vs. a dedicated vector DB), de-risked
      with a measured latency test, documented exit criteria
   R: shipped on schedule, cache hits in ~tens of ms, avoided a second bill
   Showcases: technical judgment · cost ownership · risk management
   ⚠️ I'll frame the "customer" and "deadline" as assumptions — correct me.

You:  Yep, but it was internal, not a customer. Go.

  → writes ./brag-book/0001-pgvector-vs-pinecone-decision.md
  → then discloses what it embellished:
     • Result "~tens of ms" — placeholder, confirm the real figure  [ASSUMED]
     • "documented exit criteria" — did you actually write these down? [ASSUMED]
  → you confirm/correct; it strips the [ASSUMED] tags from what's real. 🎯
```

---

## 🧭 What's intentionally *out* of scope

- ❌ LeetCode / DSA grinding (unless your specific loop has a coding screen)
- ❌ Low-level implementation a TPM would never be asked to hand-write
- ❌ Front-end framework deep-dives beyond what's needed to *discuss* a system

Staying in scope is a feature — it protects your prep time for what actually gets scored. ⏳

---

## 🙌 Credits & lineage

`skill-teach-tpm` is a TPM-specialized descendant of the excellent general-purpose
[`teach`](https://github.com/mattpocock/skills) skill — it keeps the learning-science core
(knowledge → skills → wisdom, storage strength, desirable difficulty, the zone of proximal
development) and layers the TPM interview lens on top.

---

*Built to be portable — drop these into any project and start prepping. Good luck out there! 🍀*
