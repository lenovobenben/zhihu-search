# zhihu-search

`zhihu-search` is a Codex/Claude skill project for researching Zhihu discussions through OpenCLI.

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

## Planned Skill

The skill name will be:

```text
zhihu-search
```

Expected local structure:

```text
zhihu-search/
  SKILL.md
```

The skill should teach an agent when and how to use these OpenCLI commands:

```bash
opencli zhihu search "query" --type all --limit 20
opencli zhihu recommend --limit 20
opencli zhihu question <question_id> --limit 50
opencli zhihu answer-detail "<answer_url>" --max-content 0
opencli zhihu answer-comments "<answer_url>" --limit 20 --replies-limit 3
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

## Current Status

This repository is only a starting point. The first useful artifact will be a concise `SKILL.md` that can be installed into a Codex skills directory.
