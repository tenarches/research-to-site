---
description: Full pipeline — deep research a topic, then build an illustrated Astro site
---
You are executing the /rts-research workflow command.

SYNOPSIS: /rts-research <topic> [| deliver to: <dir>]
PIPELINE: three stages, run by the research-to-site orchestrator under a tmux-managed
team lead: (1) deep research (minutes-scale; OKF docs + manifest.json into a run_ dir),
(2) parallel teaching-forward SVG illustration per extracted concept, (3) fast Astro/bun
site build. Observe live with `tmux attach -t <run_id>`.
REQUIRES: `factory init research-to-site` done on this machine, `~/.deep-research-agent/.env`
filled, `factory doctor` passing. If setup is incomplete, stop and tell the user what to fix.
ON SUCCESS report: research dir ($DEEP_RESEARCH_WORKSPACE/<run_id>/), site path
(.../site/dist/index.html), and the delivered path if `| deliver to:` was given.
ON FAILURE point at: <worktree>/.worker.log, <worktree>/.status.json, the tmux session
named <run_id>. A run whose site stage failed can be resumed with /rts-build-site.

Topic and options: ${@:-MISSING}

If the line above says "MISSING": do not run anything. Show the synopsis and one example
(`/rts-research WebAssembly component model | deliver to: ~/sites`), then stop.

Otherwise spawn the research-to-site subagent with exactly this prompt:
"Research and build site for: $@"
Relay its progress and final report to the user.
