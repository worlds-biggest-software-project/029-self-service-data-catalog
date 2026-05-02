# Self-Service Data Catalog — Feature & Functionality Survey

> Candidate #29 · Researched: 2026-05-02

## Solutions Analysed

| Tool | Type | Licence / Model | URL |
|------|------|-----------------|-----|
| OpenMetadata | Open Source | Apache 2.0 | https://open-metadata.org |
| DataHub (LinkedIn / Acryl) | Open Source core + Commercial cloud | Apache 2.0 (OSS); Proprietary (Acryl Cloud) | https://datahub.com |
| Apache Atlas | Open Source | Apache 2.0 | https://atlas.apache.org |
| Amundsen (by Lyft) | Open Source | Apache 2.0 | https://www.amundsen.io |
| Alation | Commercial Enterprise | Proprietary; ~$198,000+/year | https://www.alation.com |
| Collibra | Commercial Enterprise | Proprietary; $170,000–$500,000+/year | https://www.collibra.com |
| Atlan | Commercial SaaS | Proprietary; custom enterprise pricing | https://atlan.com |
| Secoda | Commercial SaaS | Proprietary; custom (mid-market) | https://www.secoda.co |
| Select Star | Commercial SaaS (acquired by Snowflake) | Proprietary; from ~$1,000/mo | https://www.selectstar.com |

## Feature Analysis by Solution

### OpenMetadata

**Core features**
- Unified platform covering data discovery, data quality, lineage, governance, profiling, and collaboration in a single deployable package
- Column-level lineage with a no-code visual editor for manual lineage additions or corrections
- 120+ pre-built connectors for databases, data warehouses, BI tools, messaging systems, dashboards, and pipelines
- Built-in data quality tests natively integrated into the catalog (a feature rare in OSS peers)
- Business glossary management with term linking to dataset columns and assets
- Data profiling: row counts, value distributions, null percentages, and freshness tracking
- Role-based access control, domain ownership, and team-based data governance workflows
- Semantic search (released in v1.12): LLM-powered vector embeddings for natural language asset discovery using Bedrock or OpenAI models

**Differentiating features**
- Broadest out-of-box feature set among all open-source catalog tools — no bolt-on modules required
- Native data quality tests within the catalog itself, not delegated to an external tool (unique among OSS peers)
- Semantic search via vector embeddings in v1.12 provides LLM-powered discovery without requiring a separate search engine
- No-code lineage editor enables data stewards to maintain lineage without writing code
- Built by the original team behind Uber's data infrastructure and Apache Atlas founders, providing deep domain credibility

**UX patterns**
- Unified portal design; users navigate by entity type (table, pipeline, dashboard, topic)
- Markdown-rich documentation for each asset, supporting images and links for richer context
- Activity feed and collaboration features (task assignments, announcements, conversations per asset)
- Data Insights module provides organisation-level metrics on catalog coverage, KPIs, and adoption
- Complex to self-host at scale; requires MySQL/PostgreSQL + Elasticsearch; no native graph database

**Integration points**
- 120+ connectors: Snowflake, BigQuery, Redshift, Databricks, dbt, Airflow, Kafka, Looker, Tableau, Power BI, and more
- OpenLineage standard supported for pipeline lineage ingestion
- REST API and webhooks for custom integrations
- LLM integrations: OpenAI and AWS Bedrock (for semantic search embeddings)
- Managed cloud hosting available as an alternative to self-hosted deployment

**Known gaps**
- Complex operational requirements at scale (Elasticsearch, multiple services) create DevOps overhead
- UI can feel overwhelming for non-technical users given the breadth of features
- Enterprise security features (fine-grained masking, attribute-based access) lag behind Collibra and Alation
- Limited stewardship workflow automation compared to enterprise tools
- Community support quality varies; professional support requires paid managed service

**Licence / IP notes**
- Apache 2.0: permissive licence, no copyleft, patent grant included. Safe for commercial use and modification without open-sourcing derivatives. No patent encumbrances identified.

---

### DataHub (LinkedIn / Acryl)

**Core features**
- Graph-based metadata architecture (uses neo4j) enabling rich relationship traversal across the entire data estate
- End-to-end data lineage with column-level granularity and file-based lineage
- Universal search across all data assets with faceted filtering by type, owner, tag, and domain
- Real-time streaming metadata updates in seconds (not batch-based) via Kafka event architecture
- Data governance: role-based access control, tags, glossary terms, and domain-based asset grouping
- 80+ production-grade push/pull ingestion connectors (Spark, dbt, Airflow, Kafka, Flink, and more)
- Native MCP (Model Context Protocol) server and LLM integration for AI agent interoperability (2025)
- DataHub 1.0 launched January 2025, marking the platform's maturity milestone

**Differentiating features**
- Graph-based architecture (vs. OpenMetadata's relational + search approach) enables richer multi-hop lineage queries and relationship traversal
- Real-time event-driven updates via Kafka mean metadata reflects current state within seconds, not hours
- Native MCP server support positions DataHub as a data context layer for AI agents and LLM workflows
- Strong enterprise adoption by LinkedIn, Airbnb, Dropbox, and other hyperscale organisations provides production credibility
- Push and pull ingestion flexibility (not just connector-based polling)

**UX patterns**
- Search-first landing page; asset pages show schema, lineage graph, documentation, ownership, and usage statistics
- GraphQL API makes the metadata graph queryable from any application
- Acryl Cloud adds enterprise UX enhancements, automated observability, and managed upgrades
- Self-hosted deployment requires Kafka, Elasticsearch, MySQL, and neo4j — operationally complex for small teams

**Integration points**
- Kafka for real-time event ingestion; REST and GraphQL APIs for programmatic access
- 80+ connectors: Snowflake, Databricks, dbt, Airflow, Spark, BigQuery, Redshift, Tableau, and more
- OpenLineage standard supported for pipeline lineage
- MCP Server for AI agent integration (2025 feature)
- AWS Marketplace deployment option
- Acryl Cloud for fully managed enterprise hosting

**Known gaps**
- Self-hosting complexity (Kafka + neo4j + Elasticsearch + MySQL) is a significant operational burden for small teams
- Enterprise features (automated PII classification, advanced governance workflows, SLA monitoring) gated behind Acryl commercial tier
- UI is less polished than modern commercial tools (Atlan, Secoda)
- Data quality and profiling features less mature than OpenMetadata
- Stewardship workflows and policy enforcement require manual configuration

**Licence / IP notes**
- Core DataHub is Apache 2.0 (OSS); permissive, patent grant included, safe for commercial use. Acryl Cloud is fully proprietary. No patent encumbrances identified.

---

### Apache Atlas

**Core features**
- Type-and-Entity metadata model enabling custom asset type definitions across any data platform
- Column-level lineage across Hadoop-native sources (Hive, HBase, Kafka, Sqoop, Storm)
- Fine-grained access control and data masking via deep integration with Apache Ranger
- Classification and tagging system for PII, sensitivity, and regulatory labelling
- Business glossary with hierarchical term definitions and entity associations
- Comprehensive audit log for compliance and regulatory reporting
- Current stable release: v2.4.0 (January 2025); v2.5.0 adds Trino extractor and PostgreSQL backend

**Differentiating features**
- Deepest native integration with Apache Ranger for fine-grained security policies and data masking — unmatched in any other OSS catalog
- Longest-standing open-source catalog with large Hadoop ecosystem installations that cannot easily migrate
- Flexible type system allows custom metadata models for domain-specific use cases

**UX patterns**
- Dated web UI; navigation is functional but not intuitive for non-technical users
- Search is keyword-based with limited semantic capability
- Ranger integration requires separate Ranger administration expertise
- Deployment requires Hadoop ecosystem knowledge; complex for cloud-native teams

**Integration points**
- Native Hadoop integration: Hive, HBase, Kafka, Storm, Sqoop, Falcon, Oozie
- REST API for programmatic metadata access
- Apache Ranger integration for policy enforcement
- Limited modern SaaS connectors; Trino support added in v2.5.0

**Known gaps**
- Dated UI that significantly lags behind modern alternatives
- Limited cloud-native connectors for Snowflake, BigQuery, Databricks, or dbt
- Slower development pace relative to OpenMetadata and DataHub; primarily maintained for Hadoop-ecosystem users
- No LLM-powered or semantic search capability
- Weak business user experience; designed for data engineering teams, not self-service users
- Declining market adoption outside Hadoop-centric organisations

**Licence / IP notes**
- Apache 2.0: permissive, patent grant included, safe for commercial use. No patent encumbrances identified.

---

### Amundsen (by Lyft)

**Core features**
- Data discovery and metadata search focused on finding the right dataset quickly
- Social/crowd-sourced metadata: users can rate datasets (popularity), add descriptions, and tag assets
- Pagerank-style search ranking based on query frequency and downstream usage
- Table-level lineage (column-level lineage limited compared to peers)
- Neo4j graph backend for entity relationship storage
- Python-based ingestion framework supporting Hive, BigQuery, Snowflake, Airflow, and others

**Differentiating features**
- Pioneered social/crowd-sourced metadata enrichment (follower counts, usage-based ranking) — a pattern adopted by later tools
- Usage-based search ranking surfaces the most commonly used datasets first, reducing discovery friction
- Lightweight architecture relative to OpenMetadata; easier to self-host for small teams

**UX patterns**
- Search-centric landing experience; asset detail pages show description, owners, usage stats, and sample data
- Popularity and freshness signals visually prominent on asset cards
- Limited UI beyond search and discovery — no built-in quality tests, governance workflows, or documentation editor

**Integration points**
- Ingestion framework: Hive, BigQuery, Snowflake, Redshift, Airflow, dbt, and others via community extractors
- REST API for metadata access
- Neo4j + Elasticsearch backend

**Known gaps**
- Lineage coverage (especially column-level) significantly lags OpenMetadata and DataHub
- No built-in data quality or profiling capability
- Governance features (policy enforcement, stewardship workflows) are absent
- Limited LLM or semantic search capability
- Slower development pace; community contributions less active than DataHub/OpenMetadata in 2025–2026
- No managed cloud offering

**Licence / IP notes**
- Apache 2.0: permissive, patent grant included. No patent encumbrances identified.

---

### Alation

**Core features**
- AI-powered data catalog with search, trust flags, stewardship assignments, and data intelligence layers
- Data lineage from source through transformation to BI dashboard with automated impact analysis
- Compose: browser-based SQL query editor with catalog-embedded context (which tables, what quality)
- Alation Anywhere: catalog access embedded directly in tools like Tableau, Power BI, and Slack
- CDE Manager (November 2025): agentic AI suite governing Critical Data Elements for regulatory and AI compliance
- Curation Automation: AI agents that automatically curate and document data assets at scale
- Open Connector Framework for custom data source integration
- 30%+ query accuracy improvement cited for a recent AI-enhanced query feature (VentureBeat, 2025)

**Differentiating features**
- Market pioneer with deepest enterprise trust and compliance track record (banking, healthcare, insurance)
- Alation Anywhere embeds catalog intelligence natively inside BI tools and Slack — reducing context switching
- CDE Manager (2026 direction): outcome-based agentic governance that defines desired business outcomes and has AI agents operationalise them automatically
- Compose SQL editor with catalog context is a genuinely differentiated workflow integration
- Strongest approval workflow and stewardship engine among commercial catalogs

**UX patterns**
- Enterprise-grade portal with search, asset pages, governance workflows, and reporting
- Trust flags (endorsement, warning, deprecation) surface at point of use inside Compose and BI tools
- Implementation requires professional services engagement; typical 4–12 weeks to production
- Designed for data stewards, CDOs, and governance teams — not optimised for self-service analyst onboarding

**Integration points**
- 80+ connectors: Snowflake, Databricks, Teradata, Oracle, SQL Server, BigQuery, Redshift, Hive
- BI tool integrations: Tableau, Power BI, MicroStrategy, Looker
- Workflow integrations: ServiceNow, Jira, Slack, Teams
- Open Connector Framework for custom sources
- REST API and Python SDK

**Known gaps**
- Pricing ($198,000+/year minimum) excludes SMB and mid-market buyers
- 4–12 week implementation window creates a high adoption barrier
- Search quality and AI capability trail newer AI-first entrants (Atlan, Secoda)
- Self-service onboarding for individual analysts is weak; it is primarily a governance platform
- No free tier or self-hosted OSS option

**Licence / IP notes**
- Fully proprietary enterprise SaaS. No open-source components. Alation holds patents in query-based metadata enrichment (behavioural analysis of query patterns to infer metadata). Competitive products using similar query-log-mining techniques should evaluate IP risk. Standard enterprise data processor agreements apply.

---

### Collibra

**Core features**
- Unified data and AI governance platform: business glossary, data catalog, lineage, quality, workflow engine, and AI governance
- Highly configurable stewardship workflow engine for data governance policies, approval chains, and regulatory readiness
- Fine-grained RBAC, auditing, encryption, and data privacy controls architected for large enterprise data estates
- AI governance capability cataloguing, assessing, and monitoring AI models and agents across AWS, Azure, Google, and Databricks (2025–2026)
- Enterprise-scale architecture handling large numbers of assets, users, metadata events, and lineage graphs
- March 2026 GA release added enhanced data product visibility and alignment automation across teams
- Dominant in regulated industries: banking, healthcare, insurance, and pharmaceuticals

**Differentiating features**
- Most configurable stewardship workflow engine in the market — can model any governance process, policy, or approval chain
- AI governance cataloguing of ML models and agents alongside data assets (unique among enterprise catalog peers)
- Proven at hyperscale enterprise data estates where other tools struggle
- Regulatory compliance positioning (GDPR, CCPA, BCBS 239, HIPAA) is strongest in class

**UX patterns**
- Highly configurable but complex to administer; requires dedicated data governance staff
- Implementation typically takes 3–9 months with significant professional services involvement
- User interface is functional but not modern; newer entrants offer significantly better UX
- Strong role separation between data stewards, data owners, and consumers

**Integration points**
- Connectors for major cloud warehouses, on-premises databases, BI tools, and ETL/ELT platforms
- Collibra Connect: integration framework for custom connectors
- REST API for programmatic governance operations
- Integrations with AWS, Azure, GCP, and Databricks for AI governance asset cataloguing

**Known gaps**
- Price ($170,000–$500,000+/year) and implementation timeline (3–9 months) create a very high barrier to entry
- UI significantly lags modern SaaS alternatives (Atlan, Secoda) in usability
- No self-hosted OSS option
- Smaller analytics-layer asset coverage (dbt, Looker) compared to Atlan or Select Star
- Not suitable for SMB or mid-market organisations

**Licence / IP notes**
- Fully proprietary enterprise SaaS. No open-source components. Broad enterprise data governance IP portfolio; no specific patent encumbrances identified in public sources that would affect a new open-source catalog. Standard enterprise processor agreements with DPA, BAA (for HIPAA customers), and SOC 2 compliance required.

---

### Atlan

**Core features**
- Cloud-native data catalog positioning as a collaboration hub across the modern data stack
- AI agents that read SQL query history, BI semantics, and pipeline code to generate asset descriptions and link business terms automatically
- Column-level lineage parsing SQL, dbt transformation logic, and BI metadata across 100+ certified connectors
- AI-powered PII classification: identifies sensitive data types without manual tagging
- Enterprise Data Graph: unified metadata layer across Snowflake, Databricks, dbt, Tableau, Looker, and others
- Slack and Microsoft Teams integrations enabling catalog queries and governance actions from messaging tools
- Named a Leader in Gartner Magic Quadrant for Data & Analytics Governance Platforms 2026 (cited as only platform with future-proof architecture)
- Typical deployment: 4–8 weeks to full production

**Differentiating features**
- AI agents that auto-generate metadata descriptions from actual query and transformation code — addressing the blank-page adoption problem
- Slack/Teams-first access model reduces context switching for analytics teams who live in messaging tools
- 100+ certified connectors with deep semantic understanding of modern data stack tools (dbt, Snowflake, Databricks)
- Gartner Magic Quadrant Leader 2026 recognition positions it as the leading modern commercial alternative to Alation/Collibra

**UX patterns**
- Modern, consumer-grade SaaS design targeting analytics engineers and data analysts, not only governance teams
- Conversational discovery: analysts can query the catalog from Slack without visiting the portal
- Asset pages show AI-generated descriptions, usage stats, related assets, and downstream dashboards
- POC (proof of concept) deployment available; typical enterprise onboarding 4–8 weeks

**Integration points**
- 100+ certified connectors: Snowflake, Databricks, dbt, Tableau, Looker, Power BI, Fivetran, Airbyte, Airflow, and more
- Slack and Microsoft Teams for in-workflow catalog access
- REST API and Python SDK
- OpenLineage support for pipeline lineage ingestion
- Atlan Marketplace for community-built connectors

**Known gaps**
- Pricing is opaque (custom enterprise quotes only); no public SMB tier
- Proprietary lock-in; no self-hosted OSS option
- Younger product than Alation/Collibra; less mature stewardship workflow engine
- Governance workflow depth (approval chains, regulatory compliance) lags Collibra for heavily regulated industries
- AI auto-generation quality depends on query history volume; new or sparse environments yield weaker results

**Licence / IP notes**
- Fully proprietary SaaS. No open-source components. No patent encumbrances identified in public sources. Standard enterprise SaaS terms with DPA.

---

### Secoda

**Core features**
- AI-first data catalog with automated column-level lineage, NLP-powered search, and 80+ integrations
- NLP search interface translating natural language questions into catalog queries without complex syntax
- Automated metadata enrichment using LLMs to generate column descriptions from query patterns and code
- Data lineage chat: users can ask an LLM questions about column relationships, table dependencies, and impact
- Automated column- and table-level lineage tracking across connected data sources
- Data quality monitoring and metadata health scoring
- Deployment time: 1–2 weeks (compared to 3–9 months for Collibra/Alation)
- Integrations with Looker, dbt, Snowflake, BigQuery, Hightouch, Fivetran, and 80+ tools

**Differentiating features**
- Purpose-built AI-first architecture with LLM at the center, not bolted on
- Fastest deployment time in the commercial catalog market (1–2 weeks)
- Data lineage accessible via conversational chat interface — users can ask lineage questions in plain English
- Positioned specifically for mid-market teams who need enterprise features at accessible speed and cost

**UX patterns**
- Clean, modern SaaS UI targeting data engineers and analysts rather than governance specialists
- Search-first discovery with AI-powered results ranking
- Conversational lineage exploration reduces the need to navigate graph UIs
- Fast onboarding by design; minimal professional services required

**Integration points**
- 80+ integrations: Snowflake, BigQuery, Databricks, Redshift, dbt, Looker, Tableau, Fivetran, Hightouch
- Slack and Teams integration for in-workflow metadata queries
- REST API for custom integrations
- OpenLineage support

**Known gaps**
- Newer entrant with less enterprise credibility and customer reference base than Alation or Collibra
- Governance workflow depth (stewardship, approval chains, regulatory compliance) lags enterprise tools
- Data quality feature maturity trails OpenMetadata's native quality tests
- No self-hosted OSS option
- Custom pricing with no transparent tiers creates sales-cycle friction for SMB buyers

**Licence / IP notes**
- Fully proprietary SaaS. No open-source components. No patent encumbrances identified.

---

### Select Star (acquired by Snowflake)

**Core features**
- Automated data catalog focused on analytics assets: dbt models, Looker, Tableau, and SQL-based assets
- Auto-documents columns from SQL query usage patterns without requiring manual descriptions
- Column-level lineage across dbt models, BI tools, and warehouse tables
- ERDs showing how models and sources connect, with cross-platform search spanning dbt and BI tools
- Metadata sync every 24 hours to automatically pick up new and removed assets
- AWS Marketplace deployment available

**Differentiating features**
- Query-usage-based auto-documentation: generates metadata descriptions from historical SQL usage patterns — unique among analytics-layer catalogs
- Best-in-class coverage of analytics-layer assets (dbt + Looker + Tableau in one lineage graph)
- Acquisition by Snowflake (announced 2025) will integrate Select Star technology into Snowflake Horizon Catalog

**UX patterns**
- Lightweight, analytics-focused UI designed for data and analytics engineers
- Search spans dbt and BI tools in a unified index
- Minimal governance workflow features — narrowly scoped to analytics discovery and lineage

**Integration points**
- Deep dbt Cloud and dbt Core integration with column lineage
- BI tool integrations: Looker, Tableau, Mode, Sigma, Salesforce CRM Analytics
- Warehouse integrations: Snowflake, BigQuery, Redshift
- AWS Marketplace listing

**Known gaps**
- Narrow focus: not a full governance platform; PII classification, stewardship workflows, and policy enforcement are absent
- Post-Snowflake acquisition roadmap is uncertain; product may be sunsetted or merged into Horizon Catalog
- Coverage outside analytics layer (operational databases, streaming, unstructured data) is limited
- No OSS option; pricing starts at ~$1,000/mo for a focused use case

**Licence / IP notes**
- Fully proprietary SaaS; acquisition by Snowflake means future licensing terms may change. No patent encumbrances identified. Buyers should evaluate Snowflake-only lock-in risk given the acquisition trajectory.

---

## Cross-Cutting Feature Themes

### Table-Stakes Features
- Asset discovery and search across tables, columns, dashboards, and pipelines
- Table-level lineage from source to consumption (column-level is rapidly becoming standard)
- Business glossary and data dictionary with asset-to-term linkage
- Ownership and stewardship assignment per asset
- Basic access control (role-based permissions on catalog metadata)
- Integration with at least one major cloud warehouse (Snowflake, BigQuery, Databricks)
- REST API for programmatic metadata ingestion and access
- Freshness and last-updated timestamps per asset

### Differentiating Features
- Column-level lineage with visual graph exploration
- AI-generated metadata descriptions from query logs, dbt code, or schema context (eliminating blank-page adoption problem)
- Natural language / semantic search powered by LLM embeddings
- Native data quality tests within the catalog (OpenMetadata-style)
- PII / sensitive data classification without manual tagging (AI-driven)
- Conversational lineage exploration via chat interface (Secoda, DataHub MCP)
- Slack/Teams embedded access reducing context switching
- Governance workflow engine for stewardship, approval chains, and regulatory policy
- AI governance: cataloguing ML models and agents alongside data assets (Collibra 2025)

### Underserved Areas / Opportunities
- LLM-generated column descriptions and dataset summaries from SQL history and dbt code — eliminating manual metadata entry (the single biggest adoption blocker for all catalog tools)
- Semantic natural language search allowing analysts to ask "which dataset has customer revenue by region for EMEA?" without knowing asset names
- AI-powered data quality scoring that infers expected value distributions and flags anomalies without explicit rule authoring
- Conversational governance assistant answering compliance questions ("where is our PII stored?") and generating audit reports automatically
- Low-friction deployment (Docker Compose or managed free tier) targeting SMB and mid-market organisations priced out of Alation/Collibra and unable to operate OpenMetadata/DataHub at scale

### AI-Augmentation Candidates
- Automated metadata generation from SQL query history, dbt model code, and transformation logic
- LLM-powered semantic search with context-aware result ranking
- AI-driven PII entity recognition applied to ingested schemas and sample data
- Automated quality rule inference from historical data distributions (replacing manual rule authoring)
- Conversational governance assistant for compliance Q&A and audit report generation
- Auto-linking of business glossary terms to discovered columns based on semantic similarity

---

## Legal & IP Summary

All four open-source tools (OpenMetadata, DataHub, Apache Atlas, Amundsen) are licensed under Apache 2.0, which is permissive, includes an explicit patent grant, and does not require derivatives to be open-sourced. This makes all four safe to use as components of a commercial product. Alation holds published patents in query-log-based metadata inference; any product that mines SQL query logs to auto-generate metadata should conduct an independent patent freedom-to-operate analysis before commercialisation. All commercial tools (Alation, Collibra, Atlan, Secoda, Select Star) are fully proprietary; incorporating their code or substantially reproducing their UX would be a copyright concern, but building functionally similar open-source software is not. The Snowflake acquisition of Select Star creates platform lock-in risk for customers but no IP concern for a competing product. No FRAND-encumbered standards were identified; W3C DCAT v3 and OpenLineage are both royalty-free standards.

---

## Recommended Feature Scope

**Must-have (MVP)**:
- Connect to at least two modern data sources (Snowflake, BigQuery, or Databricks + dbt) via automated ingestion with schema and column metadata
- Unified search across all catalogued assets with freshness, ownership, and usage signals
- Table- and column-level lineage visualisation
- Business glossary with asset-to-term linkage and column annotations
- Basic role-based access control and ownership assignment
- Docker Compose or low-friction deployment targeting small data teams without dedicated platform engineers

**Should-have (v1.1)**:
- AI-generated column descriptions and dataset summaries from SQL query history and dbt model code (eliminating blank-page adoption problem)
- LLM-powered semantic search enabling natural language queries ("which table has EMEA revenue by customer?")
- Automated PII / sensitive data classification using LLM entity recognition on ingested schemas
- Data quality scoring with anomaly detection inferred from historical data distributions (no manual rule authoring)
- Slack / Teams integration for in-workflow metadata queries and governance actions

**Nice-to-have (backlog)**:
- Conversational governance assistant for compliance Q&A ("where is our PII stored?") and automated audit report generation
- Governance workflow engine for stewardship assignments, approval chains, and policy enforcement
- AI governance: cataloguing of ML models and agents alongside data assets
- OpenLineage standard ingestion for pipeline lineage from Airflow, Spark, and Flink
- Managed SaaS free tier to capture SMB and mid-market segment currently using spreadsheets or nothing
