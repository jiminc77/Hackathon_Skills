# Hackathon Skills

Three small agent skills for a timed coding task with a stakeholder, written for Codex CLI. Each folder holds one skill with `SKILL.md` at its root.

| Skill | What it does | Source |
|---|---|---|
| `grilling` | Finds decisions not made yet and asks them in numbered rounds, each with a recommended answer. | [mattpocock/skills](https://github.com/mattpocock/skills), MIT, one instruction changed: it looks facts up itself instead of spawning a sub-agent |
| `verification-before-completion` | Requires running the command that proves a claim before saying work is done. For the final check, one fresh subagent runs the checks instead of the agent that wrote the code. | [obra/superpowers](https://github.com/obra/superpowers) (commit 2ce8aa1), MIT, one section added at the end |
| `intent-handoff` | Keeps AGENTS.md, DECISIONS.md and HANDOFF.md current, and marks decisions the stakeholder has not confirmed yet. | Original, MIT |

## Install

```bash
git clone --depth 1 https://github.com/jiminc77/Hackathon_Skills ~/.agents/skills
```

If `~/.agents/skills` already exists, use this instead:

```bash
git clone --depth 1 https://github.com/jiminc77/Hackathon_Skills /tmp/hs && mkdir -p ~/.agents/skills && cp -R /tmp/hs/grilling /tmp/hs/verification-before-completion /tmp/hs/intent-handoff ~/.agents/skills/
```

Codex loads user skills from `~/.agents/skills`. Restart Codex and run `/skills` to check that the three skills are listed.

## When to call each skill

1. After talking to the stakeholder yourself, call `$grilling` to find decisions you missed. Ask rule-precedence questions yourself.
2. After the requirements are agreed, call `$intent-handoff` to write AGENTS.md. Call it again after each major decision.
3. After each unit of work, call `$verification-before-completion` with a scope, for example "with the verification commands in AGENTS.md". Commit when it passes.
4. Before submitting, call `$verification-before-completion` and ask for the final check against AGENTS.md in those words; only this request starts the subagent. Then run `grep '^## D.*[(]UNCONFIRMED[)]' DECISIONS.md` and compare the result with the summaries.

## License

The third-party skills keep their own LICENSE files. Everything else is under the MIT License in [LICENSE](LICENSE).
