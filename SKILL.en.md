---
name: skill-onboarding
description: After a user first uses a skill, actually run it once and hand back a "usage card" that surfaces the capabilities buried in its docs. **Pairs with skill-creator**: right after creating or editing a skill with it, run this flow to verify the first run and produce a card, closing the "build → run → card → feedback" loop. CLI tool skills are the priority — one command-line tool is often split across a dozen skills (21 lark-* skills all wrap a single lark-cli), so this merges them into one card and diffs the CLI's own inventory against local skills to find capabilities the user never knew existed. Triggers: first use of a skill, just finished using one, just created or edited a skill with skill-creator, or "what else can this skill do", "how do I use X", "what am I missing", "what else can this CLI do", "what commands don't I know about". Behavior is configurable (language, auto-trigger, card length, exclusion list). Not for skill quality scoring.
version: 3.2.0
agent_created: true
license: MIT
metadata:
  tags: "onboarding, capability discovery, CLI companion, skill usage"
  category: "productivity"
---

# skill-onboarding

<p align="center">
  <strong>After a user first uses a skill: run it once, then hand back one card.</strong>
</p>

<p align="center">
  <a href="SKILL.md" title="简体中文">🇨🇳 简体中文</a> ·
  <strong title="English">🇬🇧 English</strong>
</p>

## Why this exists

Skills load progressively: only `name` and `description` enter context at session start.
So **a user only ever uses the 1–2 most obvious features**, and the rest of the document may as well not exist.

This skill does one thing: after a user first genuinely uses a skill, **run it once, read it once, hand back one card.**

## Pairs with skill-creator

The two skills are only complete **used together**:

```
skill-creator     →  create / edit a skill
skill-onboarding  →  verify the first run, hand back one usage card
```

The loop is **build → run → card → feedback**. Whatever the card exposes (missing dependency,
docs disagreeing with the implementation, an ability that was never written down clearly)
is exactly what to fix in the skill next round.

With `pair_with_skill_creator` on (the default): after using skill-creator to create or edit a skill,
**run this flow right away** — don't stop at "built".

Division of labour: create / edit / delete → skill-creator; run once + verify + write the card → this skill;
quality scoring → neither.

## Three steps

1. **Pick the target** — one skill, or a CLI tool family?
2. **Probe** — read the whole thing + run read-only probes
3. **Write the card** — five sections, readable in one sitting

---

### 1 · Pick the target

**A group of skills that is really one thing** → **one card for the whole family**. Two signals:

- They share one underlying tool (`lark-im` / `lark-base` / … all resolve to `lark-cli`)
- They cross-reference each other, or one carries a "sub-skill routing" table (`design` routes out to `brand` / `design-system` / `ui-styling`)

The test isn't "the names look alike" — it's **"the user can't tell which one to use"**.

Skills may live in several different skills directories. Search all of them.

Check whether it has already been onboarded:

```
python "<skill_dir>/scripts/onboarding_state.py" check <id>
```

`NEW` → run the full flow. `SEEN` → only re-send when the user explicitly asks.

### 2 · Probe

**Read**: read SKILL.md in full, and **glance at the filenames under `references/`** — advanced capabilities usually live only there, with the main file saying nothing beyond "see xxx".

**Run**: pick the cheapest side-effect-free path. It must be a real call.

| Type | Probe |
|---|---|
| CLI tool | `--help` for the subcommand list → `doctor` / `status` / `whoami` for availability |
| Ships scripts | `--help` / dry-run / feed it minimal fake data |
| Generates artifacts | Write to a temp dir, delete afterwards |
| **No scripts / relies on an external service** | Check whether its declared prerequisites are present: is the tool on PATH, is the connection established. Run any self-check command it ships |
| Write-only (send mail, order, deploy) | Don't run it; verify up to a fully-constructed request |

**Within a set of scripts, prefer the ones that retrieve or query; avoid the ones that generate or call external services** — those need keys, cost money, and may mutate outside state.

**`--help` and the argument tables are the capability inventory — run them all if you can.** For CLI tools, `--help` on every major domain; for script-based skills, `--help` on every main script.
A user's blind spot is never "what is this tool called" — it's "there are fifteen more subcommands / fifteen more flags?".

**Three things that get misread as "the script is broken"**:

- `--help` reports a path error → usually the script **has no argument parsing** and treated `--help` as input. Run it with no args, or follow the usage format it prints itself.
- Output says "not found: `./xxx`" → the script **hardcodes a relative path** and must run from the skill directory. Nothing is actually missing.
- It returns structured JSON (even on error) → that's this skill's output protocol. Read the JSON, not the traceback.

**When it really fails, pick one of four causes and pick correctly**: missing dependency / **environment problem** / the command itself is broken / it simply never implemented `--help`.
Environment problems (shell, paths, wrapper) must read "environment issue, worked around" — **never "the skill is broken"**.

### 3 · Write the card

```
<✅ Verified working ｜ ⚠️ Partially working: reason ｜ ❌ Could not verify: reason>
<One line: what it's good at, what it isn't>

🎯 The three moves you'll use most
1. 「what to say」→ what you get
2. ...
3. ...

💡 Things you probably didn't know it could do
- 「what to say」→ why it's worth knowing

🔑 If you remember one thing, remember this
<the shortest possible phrase>
```

**Pick the second section's heading by nature**: `🎯 The three moves you'll use most` for tools; `🧭 When it comes into play` for methods and guidelines.

**A family of skills gets a family card**: the second section becomes a "what do you want to do" list, grouped by what the user would actually say, **not by command or module name**:

```
🧭 What do you want to do

· Chat / groups      → send, search history, create groups, escalate
· Set brand tone     → brand
· Make a logo/banner → built into design
· Build a deck       → built into design, with charts
```

**Rules**

- **No paths, no filenames, no provenance.** Users want capability, not location.
- Every capability needs a **copy-pasteable phrase**. If you can't write one, it's still a feature description.
- **Sections are a ceiling, not a quota.** If there's only one or two things to do, write one or two — the 💡 section can be absent entirely. Padding is fabrication.
- Readable in one sitting: single skill ≤40 lines, family card ≤60.
- For family cards, the 💡 section should lead with **diff findings**: what the tool supports vs what's installed locally — the gap is what the user never knew about.
- Any problem found must become an actionable next step, not just a complaint.

**Archive**

```
write   → ~/.workbuddy/skill-onboarding/cards/<id>.md
mark    → python "<skill_dir>/scripts/onboarding_state.py" mark <id>
```

## Configuration

Set once, applies from then on. Stored at `~/.workbuddy/skill-onboarding/config.json` (defaults used if absent).

```
python "<skill_dir>/scripts/onboarding_state.py" config                # show
python "<skill_dir>/scripts/onboarding_state.py" config set <key> <value>
python "<skill_dir>/scripts/onboarding_state.py" config reset          # back to defaults
```

| Key | Default | Effect |
|---|---|---|
| `language` | `zh` | Card language: `zh` / `en` / `auto` (follow the user) |
| `auto_trigger` | `true` | Offer a card automatically after a first run |
| `max_lines` | `40` | Line cap for a standard card |
| `family_max_lines` | `60` | Line cap for a family card |
| `exclude` | `[]` | Skills never to onboard (`check` returns `SKIP`) |
| `pair_with_skill_creator` | `true` | Run a first-run verification after creating / editing a skill |

Hard to break: invalid values are rejected up front, and `config reset` always brings you back.

## Safety

- **Read-only first**: no deleting files, no sending messages, no writing to production data, no placing orders, no changing config.
- IM write operations are limited to conversations of ≤3 people. Large groups are read-only, always.
- Anything that can only be verified by really touching a third party: verify up to a constructed request, and note "not actually run".
- Use fake data for verification. Never pull in real business data.

## Don't

- Write the card after reading only the description → step 2 skipped.
- Write "verified working" with zero tool calls → fabricated conclusion.
- Produce one card per skill in the same family → fragments the picture; the user still can't see the whole.
- Output scorecards / compliance checks / improvement advice → that's skill-tester's job.
- Recite the SKILL.md directory structure → that's a table of contents, not usage.

## Environment notes

- The scripts are pure Python standard library — `python` / `python3` just works. If it isn't on PATH,
  use the absolute path to your own interpreter.
- **Set the working directory via a `cwd` option, not by relying on `cd`** — in some restricted shells
  `cd` silently does nothing and the script still runs from the original directory. Plenty of skill
  scripts hardcode relative paths like `./references/...`.
- Some CLIs ship a `sh` wrapper depending on `dirname` / `sed`. On a shell with a broken toolchain it
  dies with `Cannot find module '...\node_modules\...'` (note the truncated path — the wrapper failed
  to resolve its own directory). Call the real entry point directly to bypass it —
  **this is an environment problem, not a broken skill**.

## Example

`example.md` — one standard card plus one CLI tool card. Match that density.
