---
name: zhihu-search
description: Use Zhihu as a logged-in Chinese discussion research source through OpenCLI. Use when the user asks phrases like "知乎上怎么说", "知乎上搜一搜", "去知乎看看", "中文社区怎么看", "搜索中文信息", or when Chinese-language discussion context would materially improve an answer. Automatically include Zhihu as one search source, inspect questions and answers, weigh answers by vote counts and relevance, and cite Zhihu URLs. Requires the user's existing logged-in Zhihu browser session and OpenCLI Browser Bridge.
---

# Zhihu Search

Use this skill to research Zhihu discussions through OpenCLI. Treat Zhihu as a source of Chinese-language discussion context, personal experience, opinions, and leads, not as an authoritative fact source.

## Command

Always use the local OpenCLI source checkout because some Zhihu commands may not be in the published release yet:

```bash
cd /Users/lihaidong/code/OpenCLI
npm run dev -- zhihu <command> ...
```

In examples below, `zhihu` means:

```bash
cd /Users/lihaidong/code/OpenCLI
npm run dev -- zhihu
```

Useful read commands:

```bash
zhihu search "query" --type all --limit 10 -f json
zhihu recommend --limit 10 -f json
zhihu hot --limit 10 -f json
zhihu question <question_id> --limit 5 -f json
zhihu answer-detail "<answer_url>" --max-content 0 -f json
zhihu answer-comments "<answer_url>" --limit 10 --replies-limit 2 -f json
```

## Search Workflow

Start broad, then deepen only where useful:

1. Build 2-4 search queries, not just the user's original wording. Keep key English names, add Chinese intent words such as `怎么看`, `评价`, `体验`, `坑`, `对比`, `方案`, `实践`.
2. Run `search` first for explicit topics. Use `recommend` or `hot` only for current/general "知乎最近在聊什么" requests.
3. Use `--limit 10-20` for quick factual lookups. For platform sentiment, public opinion, or "风向" analysis, inspect at least 50 search results when available; use more if the result set is broad and stable.
4. Pick promising results by title relevance, vote count, recency when relevant, information density, and viewpoint diversity.
5. For question URLs, read up to 5 answers with `question`; for answer URLs or standout answers, read full text with `answer-detail`.
6. For sentiment or controversy analysis, read top-level comments on representative answers with `answer-comments --limit 10 --replies-limit 0`; comments are useful for pushback, corrections, and audience reception.

If results are sparse or noisy, rewrite the query once or twice. If still weak, say the Zhihu sample is insufficient.

## Selection Rules

Use vote counts as a weighting signal, not as truth:

- Prefer high-vote answers when they are directly relevant to the user's question.
- Include lower-vote answers when they provide concrete evidence, a minority viewpoint, technical detail, or firsthand experience.
- Discount answers that are high-vote but off-topic, rhetorical, outdated, unsupported, or mostly emotional.
- For "怎么看/评价", sample multiple viewpoints.
- For "体验/坑/值不值", prioritize concrete user experience and comments.
- For technical topics, prioritize implementation detail and cross-check outside Zhihu when facts matter.
- For current events, finance, legal, medical, or other high-stakes topics, use Zhihu only as discussion context and verify facts elsewhere.

## Output

Group findings by theme. Include representative URLs and vote counts when useful. State the sample size, for example: "I checked 50 Zhihu search results, read 8 answers, and sampled first-level comments on 4 answers." Separate facts, opinions, personal experience, and speculation. When answers conflict, report the disagreement instead of forcing one conclusion.

## Safety

- Use only the user's existing logged-in browser session and cookies.
- Do not bypass Zhihu access controls, captchas, verification, paywalls, or risk-control prompts.
- Stop immediately on 401, 403, captcha, verification, account-risk, or abnormal traffic signals.
- Do not run many large Zhihu requests in parallel.
- Do not call write commands such as `answer`, `comment`, `like`, `favorite`, or `follow` unless the user explicitly asks for that exact write action.
- Cite source URLs for every substantive Zhihu-derived point.
