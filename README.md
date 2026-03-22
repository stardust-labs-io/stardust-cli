# stardust-cli

Command-line interface for [Stardust Jams](https://stardust-jams.stardustlabs.io) — auto-generated from the OpenAPI spec.

## Install

```bash
# Download
curl -fsSL https://raw.githubusercontent.com/stardust-labs-io/stardust-cli/main/stardust -o /usr/local/bin/stardust
chmod +x /usr/local/bin/stardust
```

## Setup

1. Create an API key in the Stardust Jams app under **Settings > API Keys**
2. Export it:

```bash
export STARDUST_API_KEY=sj_your_key_here
```

Optionally point to a different server:

```bash
export STARDUST_API_URL=http://localhost:5550  # default: https://stardust-jams.stardustlabs.io
```

## Usage

```bash
stardust help                  # List all commands
stardust <command> [options]   # Run a command
```

Commands map directly to API endpoints. Pass query parameters as the first argument and JSON body via stdin or flags.

```bash
# Search
stardust get-search "term=jazz&types=artist"

# Get an event
stardust get-event 42

# Create an event
stardust create-event '{"name": "Jazz Night", "venue_id": 1}'

# List your API keys
stardust list-api-keys

# Like a recording
stardust like-recording 7
```

## Requirements

- bash 4+
- curl
- [jq](https://jqlang.github.io/jq/) (optional, for pretty-printed output)

## License

MIT
