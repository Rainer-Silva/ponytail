# INSTRUCTIONS.md — Ponytail (Rainer-Silva fork)

This file was added to the fork for Rainer Andrade Silva on 12 November 2026 (Europe/Stockholm). It is not part of the upstream project.

- **Upstream:** https://github.com/DietrichGebert/ponytail
- **This fork:** https://github.com/Rainer-Silva/ponytail
- **Site:** https://ponytail.dev
- **License:** MIT
- **Reviewed snapshot:** 189,338 stars, 10,541 forks, last upstream commit 29 Oct 2026, 12:59 CET (Europe/Stockholm), latest release v5.3.3. The Instagram reel claimed about 183k stars; the live count is in the same range.

## What it is

Ponytail is a skill / plugin for coding agents (Claude Code, Cursor, Codex, OpenCode, Gemini CLI, and several others). It tries to make the agent behave like a “lazy senior developer”: reuse what is already in the repo, prefer the standard library or a built-in platform feature, and write only the code the task needs. It also adds `/ponytail-review` and `/ponytail-audit` commands, and in recent Claude Code versions a local cost/token “band” and board (data stays in `~/.config/ponytail/band/` by default).

Upstream’s own benchmark (Claude Code, Opus 5.5, 39 tasks, 5 runs each, October 2026) claims Ponytail 5 uses about **45% fewer tokens**, **26% lower cost**, **53% less code**, and **41% less time**, while shipping more tests. Those numbers are the author’s benchmark, not an independent audit. The skill also adds extra rules into the prompt, so very short tasks can sometimes use *more* tokens, not fewer.

## Can it cut token usage / cost?

| Question | Honest answer |
|---|---|
| Cut Grok Bot / this assistant’s usage? | **No.** Grok Bot will not load this skill unless it is separately installed into a coding agent you run. |
| Cut tokens in Claude Code, Cursor, Codex, etc.? | **Possibly.** This is the only repo in the reel whose stated purpose is to reduce tokens, cost, and unnecessary code. Treat the “−45% tokens” figure as a vendor claim and measure it on a few of your own tasks before relying on it. |
| Fit for Rainer’s setup? | Best candidate of the five for coding-agent savings. Install into a coding agent you control (for example Cursor or Claude Code), not into Grok Bot’s backend. |

## Setup (do not run until you have decided to try it)

Read `INSTALL.md` for your agent. Examples from upstream:

- **Claude Code:** `/plugin marketplace add DietrichGebert/ponytail` then, in a second prompt, `/plugin install ponytail@ponytail`
- **Cursor:** see `INSTALL.md` (hooks plus the skill). The Claude/Codex/Cursor hooks run small Node.js scripts, so `node` should be on your PATH.
- **OpenCode:** `opencode plugin add @dietrichgebert/ponytail`
- **Any agent that reads `AGENTS.md`:** copy `AGENTS.md` into the project, or install `skills/ponytail/SKILL.md` as a skill.

Prefer installing from a tagged release, and scan `skills/ponytail/` with SkillSpector (`--no-llm`) first. To use this fork, point the marketplace/plugin URL at `https://github.com/Rainer-Silva/ponytail` instead of upstream.

Levels such as `lite` / `full` / `ultra` / `off` trade how strongly the rules are applied. Start with the default or `lite`, then measure.

## Risks and caveats

- **Star count is extreme** for a repo created on 12 June 2026 (about 1,246 stars/day, ~189k stars in five months). That is possible for a viral agent skill, but it is also in the range where purchased or inflated stars are common. Judge the code and a small trial, not the badge.
- Lifecycle hooks execute Node.js on agent events. Review `hooks/` and `scripts/cursor-hooks.js` before enabling them. The skills can still be used if hooks are off (you may see a harmless `node: command not found` if Node is missing).
- “Write less code” must not mean skipping validation, error handling, security, or accessibility. Upstream says those are out of scope for cuts; still review the agent’s output.
- There is a ponytail.dev waitlist / “something’s coming” banner. Do not join paid products or add billing without approval.
- No passwords or API keys in chat.

## Cost note

Running anything that needs paid APIs or servers requires Rainer’s spend approval first. Forking, reading the skill, and installing it into an agent you already pay for should not add a new subscription, but the agent’s normal token billing still applies. Measure whether costs actually go down before keeping it enabled.

## Recommendation

The only one of the five that is actually aimed at token savings. Worth a careful, measured trial in a coding agent (after a SkillSpector scan), not a way to cut Grok Bot usage. Do not treat the published −45% figure as guaranteed.
