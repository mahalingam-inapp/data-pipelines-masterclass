# Course Design Patterns: Diagrams, Code & Examples

This document describes the visual and interactive elements added across modules so you can extend or replicate them.

## 1. Diagrams (inline SVG)

- **Purpose:** Explain flow, architecture, and relationships without external image files.
- **CSS class:** `.diagram-box` (wrapper), `.diagram-title` (heading).
- **Where used:**
  - **Module 1:** Pipeline flow (Ingest → Transform → Store → Serve).
  - **Module 2:** Role handoffs (Architect → Pipeline → Analyst; Engineer).
  - **Module 3:** Use case flow (3 CSVs → Ingest → Clean → Join → Output).
  - **Module 4:** Sources and landing zone (DB, Files, API → Landing → Transform → Warehouse).
  - **Module 5:** Retry with exponential backoff (conceptual).
  - **Module 6:** Two sources → landing → downstream.
  - **Module 7:** Transform flow (Filter → Map → Join → Aggregate → Load).
  - **Module 8:** Medallion layers (Bronze → Silver → Gold) with distinct colors.
  - **Module 9:** Lineage (Landing → Bronze → Silver → Gold → Report).
  - **Module 10:** Promotion flow (Dev → Staging → Prod).
  - **Module 13:** Storage landscape (Warehouse, Lake, Mart, Cube; Lakehouse).
  - **Module 16:** Pipeline to report (Gold → Semantic layer → Power BI / Tableau).
  - **Module 17:** Star schema (Fact: Sales + dimensions: Product, Region, Date, Customer, Store).
  - **Module 18:** Tableau flow (Data → Extract/Live → Workbook → Dashboard).
  - **Module 20:** Capstone full pipeline (Ingest → Bronze → Silver → Gold → Quality/Mart → Report).

All diagrams use inline SVG so they scale and require no external assets.

## 2. Code snippets

- **Purpose:** Show real or conceptual SQL, Python, YAML, DAX, Tableau so learners can copy or adapt.
- **CSS:** `.code-block`, `.code-lang` (language label), `pre`/`code` (dark theme).
- **Where used:**
  - **Module 1:** Pipeline definition (conceptual YAML).
  - **Module 2:** Debugging checklist (pseudocode).
  - **Module 3:** Join step (SQL).
  - **Module 4:** Ingest CSV to landing (Python).
  - **Module 5:** Incremental fetch (pseudocode).
  - **Module 6:** API land (Python).
  - **Module 7:** Bronze to Silver (SQL, dedup).
  - **Module 8:** Silver to Gold aggregate (SQL).
  - **Module 9:** Bronze from landing (dbt-style SQL).
  - **Module 10:** dbt_project.yml (environments).
  - **Module 13:** Partitioned table DDL (SQL).
  - **Module 17:** DAX (Revenue YTD, Prior Year).
  - **Module 18:** Tableau LOD and % of total.

## 3. Worked examples

- **Purpose:** Before/after or step-by-step with concrete inputs/outputs.
- **CSS:** `.worked-example`, `.before`, `.after` (optional).
- **Where used:**
  - **Module 1:** From spreadsheets to pipeline (before: 3 CSVs in Excel; after: one pipeline output).
  - **Module 2:** What the engineer checks when "numbers are wrong" (checklist + code).
  - **Module 3:** Join step in SQL with explanation.
  - **Module 6:** API call and land (Python pattern).
  - **Module 7:** Bronze to Silver SQL + “Why filter before dedup?”
  - **Module 8:** Silver to Gold aggregate SQL.
  - **Module 9:** Bronze copy (dbt model example).

## 4. Interactive / demo boxes

- **Purpose:** “Try it” or “See answer” without leaving the page; encourage practice.
- **HTML:** `<details>` / `<summary>` for expandable content.
- **CSS:** `.demo-box`, `summary` (cursor, color).
- **Where used:**
  - **Module 1:** Draw the pipeline for “e-commerce orders” (example sketch).
  - **Module 2:** Role-play (engineer; analyst says revenue is low—what do you ask?).
  - **Module 3:** Fill in the one-page diagram template.
  - **Module 4:** What happens if you run the ingest twice? (idempotency).
  - **Module 5:** Design an incremental strategy for a `last_updated` source.
  - **Module 7:** Why filter before dedup? (reveal explanation).

## 5. Reusing these patterns

- **New diagram:** Add `.diagram-box` and `.diagram-title` (and optional SVG styles) in the module’s `<style>`; paste or draw SVG inside the box.
- **New code block:** Use `.code-block` > `.code-lang` + `pre` > `code`; set `.code-lang` text to the language (e.g. SQL, Python, YAML).
- **New worked example:** Use `.worked-example` > `h4` + paragraphs; use `.before` / `.after` for before/after contrast.
- **New demo:** Use `.demo-box` > `<details>` > `<summary>` (prompt) + `<div class="demo-content">` (answer or steps).

Modules are self-contained (no shared CSS file), so when adding a pattern to a new module, copy the relevant CSS from an existing module that already uses it.
