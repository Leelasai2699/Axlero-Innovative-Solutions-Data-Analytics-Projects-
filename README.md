Project -1: Metrics Mind
we are going to build and deploy AI powered BI (Business intelligence) System where the company manager when asks business questions in Natural English language, AI should use semantic layer to retrieve business metric terms where we define the rules of the company in it, analyze the data and return the answer with proper valid explanation and visualization.

- Create company (synthetic) data
- store the data in datawarehouse(snowflake - a cloud based software platform to store data)
- clean & organize the data
- create semantic layer (business rule book to AI)
- connect AI to semantic layer 
- Build the chat interface & charts
- Test

# MetricMind: Agentic Semantic BI Engine

## 1. Project Overview
MetricMind is a business intelligence analytics project built for NovaMart Global, a fictional multinational e-commerce company. It transforms raw sales data into governed business metrics to support consistent, data-driven decisions.

## 2. Technology Stack
- **Snowflake:** Cloud data warehouse and SQL analytics
- **dbt:** Data transformation and metric modeling
- **SQL:** Business-question analysis

## 3. Data Pipeline
CSV datasets → Snowflake RAW tables → dbt staging models → `mart_metricmind` → `semantic_metrics` → business-question SQL queries.

## 4. Key Business Metrics
Validated against 10,000 transactions:
- **Total Revenue:** 6,470,555.19
- **Total Profit:** 1,578,893.49
- **Overall Profit Margin:** 24.40%

## 5. Business Questions
1. Which regions generate the most revenue?
2. Which product categories have the highest profit margin?
3. Which quarter generated the most profit?

The SQL queries are documented in `MetricMind_Business_Questions.sql`.

## 6. Project Files
- `data/` — Source CSV datasets
- `snowflake/` — Snowflake-related project files
- `models/semantic_metrics.sql` — Governed metric aggregation model
- `MetricMind_Business_Questions.sql` — Business analysis queries

## 7. Current Status and Limitations
The Snowflake data pipeline, dbt transformations, aggregate metric model, and three business analyses have been implemented and tested.

**Remaining scope:** The natural-language AI agent, interactive chat interface, dynamic visualizations, and additional governance features from the original project brief have not yet been implemented. The current deliverable is an analytics MVP, not a complete agentic BI engine.
