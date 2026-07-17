## /rts-list-runs — list all research runs

**Synopsis:** `/rts-list-runs`

**What it does:** Read-only listing of every research run recorded in
`~/.deep-research-agent/runs.json`. Fast; no pipeline stages run.

**Required setup:** `~/.deep-research-agent/.env` filled (for `$DEEP_RESEARCH_WORKSPACE`).
If `runs.json` is missing, there are no runs yet — start one with `/rts-research`.

**Output:** a table of runs. To build a site for a listed run, use `/rts-build-site <run_dir>`.

Read ~/.deep-research-agent/runs.json and display a table of all research runs:

| run_id | topic | created_at | site_built |
|--------|-------|------------|------------|

- site_built: yes if <run_dir>/site/dist/index.html exists, no otherwise
- Sort by created_at descending (newest first)
- If runs.json does not exist or is empty, say so clearly
