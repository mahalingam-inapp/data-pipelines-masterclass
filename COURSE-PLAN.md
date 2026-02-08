# End-to-End Data Pipelines Course Plan

A progressive, practice-oriented curriculum from fundamentals to capstone—with use cases and interactive elements in every section.

---

## Overview

| Section | Focus | Level |
|--------|--------|--------|
| 1 | Introduction & Purpose | Beginner |
| 2 | Data Ingestion | Beginner → Intermediate |
| 3 | ETL & Medallion Architecture | Intermediate |
| 4 | Data Management | Intermediate → Advanced |
| 5 | Storage | Intermediate |
| 6 | Analytics (Power BI, Tableau) | Intermediate → Advanced |
| 7 | Capstone, Simulation, Layered View & Roadmap | Advanced / Holistic |

The course is delivered as **23 modules** across these 7 sections.

## Role-based pathways

Elements throughout the course are tagged for **technical architects**, **data engineers**, and **analysts**. Use these to tailor depth and activities.

| Role | Primary focus | Where to lean in |
|------|----------------|------------------|
| **Technical architect** | Design, trade-offs, standards, governance, scalability, technology selection | Sections 1, 3, 4, 5, 7 — diagrams, decision frameworks, review exercises |
| **Data engineer** | Implementation, orchestration, testing, reliability, performance, tooling | Sections 2, 3, 4, 7 — labs, code, DAGs, failure simulation |
| **Analyst** | Consumption, semantics, reporting, discovery, self-serve, data requests | Sections 1, 4, 5, 6, 7 — reports, dictionaries, lineage trace, business-question flow |

See the **Appendix: Role-specific elements** for a full mapping and suggested activities per section.

---

# Section 1: Introduction and Purpose

## 1.1 Learning Objectives
- Define data pipelines and their role in modern organizations
- Distinguish pipelines from ad hoc scripts and one-off ETL
- Identify business drivers: reporting, ML, compliance, real-time ops
- Map pipeline concepts to roles (analyst, engineer, architect)

## 1.2 Chapter Outline

### Chapter 1.1 — What Is a Data Pipeline?
- **Basics:** Definition; pipeline vs. ETL vs. data integration; batch vs. streaming (high-level).
- **Ramp-up:** Pipeline stages (ingest → transform → store → serve); failure modes and why reliability matters.
- **Practical use cases:** 
  - Daily sales reporting from POS to dashboard
  - Customer 360 from CRM, support, and billing
  - Regulatory reporting (e.g., finance, healthcare)
- **Interactive elements:** 
  - Poll: “Which stage fails most often in your experience?”
  - Draw-the-pipeline: Given a scenario (e.g., “e-commerce orders”), sketch boxes and arrows on a shared board (Miro/FigJam or whiteboard).

### Chapter 1.2 — Why Data Pipelines Matter
- **Basics:** Cost of bad data; speed of insight; single source of truth.
- **Ramp-up:** ROI of automation; data quality and trust; governance and lineage.
- **Practical use cases:** 
  - Reducing manual Excel consolidation
  - Enabling self-serve analytics
  - Supporting audit and compliance
- **Interactive elements:** 
  - Discussion: “Describe one manual data process you’d like to automate.”
  - Quick vote: Rank pain points (latency, quality, access, cost).

### Chapter 1.3 — Roles and Responsibilities
- **Basics:** Data engineer, analyst, architect; handoffs and ownership.
- **Ramp-up:** Platform vs. pipeline ownership; SLA and monitoring expectations.
- **Interactive elements:** 
  - Role-play: “You are the data engineer; the analyst says the numbers are wrong—what do you check first?”

### By role: Technical architect | Data engineer | Analyst
- **Architect:** Define a simple “pipeline design checklist” (sources, frequency, failure handling, ownership); review another team’s diagram against scalability and single point of failure.
- **Engineer:** Turn the one-page diagram into a minimal runnable spec (e.g., inputs, outputs, one transform step) and note which component you’d implement first.
- **Analyst:** Annotate the diagram with “where I would get my report data” and one question you’d ask the engineer (e.g., “How fresh is this?” or “What if a file is missing?”).

## 1.3 Section Use Case: “From Spreadsheets to Pipeline”
- **Scenario:** A small team currently merges 3 CSV exports (sales, returns, inventory) in Excel every Monday. Goal: one weekly pipeline that outputs a single dataset for reporting.
- **Deliverables:** A one-page pipeline diagram (ingest → clean → join → output) and a short “before vs. after” narrative.
- **Interactive wrap-up:** Peer review of one other team’s diagram; suggest one improvement (e.g., add validation, handle missing files).

---

# Section 2: Data Ingestion

## 2.1 Learning Objectives
- Compare batch vs. streaming ingestion and when to use each
- Use connectors, APIs, and file-based ingestion patterns
- Handle schemas, file formats (CSV, JSON, Parquet), and incremental loads
- Apply basic error handling and idempotency

## 2.2 Chapter Outline

### Chapter 2.1 — Ingestion Fundamentals
- **Basics:** Source types (DBs, files, APIs, events); push vs. pull; frequency (daily, hourly, real-time).
- **Ramp-up:** Throughput and volume; schema-on-read vs. schema-on-write; landing zone concept.
- **Practical use cases:** 
  - Ingesting SaaS API data (e.g., Stripe, Salesforce)
  - Loading files from SFTP/S3/GCS
  - Consuming change-data-capture (CDC) from a transactional DB
- **Interactive elements:** 
  - Live demo: Ingest a sample CSV and a sample JSON from URLs; show raw vs. structured view.
  - Quiz: “For 10M events/day from mobile app—batch or stream?”

### Chapter 2.2 — Connectors, APIs, and Files
- **Basics:** REST APIs (auth, pagination, rate limits); file-based (CSV, JSON, Parquet); cloud storage (S3, ADLS, GCS).
- **Ramp-up:** Idempotent loads; incremental keys and watermarking; handling duplicates and late data.
- **Practical use cases:** 
  - Full vs. incremental sync for a CRM table
  - Webhook + API fallback for order events
  - Daily file drop with filename/date conventions
- **Interactive elements:** 
  - Lab: Call a public API (e.g., OpenWeather, GitHub), persist response to a file; discuss idempotency if run twice.
  - Pair exercise: Design an incremental strategy for a “last_updated” source table.

### Chapter 2.3 — Reliability and Error Handling
- **Basics:** Retries, backoff, dead-letter queues; logging and alerting.
- **Ramp-up:** Partial failure handling; replay and backfill; idempotent design.
- **Interactive elements:** 
  - Scenario: “API returns 500 for 2 hours then recovers—what should the pipeline do?” (discuss retry, DLQ, alert).

### By role: Technical architect | Data engineer | Analyst
- **Architect:** Document an "ingestion decision matrix": when to use batch vs. stream, push vs. pull, and which landing pattern (object store vs. DB); add one scalability or cost consideration.
- **Engineer:** Implement the Section use case (CSV + API → landing) with retry logic and one idempotency safeguard (e.g., run twice, same result); add logging or a simple alert.
- **Analyst:** Define a "data request" for a new source: business question, required fields, acceptable latency, and how you'd validate the data once it lands.

## 2.3 Section Use Case: “Ingest and Land”
- **Scenario:** Ingest (1) a public dataset (e.g., sample sales CSV from a URL), (2) one REST API (e.g., mock or public), into a “landing” area (local folder or cloud bucket). Document schema and any assumptions.
- **Deliverables:** Script or low-code flow that runs on demand; one-page doc with source, frequency, and error-handling notes.
- **Interactive wrap-up:** Swap with another learner; run their ingestion and suggest one improvement (e.g., add a timestamp column, handle empty response).

---

# Section 3: ETL and Medallion Architecture

## 3.1 Learning Objectives
- Implement core ETL operations: filter, map, aggregate, join
- Design and implement Bronze → Silver → Gold (medallion) layers
- Apply incremental processing and SCD Type 2 where appropriate
- Use at least one ETL tool or framework (e.g., dbt, Spark, ADF, Databricks)

## 3.2 Chapter Outline

### Chapter 3.1 — ETL Fundamentals
- **Basics:** Extract (covered in Section 2), Transform (clean, reshape, aggregate), Load (insert/upsert into target).
- **Ramp-up:** Transform patterns (dedup, pivot, surrogate keys); testing (row counts, checksums, sample comparisons).
- **Practical use cases:** 
  - Normalizing product catalog from multiple sources
  - Building a daily snapshot of “customer state”
  - Aggregating clickstream to session-level metrics
- **Interactive elements:** 
  - Live coding: Take landed CSV, apply 3 transforms (rename, filter, add column); show before/after.
  - Quiz: “Which transform should run first: dedup or filter? Why?”

### Chapter 3.2 — Medallion Architecture (Bronze, Silver, Gold)
- **Basics:** Bronze = raw copy; Silver = cleaned, conformed, integrated; Gold = business-level aggregates and marts.
- **Ramp-up:** When to add a layer; schema evolution; partitioning and clustering for performance.
- **Practical use cases:** 
  - Bronze: raw API payloads; Silver: flattened, typed, deduplicated; Gold: KPIs by region and product.
  - Adding a new source: only new Bronze + Silver tables, reuse Gold logic where possible.
- **Interactive elements:** 
  - Diagramming: Given a source (e.g., orders API), draw Bronze/Silver/Gold tables and list 2–3 columns per layer.
  - Debate: “Do we need Bronze if we have a data lake?” (discuss audit, replay, cost).

### Chapter 3.3 — Incremental Processing and SCD
- **Basics:** Full refresh vs. incremental; key columns and watermarks; SCD Type 1 vs. Type 2.
- **Ramp-up:** Merge/upsert semantics; handling late-arriving and out-of-order data.
- **Practical use cases:** 
  - Daily incremental of “orders” by `order_id` and `updated_at`
  - SCD Type 2 for “customer” (history of address/segment changes)
- **Interactive elements:** 
  - Worksheet: Given a small table and an “updates” file, manually perform one merge (Type 1) and one Type 2 step; compare row counts.
  - Tool lab: Implement one incremental model in dbt (or equivalent) with a stub source.

### By role: Technical architect | Data engineer | Analyst
- **Architect:** Produce a "medallion standards" one-pager: naming, partitioning, retention, and when to add a layer; review one team's Bronze/Silver/Gold design for governance and lineage.
- **Engineer:** Build the full medallion (Bronze → Silver → Gold) with at least one incremental Silver/Gold model; add a simple lineage artifact (e.g., dbt docs or a table list).
- **Analyst:** Map "report columns" back to Bronze/Silver/Gold (which layer and table); write one business rule that should be enforced in Silver or Gold (e.g., "revenue ≥ 0") and how you'd verify it in a report.

## 3.3 Section Use Case: “Medallion in Practice”
- **Scenario:** Start from the Section 2 use case (landed sales + one API). Build Bronze (raw), Silver (cleaned, joined, deduplicated), and Gold (e.g., daily sales by product and region). Use any tool (SQL, dbt, Spark, ADF, etc.).
- **Deliverables:** Code or config for each layer; lineage diagram; short note on incremental strategy for Silver/Gold.
- **Interactive wrap-up:** Present Bronze→Silver→Gold to a partner; they ask one “what if” (e.g., new column, new source) and you outline the change.

---

# Section 4: Data Management

## 4.1 Learning Objectives
- Apply data engineering practices: versioning, testing, documentation, orchestration
- Implement cleaning, validation, and staging patterns
- Define “processed” and “curated” datasets with clear ownership
- Introduce data quality checks and monitoring

## 4.2 Chapter Outline

### Chapter 4.1 — Data Engineering Practices
- **Basics:** Code and config in version control; environments (dev/staging/prod); repeatable runs.
- **Ramp-up:** Testing (unit, integration); documentation (data dictionary, lineage); code review for pipelines.
- **Practical use cases:** 
  - Moving a pipeline from “someone’s laptop” to scheduled runs in CI/CD
  - Adding a data quality test that blocks release if row count drops 50%
- **Interactive elements:** 
  - Checklist: Review a sample pipeline repo—does it have README, env config, and at least one test?
  - Role-play: Propose a “definition of done” for a new pipeline (list 5 criteria).

### Chapter 4.2 — Cleaning, Validation, and Staging
- **Basics:** Cleaning (nulls, types, formats); validation (ranges, referential integrity); staging = intermediate tables used only by pipelines.
- **Ramp-up:** Reusable rules (e.g., “email format”, “positive amount”); soft vs. hard failures; quarantine tables.
- **Practical use cases:** 
  - Staging: raw → cleaned with types and constraints before Silver
  - Rejecting bad rows to a quarantine table and alerting
- **Interactive elements:** 
  - Lab: Write 3 validation rules for a sample dataset; run them and count pass/fail; decide “block” vs. “warn”.
  - Discussion: “One critical column has 5% nulls—fix at source, impute, or exclude?”

### Chapter 4.3 — Processed and Curated Data
- **Basics:** “Processed” = post-Silver, ready for consumption; “curated” = business-approved, documented, governed.
- **Ramp-up:** Ownership (who can change what); SLAs; access control and PII handling.
- **Practical use cases:** 
  - Processed: Silver tables exposed to analysts; Curated: certified datasets for company-wide reporting
  - PII: strip or mask in processed; restrict access to curated PII dataset
- **Interactive elements:** 
  - Matrix: Fill a 2×2 (Processed vs. Curated × Internal vs. External); where does “board report” sit?
  - Scenario: “Marketing wants a new column in the curated customer table”—walk through change process.

### Chapter 4.4 — Data Quality and Monitoring
- **Basics:** Expectations (row count, nulls, uniqueness); freshness; basic alerting.
- **Ramp-up:** Data quality frameworks (e.g., Great Expectations, Soda); dashboards for pipeline health.
- **Interactive elements:** 
  - Implement one freshness check and one distribution check (e.g., “revenue > 0”) in a tool or SQL.
  - Review a sample “pipeline run” report: identify which check failed and what to do next.

### By role: Technical architect | Data engineer | Analyst
- **Architect:** Define "definition of done" for a pipeline release (tests, docs, ownership, SLA); design a simple data-quality SLA (e.g., freshness + one critical check) and escalation path.
- **Engineer:** Add validation rules and a quarantine path to the medallion use case; implement one automated quality check (e.g., row count or uniqueness) and wire it into a run (or DAG).
- **Analyst:** Co-author the data dictionary for the Gold table (business names, definitions, known caveats); write one "sanity check" you run when you get new data (e.g., compare to prior period).

## 4.4 Section Use Case: “From Raw to Curated”
- **Scenario:** Extend the medallion use case: add (1) validation rules and a quarantine path, (2) one data quality check (e.g., row count or key metric), (3) a one-page data dictionary for the Gold table. Optionally: one orchestration run (e.g., Airflow DAG or pipeline schedule).
- **Deliverables:** Validation logic, quality check, dictionary, and (optional) DAG or schedule description.
- **Interactive wrap-up:** Exchange dictionaries with another team; use their Gold table description to write one analytical query and one quality check.

---

# Section 5: Storage

## 5.1 Learning Objectives
- Compare data warehouses, data lakes, data marts, and cubes
- Choose storage by use case: BI, ML, ad hoc, compliance
- Understand key concepts: partitioning, indexing, and access patterns
- Map medallion and processed/curated layers to physical storage

## 5.2 Chapter Outline

### Chapter 5.1 — Storage Types and Trade-offs
- **Basics:** Warehouse (structured, SQL, analytics); lake (files, scale, diverse formats); mart (subset for a team/use case); cube (pre-aggregated for fast BI).
- **Ramp-up:** Lakehouse (unified); when to use which; cost and performance trade-offs.
- **Practical use cases:** 
  - Warehouse: reporting and ad hoc SQL
  - Lake: raw events, ML features, archival
  - Mart: “Marketing performance” or “Supply chain”
  - Cube: executive dashboard with sub-second response
- **Interactive elements:** 
  - Drag-and-drop: Place 5 use cases (e.g., “ML training”, “board KPI”, “raw logs”) on the right storage type.
  - Discussion: “We have only a warehouse today—when would you add a lake?”

### Chapter 5.2 — Warehouses and Lakes in Detail
- **Basics:** Key offerings (Snowflake, BigQuery, Redshift, Synapse; S3 + Athena, Delta, etc.); tables vs. files; ACID and consistency.
- **Ramp-up:** Partitioning and clustering; compression; access control and encryption.
- **Practical use cases:** 
  - Storing Bronze in object storage, Silver/Gold in warehouse (or lakehouse)
  - Partitioning by date for incremental and pruning
- **Interactive elements:** 
  - Compare: Two slides—same query on unpartitioned vs. partitioned table; discuss impact on cost and speed.
  - Lab: Create one partitioned table (or folder layout) and run a query that benefits from partition pruning.

### Chapter 5.3 — Data Marts and Cubes
- **Basics:** Mart = subject-area subset (schema, tables, maybe a DB); cube = aggregated model (measures, dimensions) for fast BI.
- **Ramp-up:** When to build a mart vs. query Gold; when to add a cube (latency, concurrency); tools (e.g., Analysis Services, Looker semantic layer).
- **Practical use cases:** 
  - “Sales mart”: sales, product, region; “Finance mart”: GL, budgets
  - Cube: “Revenue by region, product, month” with drill-down
- **Interactive elements:** 
  - Design: For “Revenue by region and product”, list dimensions and measures; sketch a simple cube structure.
  - Tool tour: Brief demo of one cube or semantic layer (e.g., Power BI dataset, Tableau data model) and point out dimensions/measures.

### By role: Technical architect | Data engineer | Analyst
- **Architect:** Own the "storage map" deliverable: justify lake vs. warehouse per layer; add security and access boundaries (who can read Bronze vs. Gold); document one "10x scale" or "real-time" evolution.
- **Engineer:** Implement the chosen storage (e.g., create partitioned tables or lake folders, one mart or cube); run one query that demonstrates partition pruning or mart usage.
- **Analyst:** Specify "what I need in the mart" (dimensions, measures, grain) and one performance requirement (e.g., "dashboard load < 5 sec"); review the storage map from a "can I build my report?" angle.

## 5.5 Section Use Case: “Storage Strategy for One Domain”
- **Scenario:** Pick one business domain (e.g., e-commerce orders). Propose: (1) where Bronze/Silver/Gold live (lake vs. warehouse), (2) one data mart (tables and purpose), (3) whether a cube is justified and why. Document in a one-page “storage map”.
- **Deliverables:** Storage map diagram and short rationale; optional: create the mart (or cube) in a sandbox.
- **Interactive wrap-up:** Present the map; instructor or peer asks “What if we add 10x volume?” or “What if we need real-time?”—revise the map verbally or on the diagram.

---

# Section 6: Analytics

## 6.1 Learning Objectives
- Connect pipelines to analytics: from curated data to reports and dashboards
- Build and share reports in Power BI (data model, DAX, visuals)
- Build and share workbooks in Tableau (data model, calculations, dashboards)
- Apply best practices: performance, governance, and self-serve

## 6.2 Chapter Outline

### Chapter 6.1 — From Pipeline to Analytics
- **Basics:** Curated/Gold as source of truth; refresh schedules; semantic layer and business metadata.
- **Ramp-up:** DirectQuery vs. import; incremental refresh; row-level security (RLS).
- **Practical use cases:** 
  - Daily refresh of a Power BI dataset from a Gold table
  - Tableau extract on a mart with weekly refresh
- **Interactive elements:** 
  - Trace: From “I click a filter” to “which table and column in the pipeline?” (lineage discussion).
  - Poll: “How often should the sales dashboard refresh?” (real-time vs. daily vs. weekly).

### Chapter 6.2 — Power BI: Data Model and DAX
- **Basics:** Connect to a database or file; tables, relationships, and star schema; measures vs. columns.
- **Ramp-up:** DAX for common metrics (YTD, prior period, ratios); calculated tables; time intelligence.
- **Practical use cases:** 
  - Sales report: revenue, units, growth %; filters by region, product, date
  - KPI card with target vs. actual and conditional formatting
- **Interactive elements:** 
  - Live: Build a simple star schema (one fact, two dimensions) in Power BI; add one measure (e.g., Total Revenue).
  - Challenge: Write one DAX measure (e.g., “Revenue YoY %”) in a shared PBIX or in a snippet; compare with solution.

### Chapter 6.3 — Power BI: Visuals and Dashboards
- **Basics:** Choosing visuals (bar, line, matrix, map); filters (visual, page, report); drill-through and bookmarks.
- **Ramp-up:** Performance (aggregations, reduce columns); sharing (workspace, apps); RLS.
- **Practical use cases:** 
  - Executive dashboard: KPIs, trend, top N; export to PDF
  - Self-serve: parameterized report for “any region”
- **Interactive elements:** 
  - Lab: Publish a report to a workspace; configure one filter and one drill-through; share with a peer for feedback.
  - Critique: Review a sample report—list 2 UX improvements (e.g., default filter, clearer titles).

### Chapter 6.4 — Tableau: Data Model and Calculations
- **Basics:** Connect to a table or file; dimensions and measures; shelves (rows, columns, marks).
- **Ramp-up:** Calculated fields (LOD, table calcs); parameters; blending (when needed).
- **Practical use cases:** 
  - Sales by region and product with “% of total” and “running sum”
  - Parameter: “Select metric” (Revenue, Units, Margin) driving the view
- **Interactive elements:** 
  - Live: Build one bar chart and one line chart from the same dataset; add a quick table calculation.
  - Pair: Write one LOD expression (e.g., “Revenue per customer”) and explain the level.

### Chapter 6.5 — Tableau: Dashboards and Storytelling
- **Basics:** Dashboard layout; actions (filter, highlight, URL); stories for narrative.
- **Ramp-up:** Performance (extracts, filters); Tableau Server/Cloud (scheduling, permissions).
- **Practical use cases:** 
  - Regional dashboard with map + detail table; click region to filter
  - Story: “Q3 performance” with three points (overview, problem, action)
- **Interactive elements:** 
  - Lab: Create a dashboard with two views and one filter action; publish to Server/Cloud (or export); have a partner test the interaction.
  - Compare: Same dataset in Power BI and Tableau—when would you choose which for your org?

### By role: Technical architect | Data engineer | Analyst
- **Architect:** Define "report/dataset governance": who can publish, certification criteria, refresh SLAs, and RLS standards; review one report for compliance (sources, refresh, security).
- **Engineer:** Document how the report connects to the pipeline (source table, refresh job, incremental vs. full); add or validate one performance safeguard (e.g., aggregation table, filter pushdown).
- **Analyst:** Build both the Power BI and Tableau deliverables; document the "report card" (purpose, audience, refresh) and one improvement; trace one visual back to pipeline column and quality check.

## 6.6 Section Use Case: “End-to-End Report”
- **Scenario:** Use the Gold (or curated) dataset from earlier sections. Build (1) one Power BI report (data model + 2–3 visuals + one DAX measure) and (2) one Tableau workbook (2 views + one dashboard with an action). Document data source and refresh assumption.
- **Deliverables:** PBIX and TWBX (or links); one-page “report card” (purpose, audience, refresh, one improvement to do next).
- **Interactive wrap-up:** Demo to a small group; collect one “what I’d add” from each viewer.

---

# Section 7: Capstone, Simulation, Layered View, and Roadmap

Section 7 comprises **four modules (20–23)**: Capstone (full pipeline), Simulation & Holistic View, **Layered Pipeline View**, and Roadmap & Next Steps.

## 7.1 Learning Objectives
- Apply the full pipeline lifecycle in one coherent scenario
- Make trade-off decisions (batch vs. stream, layers, storage, tooling)
- Practice troubleshooting and iteration in a safe environment
- Explore the end-to-end pipeline by role and platform (business user, AWS, Azure)
- Present and document an end-to-end solution

## 7.2 Chapter Outline

### Chapter 7.1 — Capstone: Full Pipeline Project
- **Purpose:** One project that spans ingestion → ETL (medallion) → management (quality, staging) → storage (warehouse/lake + mart) → analytics (Power BI or Tableau).
- **Scenario options:** 
  - **Retail:** POS + e-commerce + returns → daily sales and inventory view → mart → executive and ops dashboards.
  - **SaaS:** Product events + billing + support tickets → usage and churn metrics → mart → product and success dashboards.
  - **Internal ops:** HR + finance + project data → headcount, cost, and project status → mart → management reporting.
- **Deliverables:** 
  - Pipeline design doc (sources, layers, storage, refresh)
  - Code/config for at least Bronze → Silver → Gold
  - One data quality check and one curated dataset
  - One report or dashboard (Power BI or Tableau) with short narrative
- **Interactive elements:** 
  - Kickoff: Form teams; pick scenario; 15-minute “design on a whiteboard” and share back.
  - Midpoint review: Each team presents “what’s done, what’s blocked”; peers ask one question and suggest one idea.
  - Final showcase: 10-minute demo per team; others score on “clarity of pipeline”, “usability of report”, “documentation”.

### Chapter 7.2 — Simulation: Failure and Recovery
- **Purpose:** Experience failures and recovery in a controlled setting (e.g., broken source, wrong schema, late data).
- **Scenarios:** 
  - Source file missing → pipeline fails → fix (retry, fallback, alert) and re-run.
  - Schema change (new required column) → pipeline breaks → update Silver and Gold and deploy.
  - Duplicate key in source → duplicate rows in Gold → add dedup and backfill.
- **Interactive elements:** 
  - Instructor (or script) “breaks” the pipeline; teams diagnose and fix in a time box; debrief on steps taken.
  - Rotate roles: one person breaks, another fixes; then swap.

### Chapter 7.3 — Holistic View: From Business Question to Answer
- **Purpose:** Tie the course together: business question → data need → pipeline design → storage → report → action.
- **Flow:** 
  - Start with a business question (e.g., “Why did churn increase in Q3?”).
  - Map to: which data (events, billing, support), which layers, which mart, which report.
  - Discuss: what’s missing, what’s next (e.g., real-time, ML).
- **Interactive elements:** 
  - Roundtable: Each participant brings one real business question; group picks two and walks through the “question → pipeline → report” flow on a whiteboard.
  - One-pager: Write a “data request” template (question, needed data, suggested pipeline change, expected output) and use it for one of the roundtable questions.

### Chapter 7.4 — Layered Pipeline View
- **Purpose:** One continuous view of the pipeline from **data source to business consumption**, with all concepts in one place. Each layer can be viewed as a **Business user**, **Data Architect (AWS)**, or **Data Architect (Azure)** so participants see the same pipeline through different lenses.
- **Layers covered:** Data sources → Ingestion & Landing → Bronze → Staging → Validation & Quarantine → Silver → Gold → Quality checks → Storage (warehouse / lake / mart / cube / lakehouse) → Curated dataset & Dictionary → Analytics & Report → Business consumption.
- **Interactive elements:** 
  - Per-layer dropdown: switch between “Business user” (outcomes, trust, what I see/use), “Data Architect (AWS)” (e.g. S3, Glue, Redshift, Athena, QuickSight, Kinesis, DMS), and “Data Architect (Azure)” (e.g. ADLS, Data Factory, Synapse, Power BI, Purview, Event Hubs). The illustration or content for that layer updates to match.
  - Use with capstone (Module 20) and simulation (Module 21) to reinforce where each concept sits in the stack and how it appears to different roles and platforms.

### Chapter 7.5 — Roadmap and Next Steps
- **Purpose:** Where to go after the course: advanced topics (streaming, ML pipelines, data mesh) and resources. This is the final module (Module 23).
- **Interactive elements:** 
  - Self-assessment: “Rate your confidence (1–5) on ingestion, ETL, storage, analytics”; identify one area to deepen.
  - Resource share: Each person posts one resource (course, book, tool doc) for the group.
  - Completion: Use the role-specific appendix for ongoing reference and to run sessions with your team.

### By role: Technical architect | Data engineer | Analyst
- **Architect:** Lead or review the pipeline design doc; present trade-offs (batch vs. stream, layers, storage, tooling) and the "failure/recovery" strategy; facilitate the "business question → pipeline → report" roundtable.
- **Engineer:** Own implementation (ingestion, medallion, quality, optional orchestration); run the failure simulation (diagnose and fix); document runbook items (e.g., "if source fails, do X").
- **Analyst:** Own the report/dashboard and the "data request" one-pager; in the showcase, present from a stakeholder perspective (what question it answers, how often it's updated, one caveat); participate in roundtable with a real business question.

## 7.6 Capstone Use Case (Summary)
- **End-to-end scenario:** One of the capstone options above (retail, SaaS, or internal ops), executed over 2–4 weeks (or compressed in a bootcamp).
- **Holistic deliverables:** Design doc, pipeline code, quality checks, one mart (or cube) decision, one report/dashboard, and a short “lessons learned” doc.
- **Interactive wrap-up:** Presentation to “stakeholders” (instructor or peers role-playing); Q&A on design choices and trade-offs.
- **Section 7 modules (20–23):** Module 20 Capstone; Module 21 Simulation & Holistic View; Module 22 Layered Pipeline View; Module 23 Roadmap & Next Steps.

---

# Appendix: Quick Reference

## Section → Use Case Mapping
| Section | Dummy / Section Use Case |
|--------|---------------------------|
| 1 | From Spreadsheets to Pipeline (diagram + narrative) |
| 2 | Ingest and Land (CSV + API → landing) |
| 3 | Medallion in Practice (Bronze → Silver → Gold) |
| 4 | From Raw to Curated (validation, quality, dictionary) |
| 5 | Storage Strategy for One Domain (storage map) |
| 6 | End-to-End Report (Power BI + Tableau from Gold) |
| 7 | Capstone (full pipeline + report); Simulation (failure/recovery); Layered Pipeline View (source→consumption by role/AWS/Azure); Roadmap & Next Steps |

## Interactive Element Types Used
- **Polls / votes:** Quick opinion or prior experience
- **Draw / diagram:** Whiteboard or Miro (pipeline, storage, flow)
- **Labs:** Hands-on with tool (API, dbt, PBI, Tableau)
- **Pair / small group:** Design incremental strategy, review diagram, swap reports
- **Role-play / scenario:** “You are the engineer; analyst says numbers are wrong”
- **Debate / discussion:** “Do we need Bronze?” “Batch or stream?”
- **Showcase / peer review:** Present and get structured feedback
- **Simulation:** Instructor/script breaks pipeline; teams fix and debrief

## Suggested Duration (High-Level)
- **Section 1:** 1–2 sessions  
- **Section 2:** 2–3 sessions  
- **Section 3:** 3–4 sessions  
- **Section 4:** 2–3 sessions  
- **Section 5:** 2 sessions  
- **Section 6:** 4–5 sessions (split Power BI / Tableau as needed)  
- **Section 7:** 3–5 sessions (capstone can span multiple weeks)  

Total: ~18–25 sessions (adjust for session length and audience level).

---

## Appendix: Role-specific elements

Use this to assign activities, breakout groups, or deeper dives by role in each section.

### Technical architect

| Section | Focus | Suggested elements |
|--------|--------|---------------------|
| 1 | Ownership and boundaries | Pipeline design checklist; diagram review for scalability and failure points; define “pipeline” vs. “platform” ownership. |
| 2 | Ingestion strategy | Decision matrix (batch vs. stream, push vs. pull); landing patterns; scalability and cost; security at rest/in transit. |
| 3 | Medallion and standards | Medallion standards one-pager (naming, partitioning, retention); when to add a layer; governance and lineage; review Bronze/Silver/Gold design. |
| 4 | Quality and release | Definition of done for pipelines; data-quality SLA and escalation; ownership of processed vs. curated; PII and access boundaries. |
| 5 | Storage and evolution | Storage map and rationale; lake vs. warehouse per layer; security and access; “10x scale” or “real-time” evolution. |
| 6 | Report and dataset governance | Who can publish; certification; refresh SLAs; RLS and source traceability; review report for compliance. |
| 7 | End-to-end design and trade-offs | Lead design doc; present trade-offs; failure/recovery strategy; facilitate business-question → pipeline → report. |

**Architect-heavy activities:** Design reviews, decision matrices, standards one-pagers, trade-off discussions, “what if we scale?” revisions.

---

### Data engineer

| Section | Focus | Suggested elements |
|--------|--------|---------------------|
| 1 | From diagram to spec | Turn pipeline diagram into minimal runnable spec; identify first component to implement. |
| 2 | Implementation and ops | Implement CSV + API landing with retry and idempotency; logging/alerting; run twice and verify. |
| 3 | Medallion build | Full Bronze → Silver → Gold; at least one incremental model; lineage (e.g., dbt docs). |
| 4 | Validation and quality | Validation rules and quarantine path; one automated quality check; wire into run or DAG. |
| 5 | Physical storage | Create partitioned tables or lake layout; one mart or cube; query showing partition pruning or mart use. |
| 6 | Pipeline–report link | Document source table and refresh job; aggregation or filter pushdown for performance. |
| 7 | Build and runbook | Own pipeline implementation and failure simulation; document runbook (e.g., “if source fails, do X”). |

**Engineer-heavy activities:** Labs, code/config, DAGs, runbooks, failure simulation, idempotency and retry.

---

### Analyst

| Section | Focus | Suggested elements |
|--------|--------|---------------------|
| 1 | Consumption and questions | Annotate diagram with “where I get report data”; one question for the engineer (freshness, missing data). |
| 2 | Data requests | Data request for a new source: question, fields, latency, how you’d validate once landed. |
| 3 | Report-to-pipeline map | Map report columns to Bronze/Silver/Gold; one business rule for Silver/Gold and how to verify in a report. |
| 4 | Dictionary and sanity checks | Co-author Gold data dictionary (names, definitions, caveats); one “sanity check” when new data arrives. |
| 5 | Mart requirements | Specify mart needs (dimensions, measures, grain) and one performance requirement; review storage map for “can I build my report?” |
| 6 | Reports and traceability | Build PBI and Tableau deliverables; report card; trace one visual to pipeline column and quality check. |
| 7 | Stakeholder view and questions | Own report and “data request” one-pager; present as stakeholder (question, refresh, caveat); bring real business question to roundtable. |

**Analyst-heavy activities:** Data dictionaries, data requests, report building, lineage trace (report → pipeline), business-question flow, sanity checks.

---

### Mixed-role exercises (optional)

- **Section 1:** Architect draws diagram, engineer writes spec, analyst annotates consumption and asks one question.  
- **Section 3:** Architect reviews medallion design; engineer implements; analyst maps report columns to layers and adds one business rule.  
- **Section 7:** Architect leads design and trade-offs; engineer implements and runbook; analyst owns report and presents to “stakeholders”; all participate in business-question roundtable.

---

*Use this plan as a living document: adjust depth per audience (e.g., more analytics for analysts, more ETL for engineers) and plug in your preferred tools (dbt, Airflow, Snowflake, Power BI, Tableau, etc.) in each section.*
