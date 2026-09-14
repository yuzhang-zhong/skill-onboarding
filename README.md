<p align="center">
  <img src="assets/logo.jpg" alt="skill-onboarding" width="200" />
</p>

<p align="center">
  <strong>Use a skill once. Get one card back.</strong>
</p>

<p align="center">
  <strong title="English">🇬🇧</strong> ·
  <a href="README.zh-CN.md" title="简体中文">🇨🇳</a>
</p>

## You installed a pile of skills and use one of them

Not your fault.

Skills load progressively. At session start the agent sees a name and a description. The body is read later, and only if something matches. So a document describes eight features and you run into the first two. The other six you never find out about.

This skill does one thing. After you actually use a skill for the first time, it runs the thing once, reads it once, and hands you a card with the part you were missing.

## Three steps

1. **Pick the target** one skill, or a group
2. **Probe** read it in full, run read-only probes. Real calls, not guesses
3. **Write the card** one card you can finish in a sitting

## A group of skills is usually one thing

Those 21 Feishu skills sit on top of a single command. Those 7 design skills are parts of one tool.

One card each is useless. You would get 21 fragments and still no picture. So they merge.

Then it subtracts: what the tool supports, minus what is installed locally. What is left is the part you never knew about.

## Three real cases

### 1. You have 21 Feishu skills

<table>
<tr>
<td width="50%">

**Before**

You want a table. You bounce between `lark-sheets`, `lark-base`, and `lark-drive` trying to guess which one.

You want to send a message and cannot tell whether that is `lark-im` or `lark-unified`.

You have seen all 21 names. You have never worked out how they relate.

</td>
<td width="50%">

**After**

One card.

First line says the 21 skills all sit on a single `lark-cli`, covering 26 domains.

Then you learn it also handles mind notes and slash commands, with no local skill for either, and you can just ask. And that every operation can dry-run before you commit to sending anything.

</td>
</tr>
</table>

### 2. You installed an AI-flavor remover and forgot about it

<table>
<tr>
<td width="50%">

**Before**

You remember it can flag words like "仿佛", "一丝", "缓缓" in Chinese prose.

What else? No idea.

When you installed it, why you stopped using it, also no idea.

</td>
<td width="50%">

**After**

Line one tells you the truth: the skill is disabled, you have to enable it before it triggers on its own.

Then you find it carries six named master-prose techniques. You can ask for "rewrite this the way Yu Hua would".

You also learn which edits it does automatically and which ones need a human, so you stop guessing.

</td>
</tr>
</table>

### 3. You want a deck and do not know who to ask

<table>
<tr>
<td width="50%">

**Before**

`slides`, `design`, `design-system`, `ui-ux-pro-max`. All four look relevant.

You picked `slides` at random, shipped something passable, and never checked whether the other three would have been better.

</td>
<td width="50%">

**After**

One card turns seven design skills into a single table. Brand tone goes to `brand`. Colors and type scales go to `design-system`. Logos and decks are built into `design`.

It also mentions `ui-ux-pro-max` has three dials you can turn, visual variance, motion intensity, visual density, ten steps each. You would never have guessed that one.

</td>
</tr>
</table>

## What a card looks like

```
Working. The CLI itself is fine, every self-check passes.

The whole Feishu suite. 26 domains, and your 21 local Feishu skills all sit on
top of this one command.

What you can do

    Messages, groups     send, search history, create groups, escalate
    Documents            create, read, insert images, search, restore versions
    Sheets               read/write cells, verify formulas, charts, pivot tables, import/export
    Drive                upload, download, move, comments, permissions, two-way sync
    Calendar, meetings   agenda, free/busy, find rooms, suggest times
    Tasks                create, complete, remind, lists, attachments

What most people miss

    "preview it first"        every operation can dry-run before you commit
    "check Feishu on my end"  one command covers version, auth, identity, network
    "agenda and tasks, both"  a built-in combo, one line for today or this week
    "sync this folder up"     directory-level mirroring, no file-by-file uploads

If you remember one thing

    "handle this in Feishu for me, preview it first"
```

No file paths, no filenames, no provenance anywhere in the card. You want the capability, not its address.

More examples in [`example.md`](example.md).

## Pairs with skill-creator

```
skill-creator      create a skill, edit a skill
skill-onboarding   verify the first run afterwards, hand back one card
```

Build, run, card, then take whatever the card exposed back to the skill. A missing dependency, docs that disagree with the code, an ability nobody wrote down clearly. That is what the next round fixes.

Pairing is on by default. After skill-creator creates or edits something, run this before moving on.

The split is simple. Create, edit, and delete belong to skill-creator. Running and writing cards belong here. Scoring quality belongs to neither.

## Install

```bash
git clone https://github.com/yuzhang-zhong/skill-onboarding.git \
  ~/.workbuddy/skills/skill-onboarding
```

Point it at your own skills directory. Claude Code uses `~/.claude/skills/`. The state script is pure Python standard library, nothing to install.

## Configuration

```bash
python scripts/onboarding_state.py config                # show
python scripts/onboarding_state.py config set <key> <v>  # change
python scripts/onboarding_state.py config reset          # defaults
```

| Key | Default | Effect |
|---|---|---|
| `language` | `zh` | Card language, `zh` / `en` / `auto` |
| `auto_trigger` | `true` | Offer a card after a first run |
| `max_lines` | `40` | Line cap for one card |
| `family_max_lines` | `60` | Line cap for a family card |
| `exclude` | `[]` | Skills to skip |
| `pair_with_skill_creator` | `true` | Verify after a skill is created or edited |

Bad values are rejected on the spot. If things get messy, `config reset` puts everything back.

## Who it is for

| | Audience | Output |
|---|---|---|
| `skill-creator` | authors | create and iterate skills |
| `skill-tester` and friends | authors | structure checks, quality scores |
| **this skill** | **users** | **a card after the first run** |

Judging whether a skill is good is somebody else's job. This one only works out how you should use it.

## License

MIT.
