<p align="center">
  <a href="https://github.com/runapi-ai/gemini">
    <h3 align="center">Gemini API Skill for RunAPI</h3>
  </a>
</p>

<p align="center">
  Configure Gemini or OpenAI-compatible clients to use Gemini models on RunAPI.
</p>

<p align="center">
  <a href="https://runapi.ai/models/gemini"><strong>Model Reference</strong></a> · <a href="https://github.com/runapi-ai/gemini"><strong>Skill Repo</strong></a> · <a href="https://runapi.ai/models"><strong>All Models</strong></a>
</p>

<div align="center">

[![skills.sh](https://www.skills.sh/b/runapi-ai/gemini)](https://www.skills.sh/runapi-ai/gemini/gemini)
[![ClawHub](https://img.shields.io/badge/ClawHub-runapi--gemini-111827)](https://clawhub.ai/runapi-ai/runapi-gemini)
[![License](https://img.shields.io/github/license/runapi-ai/gemini)](https://github.com/runapi-ai/gemini/blob/main/LICENSE)

</div>
<br/>

Call the Gemini API through RunAPI with either the OpenAI SDK or Gemini
`contents` streaming clients — point any OpenAI-compatible client at
`https://runapi.ai/v1`, send `gemini-2.5-flash`,
`gemini-2.5-pro`, `gemini-3-flash-preview`, `gemini-3-pro-preview`, or
`gemini-3.1-pro-preview`, or call `gemini-3.5-flash` through the
`streamGenerateContent` path, and pay through one RunAPI balance. This skill
teaches Claude Code, Codex, Gemini CLI, Cursor, and 50+ agents how to wire a
Gemini API client up against RunAPI.

The canonical agent file is `skills/gemini/SKILL.md`.

## Install the skill

```bash
npx skills add runapi-ai/gemini -g
```

Or paste this prompt to your AI agent:

```text
Install the gemini skill for me:

1. Clone https://github.com/runapi-ai/gemini
2. Copy the skills/gemini/ directory into your
   user-level skills directory (e.g. ~/.claude/skills/
   for Claude Code, ~/.codex/skills/ for Codex).
3. Verify that SKILL.md is present.
4. Confirm the install path when done.
```

## Use the Gemini API on RunAPI

The Gemini API on RunAPI exposes two request styles:

1. **OpenAI-compatible** — `POST /v1/chat/completions`. Drop-in for
   any existing OpenAI SDK client.
2. **Contents streaming** — `POST /v1beta/models/<model>:streamGenerateContent`
   for `gemini-3-flash-preview` and `gemini-3.5-flash`. Drop-in for clients
   that send Gemini `contents` requests.

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_RUNAPI_TOKEN",
    base_url="https://runapi.ai/v1",
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
  baseURL: "https://runapi.ai/v1",
});

const response = await client.chat.completions.create({
  model: "gemini-2.5-flash",
  messages: [{ role: "user", content: "Hello!" }],
});
console.log(response.choices[0].message.content);
```

```bash
curl -X POST "https://runapi.ai/v1/chat/completions" \
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
| `gemini-2.5-flash` | `/v1/chat/completions` |
| `gemini-2.5-pro` | `/v1/chat/completions` |
| `gemini-3.1-pro-preview` | `/v1/chat/completions` |
| `gemini-3-pro-preview` | `/v1/chat/completions` |
| `gemini-3-flash-preview` | OpenAI **or** `:streamGenerateContent` |
| `gemini-3.5-flash` | `:streamGenerateContent` |

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
