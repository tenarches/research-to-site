---
description: Build (or rebuild) an Astro site from an existing research run
---
You are executing the /rts-build-site workflow command.

SYNOPSIS: /rts-build-site [<run_dir>] [| deliver to: <dir>]
WHAT IT DOES: runs only the site-builder stage (fast — no research, no tmux team).
This is NOT the command for a new research topic — that is /rts-research <topic>.
REQUIRES: ~/.deep-research-agent/.env filled, `factory doctor` passing, and an existing
research run containing manifest.json (a run without one needs /rts-research first).
ON SUCCESS report: <run_dir>/site/dist/index.html, plus the delivered copy at
<deliver_dir>/<run_id>/ if a deliver suffix or $FACTORY_DELIVER_DIR applies.
ON FAILURE point at: <run_dir>/site build output, the site-builder .status.json, and
`bun run build` errors. Re-running this command retries.

Target: ${@:-AUTO-SELECT}

If the Target above looks like a research topic (free text, not an existing directory
path): do not build. Explain that /rts-build-site takes a run directory, and that a new
topic starts with `/rts-research <topic>`. Offer to run that instead, then stop.

If the Target is "AUTO-SELECT": read ~/.deep-research-agent/runs.json and pick the most
recent run that does NOT yet have a site/dist/index.html (the retry path for a failed
site stage). Tell the user which run you selected and why before building. If every run
already has a site, show a table of runs (run_id | topic | created_at) and ask which to
rebuild. If runs.json is missing or empty, say so and suggest /rts-research.

Otherwise, spawn the site-builder subagent with exactly this prompt:
"Build site for: $@"
Relay its progress and final report to the user.
