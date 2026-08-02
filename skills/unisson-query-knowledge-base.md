---
name: Query the Unisson product knowledge base
description: >-
  Read the Explorer-maintained knowledge base - features, documented
  workflows, company knowledge, and agent insights - to answer how-to
  questions about the connected product.
api: openapi/unisson-openapi-original.json
operations:
- get_summary_api_v1_knowledge_base_summary_get
- list_features_api_v1_knowledge_base_features_get
- get_feature_api_v1_knowledge_base_features__feature_id__get
- list_workflows_api_v1_knowledge_base_workflows_get
- get_workflow_api_v1_knowledge_base_workflows__workflow_id__get
- list_company_knowledge_api_v1_knowledge_base_company_knowledge_get
- list_agent_insights_api_v1_knowledge_base_agent_insights_get
generated: '2026-07-21'
method: generated
---

# Query the Unisson product knowledge base

Authenticate with `Authorization: Bearer <token>`.

1. **Orient** — `GET /api/v1/knowledge-base/summary`
   (`get_summary_api_v1_knowledge_base_summary_get`) for KB coverage stats.
2. **Browse features** — `GET /api/v1/knowledge-base/features`
   (`list_features_api_v1_knowledge_base_features_get`), then drill in with
   `GET /api/v1/knowledge-base/features/{feature_id}`
   (`get_feature_api_v1_knowledge_base_features__feature_id__get`).
3. **Find the workflow** — `GET /api/v1/knowledge-base/workflows`
   (`list_workflows_api_v1_knowledge_base_workflows_get`) and fetch detail
   with `GET /api/v1/knowledge-base/workflows/{workflow_id}`
   (`get_workflow_api_v1_knowledge_base_workflows__workflow_id__get`).
4. **Add org context** — `GET /api/v1/knowledge-base/company-knowledge`
   (`list_company_knowledge_api_v1_knowledge_base_company_knowledge_get`)
   and `GET /api/v1/knowledge-base/agent-insights`
   (`list_agent_insights_api_v1_knowledge_base_agent_insights_get`) for
   learned insights.

Rules: treat KB content as the source of truth over stale docs; write
operations on the KB (PATCH/DELETE) exist but reserve them for curation
flows, not Q&A.
