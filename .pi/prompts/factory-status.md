## /factory-status — software factory status overview

**Synopsis:** `/factory-status`

**What it does:** Read-only snapshot of recent runs, live pipeline sessions, and available
workflow modules. Fast; nothing is launched or modified.

**Required setup:** `~/.deep-research-agent/.env` filled and `factory doctor` passing. If
`runs.json` is missing there are simply no runs yet — start one with `/rts-research`.

**Output:** concise status tables (see below). To act on what you find: `/rts-build-site`
retries a run whose site stage failed; `tmux attach -t <run_id>` inspects a live session.

Report the current status of the software factory:

1. Read ~/.deep-research-agent/runs.json — list the 5 most recent runs with:
   run_id | topic | created_at | site_built | svgs_generated

2. Check for any active tmux sessions matching the rts-* or run_* pattern:
   tmux list-sessions 2>/dev/null | grep -E '^(rts-|run_)'
   List any found with their windows and pane states.

3. List available workflow modules by scanning for directories in the software-factory
   root that contain .pi/subagents/ subdirectories. For each, show:
   module_name | available_subagents | available_slash_commands

Report as concise status tables. If any tmux sessions are running, note which workers
are active and their approximate state (RUNNING/STALLED/DONE based on pane_dead status).
