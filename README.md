# Data Pipelines Masterclass

End-to-end course plan for building and running data pipelines—from ingestion and ETL to storage and analytics.

## What’s in this repo

- **[course/](./course/)** — Interactive HTML course: open **`course/index.html`** in a browser. Welcome page + 22 modules in 7 sections, quizzes, role callouts. No vendor-specific content.
- **[COURSE-PLAN.md](./COURSE-PLAN.md)** — Full curriculum with:
  - **7 sections:** Introduction → Ingestion → ETL (medallion) → Data Management → Storage → Analytics (Power BI & Tableau) → Capstone & simulation
  - **Progressive depth:** Basics → ramp-up in every chapter
  - **Section use cases:** A concrete “dummy” use case at the end of each section
  - **Practical use cases & interactivity:** Per-chapter use cases and suggested interactive elements (polls, labs, role-play, peer review, etc.)
  - **Holistic wrap-up:** Capstone project, failure/recovery simulation, and “business question to answer” flow

## Section overview

| # | Section | Emphasis |
|---|--------|----------|
| 1 | Introduction & purpose | What pipelines are, why they matter, roles |
| 2 | Data ingestion | Batch vs. stream, connectors, APIs, reliability |
| 3 | ETL & medallion | Bronze → Silver → Gold, incremental, SCD |
| 4 | Data management | Engineering practices, cleaning, staging, quality |
| 5 | Storage | Warehouses, lakes, marts, cubes |
| 6 | Analytics | Power BI and Tableau (model, DAX/calcs, dashboards) |
| 7 | Capstone & simulation | Full pipeline project, failure scenarios, holistic view |

## How to use the plan

- **Instructors:** Use section/chapter outlines for sequencing; plug in your tools (dbt, Airflow, Snowflake, Power BI, Tableau, etc.) and adjust session count to your format.
- **Learners:** Follow section order; do each section use case before moving on; use the appendix for “section → use case” and “interactive element” reference.
- **Curriculum designers:** Copy or adapt chapters; the appendix includes a rough duration guide (e.g., 18–25 sessions).

## License & use

This course plan is provided as a reference structure. Adapt and extend it for your organization or training program.
