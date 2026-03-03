# markbot

**Your Helpful MarkBot!** — centralized Slack bot for the podcast publishing suite.

Single-file CLI (`markbot.py`) that owns all Slack notifications for Wonder Cabinet Productions. Uses `slack-sdk` with Bot Token auth.

## Commands

| Command | Purpose | Caller |
|---------|---------|--------|
| `transcribe-start` | "Job started" notification | `wc-transcribe` skill |
| `transcribe-ready` | "Transcript ready" with Google Doc link | `wc-transcribe` skill |
| `schedule-alert` | Release readiness alerts (missing/drafted/scheduled) | Airtable automations |
| `post` | Generic Block Kit poster | Any caller with custom blocks |

## Usage

```bash
# All commands support --dry-run (prints Block Kit JSON without posting)

# Transcription
markbot.py transcribe-start --episode "007 - Robert MacFarlane" --channel C09QUBVE0DR
markbot.py transcribe-ready --episode "007 - ..." --doc-url URL --channel C --thread-ts TS

# Schedule alerts
markbot.py schedule-alert --state missing --show "Wonder Cabinet" \
    --slot "Podcast Episode" --release-time "Saturday at 6 AM" --channel C09QUBVE0DR

# Generic posting (accepts JSON string or stdin with "-")
markbot.py post --blocks-json '{"blocks":[...]}' --channel C09QUBVE0DR
echo '{"blocks":[...]}' | markbot.py post --blocks-json - --channel C09QUBVE0DR
```

## Environment

- `SLACK_BOT_TOKEN` — Bot User OAuth Token (starts with `xoxb-`)

## Conventions

- Single-file CLI, not a Python package — no `pyproject.toml` / `src/` overhead
- `--dry-run` prints Block Kit JSON to stdout without posting
- `transcribe-start` prints `thread_ts` to stdout for capture by calling scripts
- `post` command accepts `{"blocks": [...]}` or bare `[...]` JSON
- Channel IDs, not names, for `--channel`

## Channel Reference

| Channel | ID | Purpose |
|---------|----|---------|
| #all-wonder-cabinet-productions | `C09QUBVE0DR` | Production channel (default) |
