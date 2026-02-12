# Sidekick OpenClaw Skill

Production-ready OpenClaw skill package for Sidekick outbound calling.

This package lets an OpenClaw agent call real businesses through:

`OpenClaw -> Sidekick API -> Twilio -> ElevenLabs voice agent -> callee`

## What is included

- `sidekick-openclaw-skill.json` - ready-to-paste tool definitions
- `sidekick-outbound-call.schema.json` - JSON schema for outbound call input
- `.env.example` - required environment variable template
- `examples/request.test_mode.json` - safe test payload
- `PUBLISH_TO_GITHUB.md` - first-time publishing guide

## Prerequisites

- A Sidekick account with a claimed phone number
- API key created in Sidekick `/agent` via the `🦞` panel
- OpenClaw runtime with env vars + HTTP tools enabled

## Quick Start (No commands)

1. In Sidekick, create API key and copy it once.
2. In OpenClaw, set env var:
   - `SIDEKICK_OUTBOUND_API_KEY=<your-key>`
3. Copy `sidekick-openclaw-skill.json` into your OpenClaw skills/tools config.
4. Reload OpenClaw.
5. Run first call using `test_mode: true` from `examples/request.test_mode.json`.

## Live call endpoint summary

- Start call: `POST https://voice.squaresidekick.com/api/outbound/call`
- Check status: `GET https://voice.squaresidekick.com/api/outbound/call/{{call_id}}?live=1`
- Wait transcript: `GET https://voice.squaresidekick.com/api/outbound/call/{{call_id}}/wait-transcript?timeout_ms=90000&interval_ms=2500`
- Cancel call: `POST https://voice.squaresidekick.com/api/outbound/call/{{call_id}}/cancel`

## Best-practice defaults

- Start in `test_mode: true`
- Use `wait_for_hello: true`
- Keep `transcript_required: true`
- Set `contact_card.name` to the OpenClaw agent name
- Set `contact_card.callback_phone` so businesses can call back

## Troubleshooting

- `401 Unauthorized`
  - API key missing/invalid in OpenClaw env.
- `No transcript yet`
  - Poll status and call `wait-transcript` endpoint.
- `Call failed`
  - Check destination number formatting (`+1...` E.164).

