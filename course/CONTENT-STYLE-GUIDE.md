# Content Style Guide — Data Pipelines Masterclass

This guide aligns the data pipelines course with the level of detail and appeal of the [AI Masterclass](https://github.com/mahalingam-inapp/ai-masterclass/tree/main/course). Use it when writing or revising modules.

---

## 1. Opening (first screen)

- **What is X?** — One or two sentences that define the topic in plain language. No jargon before the definition.
- **Key Insight** — A single, memorable callout (e.g. “Clean, integrated data is 80% of AI success”). Use a `.key-insight` or `.info-box` with a short, bold line.
- **Why it matters** — One short paragraph on why this topic matters for the business or the learner (e.g. “Without pipelines, reports are manual and inconsistent.”).

---

## 2. Structure within the module

- **Numbered steps** — For processes (e.g. ingestion, ETL), use clear step headings: “Step 1: …”, “Step 2: …” with 2–4 sentences or bullets each.
- **One idea per paragraph** — Keep paragraphs to 2–4 sentences. Use a new paragraph for a new idea or example.
- **Subheadings (h3, h4)** — Use them often so the page is scannable (e.g. “Source types in detail”, “Push vs. pull”, “Landing zone concept”).

---

## 3. Callouts and boxes

- **.key-insight** — One standout idea (e.g. “Key insight: …”).
- **.info-box** — Explanatory note, tip, or “how it works” (blue left border).
- **.success-box** — Positive outcome, best practice, or “after” state (green).
- **.warning-box** or **.highlight-box** — Caution, trade-off, or “watch out” (amber).
- **.example-box** — Concrete scenario, before/after, or worked example with a clear title (e.g. “Example: Daily sales reporting”).

---

## 4. Tables and lists

- **Comparison tables** — Use when comparing options (e.g. Batch vs. Streaming, Source type vs. Update frequency). Headers: clear column names; rows: one option or scenario per row.
- **Bullet lists** — For 3+ items (e.g. “Real-World Applications”, “Key Takeaways”, “Common issues”). Use short phrases or one sentence per bullet.
- **Numbered lists** — For ordered steps or a sequence.

---

## 5. Examples and applications

- **Concrete examples** — Name a scenario (e.g. “Retail: POS + e‑commerce → daily sales view”) and what the pipeline does in one sentence.
- **Real-World Applications** — End the module (or a section) with a short list of 4–6 domains or use cases (e.g. “E‑commerce: customer 360, recommendations”).
- **Key Takeaways** — Last section before the quiz: 4–5 bullet points that summarize the module (e.g. “Pipelines run on a schedule and handle failures; batch is enough when daily latency is acceptable.”).

---

## 6. Tone and clarity

- **Direct and active** — “You connect to the API” rather than “The API is connected to.”
- **Concrete over abstract** — “Daily at 6 a.m.” instead of “on a schedule”; “Stripe, Salesforce” instead of “SaaS APIs.”
- **One number when it helps** — “80% of insight comes from reliable data”, “retry 3 times with backoff”, “keep Bronze 90 days.”
- **Short sentences** — Prefer two short sentences over one long one.

---

## 7. Quiz

- **Question** — Full sentence (e.g. “What does it mean for a classification problem to be linearly separable?”).
- **Options** — A) B) C) D) or A) B); keep options parallel in length and style.
- **Answer block** — Start with “Correct Answer: [letter]” then 1–2 sentences explaining why (no extra jargon).

---

## 8. CSS classes to use

Ensure each module has these (or equivalent) for a consistent look:

- `.key-insight` — Bold, standout sentence (e.g. background #f0f7ff, left border #764ba2).
- `.key-takeaways` — Bullet list with title “Key Takeaways” (e.g. .success-box style).
- `.warning-box` — Amber/yellow for cautions (already .highlight-box in some modules).
- `.success-box` — Green for “after”, best practice, or success.
- `.example-box` — White box, border, optional light shadow; title inside (e.g. h4).
- Tables: `th` background #667eea, `tr:nth-child(even)` background #f8f9fa.

---

## 9. Per-module checklist

Before considering a module “done”:

- [ ] Opening: clear “What is X?” and one Key Insight or “Why it matters”.
- [ ] At least one .example-box or worked example with a concrete scenario.
- [ ] At least one table (comparison, reference, or before/after).
- [ ] Key Takeaways (4–5 bullets) before the quiz.
- [ ] Real-World Applications or similar (short list of use cases).
- [ ] Quiz: 5 questions, each with “Correct Answer: X” and a 1–2 sentence explanation.
- [ ] Paragraphs 2–4 sentences; subheadings every few paragraphs.
- [ ] Code/diagrams/demos where they help (no need for full interactivity like the AI course).

Use this guide when adding or revising content so the course feels as detailed and appealing as the AI masterclass, adapted for data pipelines.
