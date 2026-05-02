# Self-Service Data Catalog

**Status:** Candidate Project  
**Market Size:** $1.38B (2025) → $12.32B (2035) at 21.9% CAGR  
**Last Updated:** 2026-05-02

## Overview

An AI-native, open-source data catalog platform that moves from *manual metadata entry* (the single biggest adoption blocker) to *automatic metadata generation from code and usage patterns*. Today's catalogs require teams to write detailed descriptions and map business glossary terms—a time-consuming process that kills adoption. This project automates metadata generation:

- **LLM-generated column descriptions** from SQL query history, dbt model code, and schema context
- **Natural language data discovery:** "Which dataset has customer revenue by region for EMEA?"—no need to know asset names
- **AI-powered PII/sensitive data classification** without manual tagging via LLM entity recognition
- **Automated data quality scoring** inferred from historical distributions (no manual rule authoring)
- **Conversational governance assistant** answering compliance Q&A and generating audit reports

## The Market Gap

The data catalog market is bifurcated:

1. **Enterprise ($170K–$500K+/yr):** Collibra, Alation—mature but prohibitively expensive; 3–9 month implementations
2. **Open-source (free):** OpenMetadata, DataHub, Apache Atlas—powerful but operational burden; 10–20 person teams can operate
3. **Modern SaaS ($50K–$200K/yr):** Atlan, Secoda—fast deployment (1–8 weeks) but proprietary lock-in and expensive for mid-market

**The gap:** No tool solves the *blank page adoption problem*. Even free open-source catalogs fail because teams lack time to document every asset. Teams want:
- Automatic metadata generation (eliminates manual documentation)
- Low-friction deployment (Docker Compose, not Kubernetes clusters)
- SMB/mid-market pricing ($0–$10K/yr, not $170K+)
- Natural language discovery (not keyword search)

## Core Features

### MVP (Must-Have)
- Connect to at least two modern data sources (Snowflake, BigQuery, Databricks + dbt) via automated ingestion with schema and column metadata
- Unified search across all catalogued assets with freshness, ownership, and usage signals
- Table- and column-level lineage visualisation
- Business glossary with asset-to-term linkage and column annotations
- Basic role-based access control and ownership assignment
- Docker Compose or low-friction deployment targeting small data teams without dedicated platform engineers

### Should-Have (v1.1)
- **AI-generated column descriptions and dataset summaries** from SQL query history and dbt model code (eliminates blank-page adoption problem)
- **LLM-powered semantic search** enabling natural language queries ("which table has EMEA revenue by customer?")
- **Automated PII / sensitive data classification** using LLM entity recognition on ingested schemas
- **Data quality scoring** with anomaly detection inferred from historical data distributions (no manual rule authoring)
- Slack / Teams integration for in-workflow metadata queries and governance actions

### Nice-to-Have (Backlog)
- **Conversational governance assistant** for compliance Q&A ("where is our PII stored?") and automated audit report generation
- Governance workflow engine for stewardship assignments, approval chains, and policy enforcement
- AI governance: cataloguing ML models and agents alongside data assets
- OpenLineage standard ingestion for pipeline lineage from Airflow, Spark, Flink
- Managed SaaS free tier to capture SMB and mid-market segment currently using spreadsheets

## AI-Native Opportunities

1. **Automated metadata generation from code and queries**
   - Manual metadata entry is the single biggest adoption blocker for all catalog tools
   - An AI-native catalog could use LLMs to generate column descriptions, dataset summaries, and business glossary mappings directly from SQL query history, dbt model code, and transformation logic
   - Eliminates the "blank page" problem that kills catalog adoption

2. **Natural language data discovery**
   - Current catalogs require users to know what they're searching for (keyword or filter-based)
   - An LLM-powered semantic search layer lets analysts ask "which dataset has customer revenue by region for EMEA?" and receive ranked, context-aware results
   - Fundamentally different UX; no open-source tool offers this out of the box

3. **AI-powered data quality scoring**
   - Existing quality frameworks (Great Expectations, dbt tests) require explicit rule authoring
   - An AI-native catalog could learn expected value distributions, format patterns, and referential integrity rules from historical data and flag anomalies automatically
   - Reduces configuration burden from hundreds of manual rules to near-zero

4. **Conversational governance assistant**
   - Compliance teams answering "where is our PII stored?" or "what systems touch this customer table?" currently run manual audits
   - An AI agent with catalog access could answer questions instantly, generate audit-ready reports, and proactively surface new PII detected via entity recognition on ingested schemas

5. **Underserved segment — SMB and mid-market**
   - Enterprise catalogs (Collibra, Alation) are priced out of reach for most organisations
   - Open-source alternatives (OpenMetadata, DataHub) require significant engineering investment
   - An open-source AI-native catalog with low-friction deployment and AI-assisted onboarding could capture the large underserved segment currently using spreadsheets

## Competitive Landscape

| Tool | Type | Auto Metadata | NL Search | PII Detection | Data Quality | Cost | Self-Hosted |
|------|------|---------------|-----------|---------------|-------------|------|-------------|
| **OpenMetadata** | OSS | ❌ | Semantic v1.12 | ❌ | ✓ (native tests) | Free | ✓ (complex) |
| **DataHub** | OSS | ❌ | ❌ | ❌ | ❌ | Free | ✓ (complex) |
| **Atlan** | Commercial SaaS | ✓ (AI agents) | ✓ | ✓ (AI-driven) | ❌ | Custom (mid-market) | Limited |
| **Secoda** | Commercial SaaS | ✓ (LLM) | ✓ (NLP search) | ❌ | Partial | Custom (mid-market) | ❌ |
| **Collibra** | Commercial Enterprise | ❌ | ❌ | Partial | ❌ | $170K–$500K+/yr | Limited |
| **Alation** | Commercial Enterprise | ❌ | ❌ | ❌ | ❌ | $198K+/yr | Limited |
| **This Project** | OSS + SaaS | ✓ (AI-native) | ✓ (NL+semantic) | ✓ (LLM-driven) | ✓ (AI-inferred) | Free self-hosted | ✓ |

## Technical Design Considerations

- **Connectors:** Start with Snowflake, BigQuery, Databricks; add Redshift, PostgreSQL, dbt Cloud
- **Metadata ingestion:** Automated schema import with support for column statistics and sample data
- **Lineage:** dbt integration for transformation lineage; optional OpenLineage standard support for Airflow/Spark
- **AI layer:** Claude API for description generation from SQL/dbt code; LLM embeddings for semantic search; entity recognition for PII detection
- **Data quality:** Learn distributions from historical data; flag outliers, schema changes, freshness issues
- **Governance:** Simple RBAC per asset; optional policy engine for approval workflows (v1.1+)
- **Deployment:** Docker Compose for self-hosted; managed SaaS with single-sign-on and team collaboration

## Market Validation

- **Market drivers:**
  - DataHub 1.0 launch (Jan 2025) signaling maturity of open-source catalogs
  - GDPR/CCPA compliance requirements driving data discovery and PII classification demand
  - AI readiness initiatives requiring data catalog as foundational infrastructure

- **Customer personas:**
  - Data engineers / platform teams wanting self-service cataloging that auto-ingests metadata
  - Data analysts / scientists needing fast asset discovery and confidence in data quality
  - CDO / data governance leads driven by GDPR/CCPA compliance and audit readiness
  - BI/analytics managers debugging broken reports via lineage without hunting logs

## Why Build This

1. **Market timing:** DataHub 1.0 maturity + GDPR/CCPA enforcement + AI readiness converge in 2025–2026
2. **Technology maturity:** LLM-based metadata generation is proven (Atlan, Secoda); open-source gap is clear
3. **Adoption blocker solved:** Automatic metadata generation eliminates blank-page problem that kills catalog adoption
4. **Underserved segment:** SMB and mid-market priced out of enterprise tools; open-source alternatives too complex
5. **Platform leverage:** Claude API for descriptions/discovery; existing connectors from OpenMetadata/DataHub

## Success Metrics

- **Adoption:** 1K+ GitHub stars within 12 months; featured as DataHub/OpenMetadata alternative for SMB/mid-market
- **Metadata coverage:** Auto-generate descriptions for 80%+ of columns without manual tagging
- **Commercial:** Win 25+ SMB/mid-market customers with managed SaaS tier ($500–$5K/mo)
- **Deployment time:** <30 minutes to first asset indexed (vs. weeks for enterprise tools)
- **Community:** Active issue triage; 3+ contributors beyond core team

---

**Resources:**
- [OpenMetadata Documentation](https://docs.open-metadata.org/)
- [DataHub Documentation](https://datahub.io/)
- [dbt Semantic Layer](https://docs.getdbt.com/docs/use-cases/metrics/overview)
- [W3C DCAT Vocabulary](https://www.w3.org/TR/vocab-dcat-3/)
- [FAIR Data Principles](https://www.nature.com/articles/sdata201618)
