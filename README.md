# Sidekick OpenClaw Skill

OpenClaw skill for Sidekick outbound calling.

Current version: `v1.1.0` (2026-02-12)

This package lets an OpenClaw agent call real businesses through:

`OpenClaw -> Sidekick API -> Twilio -> ElevenLabs voice agent -> callee`

## Who this is for

Builders using OpenClaw who want their agent to place real phone calls.

## What is included

- `sidekick-openclaw-skill.json` - ready-to-paste tool definitions
- `sidekick-outbound-call.schema.json` - JSON schema for outbound call input
- `.env.example` - required environment variable template
- `examples/request.test_mode.json` - safe test payload
- `examples/request.natural_flow.json` - natural conversation payload (interactive AI line example)
- `examples/request.memory_context.json` - natural conversation with retrieval memory + manual context
- `PUBLISH_TO_GITHUB.md` - first-time publishing guide

## Prerequisites

- A free Sidekick account at `https://voice.squaresidekick.com` (sign up/login)
- A claimed Sidekick phone number
- API key created in Sidekick `/agent` via the `🦞` panel
- OpenClaw runtime with env vars + HTTP tools enabled

## Quick Start (No commands)

1. Go to `https://voice.squaresidekick.com`, create your free account, then log in.
2. In Sidekick, create API key and copy it once.
3. In Sidekick, claim a phone number if you have not already.
4. In OpenClaw, set env var:
   - `SIDEKICK_OUTBOUND_API_KEY=<your-key>`
5. Copy `sidekick-openclaw-skill.json` into your OpenClaw skills/tools config.
6. Reload OpenClaw.
7. Run first call using `test_mode: true` from `examples/request.test_mode.json`.

## Live call endpoint summary

- Start call: `POST https://voice.squaresidekick.com/api/outbound/call`
- Check status: `GET https://voice.squaresidekick.com/api/outbound/call/{{call_id}}?live=1`
- Wait transcript: `GET https://voice.squaresidekick.com/api/outbound/call/{{call_id}}/wait-transcript?timeout_ms=90000&interval_ms=2500`
- Cancel call: `POST https://voice.squaresidekick.com/api/outbound/call/{{call_id}}/cancel`

## Best-practice defaults

- Start in `test_mode: true`
- Use `wait_for_hello: true` for most human-run businesses
- Use `wait_for_hello: false` for interactive AI phone lines that answer immediately
- Keep `transcript_required: true`
- Set `contact_card.name` to the OpenClaw agent name
- Set `contact_card.callback_phone` so businesses can call back
- Use `opening_line` when you want exact first words spoken (verbatim)
- Keep `load_memory: true` to reuse learned context from prior calls (same destination, same account)
- Use `memory_context` for one-off private context on this call
- Use `load_soul: true` only if your backend has `OUTBOUND_SOUL_FILE` configured

## Natural conversation example

```json
{
  "to": "+18002428478",
  "instructions": "Have a natural conversation. Start with: 'Hey, how's your day going?' Wait for their response. Then ask about San Francisco weather. Wait. Then ask for a fun fact. Keep it casual back-and-forth until you get the info.",
  "opening_line": "Hey, how's your day going?",
  "wait_for_hello": false,
  "test_mode": false
}
```

`instructions` is accepted as an alias for `goal`. If both are provided, `goal` is used.

## Memory-aware example

```json
{
  "to": "+18002428478",
  "instructions": "Have a natural conversation. Ask two short questions and wait between each.",
  "opening_line": "Hey, how is your day going?",
  "wait_for_hello": false,
  "load_memory": true,
  "load_soul": false,
  "memory_context": "Keep this to a friendly 60-90 second exchange. Avoid sounding scripted.",
  "test_mode": false
}
```

## Troubleshooting

- `401 Unauthorized`
  - API key is missing or invalid in OpenClaw env.
- `No transcript yet`
  - Poll status and call `wait-transcript` endpoint.
- `Call failed`
  - Check destination number formatting (`+1...` E.164).

## Support
jinx@squaresidekick.com

Open an issue in this repository for setup help or bug reports.
