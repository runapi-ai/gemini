# Gemini API Skill for RunAPI

[![skills.sh](https://skills.sh/b/runapi-ai/gemini)](https://skills.sh/runapi-ai/gemini)

Call the Gemini API through RunAPI with either the OpenAI SDK or the native
Gemini protocol — point any OpenAI-compatible client at
`https://runapi.ai/v1beta/openai`, send `gemini-2.5-flash`,
`gemini-2.5-pro`, `gemini-3-flash-preview`, `gemini-3-pro-preview`, or
`gemini-3.1-pro-preview`, and pay through one RunAPI balance. This skill
teaches Claude Code, Codex, Gemini CLI, Cursor, and 50+ agents how to wire a
Gemini API client up against RunAPI.

The canonical agent file is `skills/gemini/SKILL.md`.

## Install the skill

Pick one:

**A.** With [skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add runapi-ai/gemini -g
```

**B.** Or manually: clone this repo and copy `skills/gemini/` into your
agent's skills directory (for example `~/.claude/skills/` for Claude Code, or
the `skills/` directory of a Codex / Gemini CLI plugin checkout).

## Use the Gemini API on RunAPI

The Gemini API on RunAPI exposes two protocols:

1. **OpenAI-compatible** — `POST /v1beta/openai/chat/completions`. Drop-in for
   any existing OpenAI SDK client.
2. **Native Gemini** — `POST /v1beta/models/<model>:streamGenerateContent`
   (currently `gemini-3-flash-preview`). Drop-in for the official Google
   Generative AI SDK.

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_RUNAPI_TOKEN",
    base_url="https://runapi.ai/v1beta/openai",
)

response = client.chat.completions.create(
    model="gemini-2.5-flash",
    messages=[{"role": "user", "content": "Hello!"}],
)
print(response.choices[0].message.content)
```

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: "YOUR_RUNAPI_TOKEN",
  baseURL: "https://runapi.ai/v1beta/openai",
});

const response = await client.chat.completions.create({
  model: "gemini-2.5-flash",
  messages: [{ role: "user", content: "Hello!" }],
});
console.log(response.choices[0].message.content);
```

```bash
curl -X POST "https://runapi.ai/v1beta/openai/chat/completions" \
  -H "x-api-key: YOUR_RUNAPI_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-2.5-flash",
    "messages": [{"role": "user", "content": "Hello!"}]
  }'
```

Get a RunAPI API Key at <https://runapi.ai/api_keys>.

## Connect Gemini CLI itself

```bash
export GOOGLE_API_KEY=YOUR_RUNAPI_TOKEN
export GOOGLE_GENAI_BASE_URL=https://runapi.ai
gemini
```

## Supported Gemini models

| Model ID | Endpoint |
|---|---|
| `gemini-2.5-flash` | `/v1beta/openai/chat/completions` |
| `gemini-2.5-pro` | `/v1beta/openai/chat/completions` |
| `gemini-3.1-pro-preview` | `/v1beta/openai/chat/completions` |
| `gemini-3-pro-preview` | `/v1beta/openai/chat/completions` |
| `gemini-3-flash-preview` | OpenAI **or** native `:streamGenerateContent` |

`gemini-flash-latest` is an alias for `gemini-3-flash-preview`.

## Routing

- Gemini API on RunAPI: <https://runapi.ai/models/gemini>
- Gemini API docs: <https://runapi.ai/docs#gemini>
- Provider page: <https://runapi.ai/providers/google>
- Browse the full RunAPI catalog: <https://runapi.ai/models>
- Skill repository: <https://github.com/runapi-ai/gemini>

## Agent rules

- Keep API keys in `GOOGLE_API_KEY` / `OPENAI_API_KEY` (or your secret
  manager); never inline them in commits or shell history.
- Stream long responses (`stream: true`) so the agent can release the
  terminal/IO loop early.
- For pricing, rate-limit, and commercial-usage answers, link to
  <https://runapi.ai/models/gemini> rather than this README.

## License

Licensed under the Apache License, Version 2.0.
