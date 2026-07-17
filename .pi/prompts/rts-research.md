{{#if args}}
Research and build site for: {{args}}
{{else}}
## /rts-research — deep research → teaching-forward Astro site

**Synopsis:** `/rts-research <topic> [| deliver to: <dir>]`

**What it does:** Runs the full three-stage pipeline via the research-to-site orchestrator:
1. Deep research (deep-researcher) — minutes-scale; runs deep-research-agent headless and
   emits OKF documents + manifest.json into a run_ dir.
2. SVG illustration (svg-illustrator) — a parallel batch, one worker per extracted concept.
3. Site build (site-builder) — fast Astro/bun/Vite build of a static site.
The optional `| deliver to: <dir>` suffix copies the built site to `<dir>/<run_id>/`.

**Required setup (run once per machine):**
- `factory init research-to-site` — initializes the workspace git repo and installs the module.
- Fill `~/.deep-research-agent/.env` with your infra endpoints and paths.
- Verify with `factory doctor`. If it reports missing binaries/env, fix those before running.

**Success outputs:**
- Research: `$DEEP_RESEARCH_WORKSPACE/<run_id>/` (OKF .md docs + manifest.json)
- Site: `$DEEP_RESEARCH_WORKSPACE/<run_id>/site/dist/index.html`
- Delivered (if requested): `<deliver_dir>/<run_id>/`

**Failure diagnostics:**
- Worker logs: `<worktree>/.worker.log`
- Live session: `tmux attach -t <run_id>` (windows are named per worker)
- Per-worker result: `<worktree>/.status.json`
- If only the site stage failed, re-run `/rts-build-site` to pick that run up.

Provide a topic to begin, e.g. `/rts-research WebAssembly component model | deliver to: ~/sites`.
{{/if}}
