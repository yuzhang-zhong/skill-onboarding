<p align="center">
  <strong>Run a skill once. Hand back one card.</strong>
</p>

<p align="center">
  <strong title="English">🇬🇧</strong> ·
  <a href="README.zh-CN.md" title="简体中文">🇨🇳</a>
</p>

## Why this exists

Skills load progressively: only `name` and `description` enter context at session start, and the body
is pulled in on demand.

The result is that **a user only ever uses the 1–2 most obvious features**, and the rest of the
document may as well not exist.

This skill does one thing: after a user first genuinely uses a skill, **run it once, read it once,
hand back one card.**

## Three steps

1. **Pick the target** — one skill, or a family?
2. **Probe** — read it in full + run read-only probes. Real calls, not inference
3. **Write the card** — one card you can read in a single sitting

## A family of skills becomes one card

One command-line tool is often split across a dozen skills — Feishu ships 21 `lark-*` skills that all
wrap a single `lark-cli`. One card per skill just fragments the picture; the user still can't see the
whole. So they get merged into a single capability map.

Then it diffs: **what the tool supports − what's installed locally**. The remainder is exactly what
the user never knew existed.

## What a card looks like

```
✅ Working. The CLI itself is fine, self-check passes on every item.

The whole Feishu suite — one command covering 26 domains. Your 21 local Feishu skills
are all thin wrappers over this one tool.

🧭 What do you want to do

· Message / manage groups → send, search history, create groups, add members, pin, SMS/call escalation
· Write documents        → create, read, insert images, search, restore old versions
· Work with sheets       → read/write cells, verify formulas, charts, pivot tables, conditional
                           formatting, import/export Excel & CSV
...

💡 Things you probably didn't know it could do

- 「preview it first, don't actually send」→ every operation supports a dry-run mode, so you can see
  the result before committing — especially useful for sending messages or editing docs
- 「check whether anything's wrong with Feishu on my end」→ one command runs a full health check:
  version, auth, identity, connectivity
...

🔑 If you remember one thing, remember this

「handle this in Feishu for me — preview it first」
```

**No file paths, no filenames, no provenance anywhere in the card.** Users want capability, not
location.

More examples in [`example.md`](example.md).

## Pairs with skill-creator

```
skill-creator     →  create / edit a skill
skill-onboarding  →  verify the first run, hand back one card
```

The loop is **build → run → card → feedback**. Whatever the card exposes (a missing dependency, docs
disagreeing with the implementation, an ability that was never written down clearly) is exactly what
to fix in the skill next round.

## Install

```bash
git clone https://github.com/yuzhang-zhong/skill-onboarding.git \
  ~/.workbuddy/skills/skill-onboarding
```

Point it at your own skills directory (Claude Code uses `~/.claude/skills/`). The state script is
pure Python standard library — zero dependencies.

## Configuration

```bash
python scripts/onboarding_state.py config                # show
python scripts/onboarding_state.py config set <key> <v>  # change
python scripts/onboarding_state.py config reset          # back to defaults
```

| Key | Default | Effect |
|---|---|---|
| `language` | `zh` | Card language: `zh` / `en` / `auto` |
| `auto_trigger` | `true` | Offer a card automatically after a first run |
| `max_lines` | `40` | Line cap for a standard card |
| `family_max_lines` | `60` | Line cap for a family card |
| `exclude` | `[]` | Skills never to onboard |
| `pair_with_skill_creator` | `true` | Run a first-run verification after creating / editing a skill |

Invalid values are rejected up front; `config reset` always brings you back. Hard to break.

## Scope

| | Audience | Output |
|---|---|---|
| `skill-creator` | authors | create / iterate a skill |
| `skill-tester` and friends | authors | structure checks, quality scoring |
| **this skill** | **users** | **a usage card after the first run** |

Deciding whether a skill is any good is someone else's job. This one only decides **how the user
should use it**.

## License

MIT.
