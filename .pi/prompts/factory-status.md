---
description: Software factory status — runs, live sessions, installed modules
---
You are executing the /factory-status workflow command.

SYNOPSIS: /factory-status
WHAT IT DOES: read-only snapshot of recent runs, live pipeline sessions, and installed
workflow modules. Fast; nothing is launched or modified.
TO ACT ON FINDINGS: /rts-build-site retries a run whose site stage failed;
`tmux attach -t <run_id>` inspects a live session.

Report the current status of the software factory:

1. Read ~/.deep-research-agent/runs.json — list the 5 most recent runs with:
   run_id | topic | created_at | site_built | svgs_generated

2. Check for any active tmux sessions matching the rts-* or run_* pattern:
   tmux list-sessions 2>/dev/null | grep -E '^(rts-|run_)'
   List any found with their windows and pane states.

3. List installed workflow modules: scan ~/.factory/modules/*/module.yaml (git-installed)
   plus any module.yaml directories in the current project tree. For each, show:
   module_name | available_subagents | available_slash_commands

Report as concise status tables. If any tmux sessions are running, note which workers
are active and their approximate state (RUNNING/STALLED/DONE based on pane_dead status).
