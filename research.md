# Self-Service Data Catalog

> Candidate #29 · Researched: 2026-05-01

## Existing Products and Software Packages

| Tool | Description | Type | Pricing | Strengths / Weaknesses |
|---|---|---|---|---|
| **OpenMetadata** | Unified open-source metadata platform covering discovery, governance, quality, profiling, lineage, and collaboration in a single package; uses MySQL/PostgreSQL + Elasticsearch (no graph DB) | Open Source (Apache 2.0) | Free self-hosted; managed cloud available | Richest out-of-box feature set in open source; built-in data quality tests unique among OSS peers; complex to operate at scale |
| **DataHub (LinkedIn / Acryl)** | Originally LinkedIn's WhereHows, now a widely adopted open-source metadata graph; Acryl Data commercializes it | Open Source core (Apache 2.0); Acryl commercial | OSS free; Acryl Cloud from ~$2,000/mo+ (quote-based) | Strong graph-based lineage, active community, DataHub 1.0 launched Jan 2025; enterprise features gated behind Acryl |
| **Apache Atlas** | Apache project for Hadoop ecosystem metadata governance; deep integration with Apache Ranger for fine-grained security and data masking | Open Source (Apache 2.0) | Free self-hosted | Dominant in Hadoop/on-prem environments; dated UI, poor cloud-native story, limited active development |
| **Amundsen (by Lyft)** | Open-source data discovery and metadata engine focused on search and exploration; contributed by Lyft | Open Source (Apache 2.0) | Free self-hosted | Pioneered social/crowd-sourced metadata; relatively limited lineage and governance vs. newer peers |
| **Alation** | Enterprise data catalog with strong data intelligence, governance workflows, and query building; targets regulated industries | Commercial (Enterprise) | ~$198,000+/year minimum; user-license packs drive cost up | Market pioneer, strong enterprise trust; very expensive, 4–12 week implementation, not SMB-friendly |
| **Collibra** | Data governance and catalog platform dominant in banking, healthcare, and insurance; most configurable stewardship workflows | Commercial (Enterprise) | $170,000–$500,000+/year; often 2–3x Atlan pricing for comparable users | Best-in-class regulatory compliance; 3–9 month implementation time, prohibitively expensive for most orgs |
| **Atlan** | Modern cloud-native data catalog positioning itself between open-source flexibility and Collibra/Alation cost; strong Slack/Teams integrations | Commercial (SaaS) | Custom enterprise pricing; POC available; typically less than Collibra | Fast-growing, modern UX, 4–12 week setup; pricing still opaque, proprietary lock-in |
| **Secoda** | AI-first data catalog and governance platform with automated column-level lineage, NL search, and 80+ integrations | Commercial (SaaS) | Custom (quote-based); targets mid-market | Strong AI/NLP layer, fast to implement; newer entrant with less enterprise credibility than Alation |
| **OvalEdge** | Data catalog with governance, quality, and lineage; positions as cost-effective Collibra alternative | Commercial (SaaS/On-prem) | Quote-based; published pricing guide suggests $50K–$150K/year range | More affordable enterprise option; smaller ecosystem and community vs. leaders |
| **Select Star** | Automated data catalog focused on analytics assets (dbt, Looker, Tableau); auto-documents columns from query usage patterns | Commercial (SaaS) | Starts ~$1,000/mo; custom Enterprise | Excellent for analytics-layer cataloging; narrow focus, not a full governance platform |

## Relevant Industry Standards or Protocols

- **W3C DCAT v3 (Data Catalog Vocabulary)** — RDF vocabulary for publishing and interlinking data catalogs on the web; DCAT 3 (latest W3C Recommendation) is the foundational interoperability standard; DCAT-US 3.0 aligns with it for US government open data.
- **ISO/IEC 11179** — International standard for metadata registries (MDR), defining the structure for representing, naming, defining, and registering metadata elements; Part 1 (Framework) updated 2023.
- **FAIR Principles (Findable, Accessible, Interoperable, Reusable)** — Widely adopted data management principles from Wilkinson et al. (2016, *Nature Scientific Data*); DCAT 3 explicitly aligns with FAIR; used as an evaluation framework for catalog completeness.
- **Dublin Core Metadata Initiative (DCMI)** — Foundational vocabulary for dataset description; embedded within DCAT and used by most catalog tools for core property definitions.
- **OpenLineage (Linux Foundation)** — Open standard for collecting lineage metadata from data pipelines (Airflow, Spark, dbt, etc.) via a common API; increasingly adopted as the integration layer for lineage ingestion.
- **GDPR / CCPA Data Governance Requirements** — Regulatory frameworks that mandate data discovery, classification of personal data, and lineage traceability; primary compliance driver for enterprise data catalog adoption.
- **dbt Semantic Layer** — De facto standard for metric definition in modern analytics stacks; catalog tools increasingly must integrate with dbt's semantic layer to reflect business-level data definitions.

## Available Research Materials

1. Wilkinson, M.D. et al. (2016). *The FAIR Guiding Principles for Scientific Data Management and Stewardship.* Scientific Data (Nature). https://www.nature.com/articles/sdata201618 — Seminal peer-reviewed paper establishing FAIR; foundational to all modern data catalog governance rationale.

2. Devaraju, A. et al. (2024). *The W3C Data Catalog Vocabulary, Version 2: Rationale, Design Principles, and Uptake.* Data Intelligence (MIT Press), 6(2), 457. https://direct.mit.edu/dint/article/6/2/457/118751 — Peer-reviewed analysis of DCAT adoption patterns and design decisions.

3. ISO (2023). *ISO/IEC 11179-1:2023 — Information Technology: Metadata Registries (MDR), Part 1: Framework.* ISO Standard. https://www.iso.org/standard/78914.html — Normative standard for metadata registry structure; updated 2023.

4. TheDataGuy (2025). *Open-Source Data Governance Frameworks: A Strategic Analysis of OpenMetadata, DataHub, Apache Atlas, and Amundsen.* TheDataGuy.pro. https://thedataguy.pro/blog/2025/08/open-source-data-governance-frameworks/ — Practitioner-authored comparative technical analysis of OSS catalog architectures.

5. Atlan (2026). *Alation vs. Collibra vs. Informatica vs. Atlan: How to Choose in 2026.* Atlan Blog. https://atlan.com/alation-vs-collibra-vs-informatica-vs-atlan/ — Vendor-authored but detailed feature matrix comparison; note vendor bias toward Atlan.

6. OvalEdge (2026). *Data Catalog Pricing Guide 2026: Costs, Models & Key Factors.* OvalEdge Blog. https://www.ovaledge.com/blog/data-catalog-pricing-guide — Independent pricing analysis with market-sourced cost ranges; useful for budget benchmarking.

7. Coalesce (2025). *The AI-Powered Data Catalog Revolution.* Coalesce Blog. https://coalesce.io/data-insights/the-ai-powered-data-catalog-revolution/ — Practitioner overview of LLM-assisted metadata enrichment patterns emerging in 2025.

8. Atlan (2026). *Top 5 Open Source Data Catalog Tools.* Atlan Blog. https://atlan.com/open-source-data-catalog-tools/ — Comparative overview of OSS options; vendor-authored but factually grounded.

## Market Research

**Market Size:**
- The global data catalog market was valued at approximately $1.38 billion in 2025, growing to ~$1.72 billion in 2026 (InsightAce Analytic).
- A separate estimate (Research Nester) places 2025 at $2.47 billion, projecting $9.77 billion by 2032 at a 21.7% CAGR.
- A third estimate (InsightAce) projects $12.32 billion by 2035 at a 21.9% CAGR from a $2.04 billion 2026 base.
- Note: estimates diverge significantly across research firms; the 20–22% CAGR consensus is more reliable than absolute values. The market is growing fast driven by data governance regulation and AI readiness requirements.

**Pricing Landscape:**

| Segment | Representative Tools | Price Range |
|---|---|---|
| Open Source (self-hosted) | OpenMetadata, DataHub, Apache Atlas, Amundsen | $0 license + infrastructure + engineering labor |
| SMB / Analytics-layer | Select Star, Secoda | $1,000–$5,000/mo |
| Mid-market commercial | Atlan, OvalEdge | $50,000–$150,000/year |
| Enterprise | Alation | $198,000+/year |
| Large Enterprise | Collibra, Informatica | $170,000–$500,000+/year |

**Key Buyer Personas:**
- **Data Engineers / Platform Teams** — want self-service cataloging that auto-ingests metadata from pipelines without manual tagging; OSS-friendly.
- **Data Analysts / Scientists** — need fast asset discovery (find "the right table") and confidence in data quality/freshness before using a dataset.
- **Chief Data Officer (CDO) / Data Governance Lead** — driven by GDPR/CCPA compliance, audit readiness, and PII classification; willing to pay enterprise pricing.
- **BI/Analytics Managers** — want lineage from source to dashboard to debug broken reports without hunting through pipeline logs.

**Notable Acquisitions / Funding:**
- Acryl Data (commercial DataHub) raised Series B in 2023; one of the better-funded OSS catalog commercialization plays.
- DataHub celebrated its 5-year anniversary and launched DataHub 1.0 in January 2025, signaling maturity.
- Enterprise pricing at Collibra and Alation ($170K–$500K+/year) creates a significant market gap for a credible open-source alternative with modern UX.

## AI-Native Opportunity

- **Automated metadata generation from code and queries:** Manual metadata entry is the single biggest adoption blocker for all catalog tools. An AI-native catalog could use LLMs to generate column descriptions, dataset summaries, and business glossary mappings directly from SQL query history, dbt model code, and transformation logic — eliminating the "blank page" problem that kills catalog adoption.

- **Natural language data discovery:** Current catalogs require users to know what they are searching for (keyword or filter-based). An LLM-powered semantic search layer would let analysts ask "which dataset has customer revenue by region for EMEA?" and receive ranked, context-aware results — a fundamentally different UX that OSS tools currently do not deliver out of the box.

- **AI-powered data quality scoring:** Existing quality frameworks (e.g., Great Expectations, dbt tests) require explicit rule authoring. An AI-native catalog could learn expected value distributions, format patterns, and referential integrity rules from historical data and flag anomalies automatically — reducing the configuration burden from hundreds of manual rules to near-zero.

- **Conversational governance assistant:** Compliance teams answering "where is our PII stored?" or "what systems touch this customer table?" currently run manual audits. An AI agent with catalog access could answer these questions instantly, generate audit-ready reports, and proactively surface new PII detected via entity recognition on ingested schemas.

- **Underserved segment — SMB and mid-market:** Enterprise catalogs (Collibra, Alation) are priced out of reach for most organizations. Open-source alternatives (OpenMetadata, DataHub) require significant engineering investment. An open-source AI-native catalog with a low-friction deployment model (Docker Compose or managed SaaS free tier) and AI-assisted onboarding could capture a large underserved segment that currently uses spreadsheets or nothing.
