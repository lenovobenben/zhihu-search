# zhihu-search

`zhihu-search` is a Codex skill for researching Zhihu discussions through OpenCLI.

The goal is to make Zhihu a safe, low-frequency, user-authorized Chinese discussion source for agents. It uses the user's own Chrome session, Browser Bridge extension, and logged-in Zhihu account through OpenCLI's Zhihu read commands.

## Why

General web search often misses or cannot access logged-in Zhihu content. OpenCLI can read Zhihu through the user's browser session, so an agent can use it as an additional Chinese-language research channel for:

- technical discussions
- product feedback
- developer opinions
- finance and crypto discussions
- AI tooling debates
- current Chinese internet topics

Zhihu should be treated as discussion context, not as an authoritative fact source.

## Skill

The skill name is:

```text
zhihu-search
```

Repository structure:

```text
zhihu-search/
  SKILL.md
  agents/openai.yaml
```

The skill teaches an agent when and how to use these OpenCLI read commands:

```bash
opencli zhihu search "query" --type all --limit 10 -f json
opencli zhihu recommend --limit 10 -f json
opencli zhihu hot --limit 10 -f json
opencli zhihu question <question_id> --limit 5 -f json
opencli zhihu answer-detail "<answer_url>" --max-content 0 -f json
opencli zhihu answer-comments "<answer_url>" --limit 10 --replies-limit 2 -f json
```

## Safety Rules

- Use the user's own logged-in browser session.
- Keep default limits small, usually 10 to 20.
- Increase limits gradually only when needed.
- Do not run many large requests in parallel.
- Stop on 401, 403, captcha, verification, or risk-control signals.
- Do not bypass Zhihu access controls.
- Cite source URLs when summarizing.
- Separate facts, opinions, personal experience, and speculation.

## Status

The concise `SKILL.md` is ready to install into a Codex skills directory. It keeps the core workflow small: search broadly, inspect representative questions and answers, sample comments when sentiment matters, weight by relevance and votes, and cite Zhihu URLs.
