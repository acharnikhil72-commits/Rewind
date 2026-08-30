# Rewind

# Rewind — A Data-Grounded "What If" Career Simulator
 
**Hackathon:** Databricks Campus Hackathon (RVCE Edition)
**Track:** Track B — Creative Campus Intelligence
**Theme:** Genie-Powered Campus Intelligence
 
---
 
## One-Line Pitch
 
Pick a past or upcoming decision you're unsure about, and watch Genie replay your path if you'd chosen differently — backed by real alumni-outcome patterns, not guesses.
 
---
 
## The Problem
 
Students constantly second-guess their choices — "should I have joined that club instead of skipping it?", "should I do a research project or an internship this year?" — but they have no way to actually see what those choices tend to lead to. Career guidance today is generic advice, not evidence.
 
## The Idea
 
Rewind lets a student describe **one decision point** — something they already did, or something they're currently deciding — and Genie:
 
1. Finds alumni from a historical dataset whose early profile closely resembles the student's
2. Identifies how those alumni diverged based on a similar choice (e.g. joined the club vs. didn't; did a research project vs. didn't)
3. Narrates both paths side by side, citing real numbers ("students who made choice A had X% higher odds of outcome Y, based on N historical cases")
This is **not** a static "if X then Y" rule — it's Genie doing live, multi-step reasoning over data every time it's asked, which is what makes it fundamentally different from a chatbot wrapped around a lookup table.
 
## Why It's Different From a Typical "Placement Chatbot"
 
Most teams will build something that checks a student's profile against job requirements — a static comparison, not real intelligence. Rewind instead surfaces **patterns discovered from data**, not rules anyone typed in manually. Nobody pre-writes "students who join robotics + do 1 research project have 3x placement odds at core-engineering companies" — that pattern is found through actual analysis of the (synthetic) alumni dataset, and Genie's job is to retrieve it, apply it to a specific student, and explain it in plain language.
 
## The Demo Moment
 
Live, on stage: type in a real decision → Genie replays two divergent outcomes with cited stats, in front of the judges. No pre-recorded "imagine if this worked" — everything shown is actually running.
 
---
 
## Data Plan
 
| Table | Contents | Source |
|---|---|---|
| `students` | Current student profile: branch, CGPA, activities, skills | Self-entered / demo data |
| `alumni_outcomes` | Historical (synthetic) student profiles + final outcomes (role type, company tier, package band) | **Responsibly generated synthetic data** — clearly labeled as such in the submission |
| `discovered_patterns` | Correlations/patterns extracted from alumni_outcomes via analysis (e.g. correlation matrix or simple decision tree) | Generated once via a Databricks notebook |
 
**Important:** Synthetic data must be explicitly labeled as synthetic in the submission — don't imply it's real. This is allowed and expected per the brief ("real, open, or responsibly generated synthetic data").
 
---
 
## Databricks Architecture
 
1. **Unity Catalog + Delta tables** (Free Edition) — hold the three tables above
2. **Notebook analysis** — one-time correlation/pattern-discovery pass over the synthetic alumni dataset, output stored as `discovered_patterns`
3. **Genie Agent** — configured over all three tables, with sample queries and verified answers/business rules so responses are governed, not freeform SQL guesses
4. **Genie Ontology** — defines shared terms ("similar profile," "outcome tier," "divergence point") so answers stay consistent
5. **Agent mode** — used for the actual "what if" query: multi-step reasoning that finds comparable alumni, retrieves the pattern, and generates a cited narrative report
6. **Frontend** — a simple choice-input UI (or the native Genie chat interface) is enough; the differentiation is entirely in the reasoning quality, not the visuals
---
 
## Build Scope (Keep It Tight)
 
- ❌ No social graph, no leaderboard, no certificate upload/OCR, no multi-turn game loop
- ✅ One input (a decision), one Genie-powered reasoning chain, one output screen (divergent path comparison)
- Everything shown to judges should be fully real and running — nothing mocked or "imagine if"
---
 
## Why This Fits the Brief
 
- **Track B match**: A "data-powered 'what if?' simulator" is explicitly listed as a suggested direction
- **Genie at the core**: Every query requires real multi-step reasoning (find comparable alumni → retrieve pattern → explain), not a static lookup
- **Data requirement met**: Real student input + clearly labeled synthetic alumni data
- **Databricks Free Edition**: Fully buildable using Delta tables, Genie Agent, Agent mode, and Ontology — all currently free
---
 
## Team To-Dos
 
- [ ] Generate synthetic alumni dataset (200–500 rows) with deliberate, realistic correlations baked in
- [ ] Run notebook analysis to extract 5–10 genuine discovered patterns
- [ ] Set up Delta tables in Unity Catalog
- [ ] Configure Genie Agent + Ontology + verified answers
- [ ] Build simple input UI for the "decision" query
- [ ] Test the live demo flow end-to-end multiple times before presenting
- [ ] Prepare a tight, clear explanation of the tech stack for Q&A
