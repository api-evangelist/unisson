---
name: Trigger and monitor a Unisson agent run from your own tool
description: >-
  Use the external Runner API to start a Unisson agent run from a
  third-party system, poll or receive webhook callbacks for its progress,
  and resume it when it pauses for input.
api: openapi/unisson-openapi-original.json
operations:
- external_status_api_v1_external_status_get
- configure_webhook_api_v1_external_webhook_put
- create_external_run_api_v1_external_runs_post
- get_external_run_api_v1_external_runs__run_id__get
- resume_external_run_api_v1_external_runs__run_id__resume_post
generated: '2026-07-21'
method: generated
---

# Trigger and monitor a Unisson agent run from your own tool

Authenticate every call with `Authorization: Bearer <token>` (organization
API keys are created at `POST /api/v1/organizations/me/api-keys`).

1. **Check the external surface is live** — `GET /api/v1/external/status`
   (`external_status_api_v1_external_status_get`).
2. **Register your callback once** — `PUT /api/v1/external/webhook`
   (`configure_webhook_api_v1_external_webhook_put`) with the HTTPS URL that
   should receive run-event callbacks. Skip this if you prefer polling.
3. **Start the run** — `POST /api/v1/external/runs`
   (`create_external_run_api_v1_external_runs_post`) with the task for the
   agent. Capture `run_id` from the response.
4. **Track progress** — poll `GET /api/v1/external/runs/{run_id}`
   (`get_external_run_api_v1_external_runs__run_id__get`) or wait for your
   webhook to fire.
5. **Resume when paused** — if the run pauses for confirmation or input,
   `POST /api/v1/external/runs/{run_id}/resume`
   (`resume_external_run_api_v1_external_runs__run_id__resume_post`).

Rules: expect FastAPI `422` validation errors (`detail[].loc/msg/type`);
there is no idempotency-key contract, so de-duplicate run creation on your
side; the API is versioned in the URI path (`/api/v1/`).
