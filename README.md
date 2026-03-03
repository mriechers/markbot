# Your Helpful MarkBot!

Centralized Slack bot for the [podcast-publishing-suite](https://github.com/Wonder-Cabinet-Productions/podcast-publishing-suite). Posts producer-friendly notifications as a single bot identity.

## Quick Start

```bash
pip install -r requirements.txt
export SLACK_BOT_TOKEN=xoxb-your-token

# Test with dry run (no token needed)
python3 markbot.py --dry-run transcribe-start --episode "Test" --channel X
```

## Setup

See [docs/SETUP.md](docs/SETUP.md) for Slack App creation and configuration.

## Commands

- **`transcribe-start`** — "Working on a transcript" notification (prints `thread_ts`)
- **`transcribe-ready`** — "Transcript ready to edit" with Google Doc link
- **`schedule-alert`** — Release readiness alerts (missing / drafted / scheduled)
- **`post`** — Generic Block Kit poster for custom payloads
