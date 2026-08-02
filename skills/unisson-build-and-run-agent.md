---
name: Build a Unisson agent and run it
description: >-
  Create a Unisson agent (from a natural-language description or from
  scratch), trigger a run, and monitor it through completion or
  cancellation.
api: openapi/unisson-openapi-original.json
operations:
- generate_agent_from_description_api_v1_agents_generate_from_description_post
- create_agent_api_v1_agents_post
- list_agents_api_v1_agents_get
- trigger_run_api_v1_runs_trigger_post
- get_run_api_v1_runs__run_id__get
- get_run_steps_api_v1_runs__run_id__steps_get
- cancel_run_api_v1_runs__run_id__cancel_post
generated: '2026-07-21'
method: generated
---

# Build a Unisson agent and run it

Authenticate with `Authorization: Bearer <token>`.

1. **Draft the agent** — `POST /api/v1/agents/generate-from-description`
   (`generate_agent_from_description_api_v1_agents_generate_from_description_post`)
   with a plain-language description of the job, or create one directly with
   `POST /api/v1/agents` (`create_agent_api_v1_agents_post`).
2. **Confirm it exists** — `GET /api/v1/agents`
   (`list_agents_api_v1_agents_get`) and note the `agent_id`.
3. **Trigger a run** — `POST /api/v1/runs/trigger`
   (`trigger_run_api_v1_runs_trigger_post`) referencing the agent.
4. **Watch it work** — `GET /api/v1/runs/{run_id}`
   (`get_run_api_v1_runs__run_id__get`) for status, and
   `GET /api/v1/runs/{run_id}/steps`
   (`get_run_steps_api_v1_runs__run_id__steps_get`) for step-by-step detail.
5. **Stop if needed** — `POST /api/v1/runs/{run_id}/cancel`
   (`cancel_run_api_v1_runs__run_id__cancel_post`).

Rules: runs can spawn child runs (`GET /api/v1/runs/{run_id}/children`);
handle `422` HTTPValidationError envelopes; no idempotency keys — guard
against duplicate triggers yourself.
