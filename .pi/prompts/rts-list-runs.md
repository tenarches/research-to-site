---
description: List all research runs with site build status
---
You are executing the /rts-list-runs workflow command.

SYNOPSIS: /rts-list-runs
WHAT IT DOES: read-only listing of every research run recorded in
~/.deep-research-agent/runs.json. Fast; nothing is launched or modified.
NOTE: runs.json entries store run_dir relative to the workspace root when
"workspace_rel" is true — resolve them against $DEEP_RESEARCH_WORKSPACE
(from ~/.deep-research-agent/.env).

Read ~/.deep-research-agent/runs.json and display a table of all research runs:

| run_id | topic | created_at | site_built |
|--------|-------|------------|------------|

- site_built: yes if <resolved run_dir>/site/dist/index.html exists, no otherwise
- Sort by created_at descending (newest first)
- If runs.json does not exist or is empty, say so clearly and suggest /rts-research
- End with: "Build a site for any run with /rts-build-site <run_dir>"
