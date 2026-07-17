{{#if args}}
site-builder: Build site for: {{args}}
{{else}}
## /rts-build-site — build (or rebuild) a site from an existing research run

**Synopsis:** `/rts-build-site [<run_dir>] [| deliver to: <dir>]`

**What it does:** Runs only the site-builder stage (fast — no research, no tmux team).
- With a `<run_dir>` argument, it builds that run directly.
- With no argument, it selects a run for you: it reads `~/.deep-research-agent/runs.json`
  and picks the most recent run that does NOT yet have a `site/dist/index.html`. This is the
  retry path when the site stage of a prior `/rts-research` failed.

**Required setup:** `~/.deep-research-agent/.env` filled and `factory doctor` passing. If a
run has no `manifest.json`, the site build cannot proceed — re-run `/rts-research` for it.

**Success outputs:** `<run_dir>/site/dist/index.html`; delivered copy at `<deliver_dir>/<run_id>/`
if a deliver suffix or `$FACTORY_DELIVER_DIR` is set.

**Failure diagnostics:** check `<run_dir>/site/.worker.log`, the site-builder `.status.json`,
and the `bun run build` output. Re-run this command to retry.

Pending-run selection (no args):
Read ~/.deep-research-agent/runs.json and find the most recent run that does NOT yet
have a site/dist/index.html file. Then run: site-builder: Build site for: <that run_dir>

If all runs already have a site built, display a table of available runs with their topics
and creation times, and ask which one to rebuild.

If runs.json does not exist or is empty, say so clearly.
{{/if}}
