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

These three cards were actually produced. Not mock-ups. Reproduced as written.

### 1. You have 21 Feishu skills

You want a table. You bounce between `lark-sheets`, `lark-base`, and `lark-drive` trying to guess. You want to send a message and cannot tell whether that is `lark-im` or `lark-unified`. You have seen all 21 names and never worked out how they relate.

Run it once, and you get this:

```
✅ Working. The CLI itself is fine, every self-check passes. Two things to note: the embedded docs trail the binary by one version, and the app identity currently in effect isn't the one named in the config.

The whole Feishu suite. 26 domains, and your 21 local Feishu skills all sit on top of this one command.

What you can do

    Messages, groups     send, search history, create groups, add members, pin, SMS/call escalation
    Documents            create, read, insert images, search, restore versions
    Sheets               read/write cells, verify formulas, charts, pivot tables, conditional formatting, import/export
    Drive                upload, download, move, comments, permissions, two-way folder sync
    Calendar, meetings   agenda, free/busy, find rooms, suggest times, RSVP, transfer organizer
    Tasks                create, complete, remind, lists, search, attachments
    The rest             Wiki, slides, boards, approval, attendance, OKR, mail, all there

What most people miss

    "preview it, don't actually send"    every operation supports dry-run, see the result before you commit
    "check Feishu on my end"             one command covers version, auth, identity, network, and pinpoints what's wrong
    "agenda and tasks, both"             a built-in combo, one line for today or this week
    "publish this Markdown as a doc"     a full pipeline: import, upload images, move each one under its heading, add captions
    "sync this folder up"                directory-level mirroring and two-way sync, no file-by-file uploads
    "pivot table and conditional format" the sheets domain runs deeper than you would think

If you remember one thing

    "handle this in Feishu for me, preview it first"
```

One line is enough: 21 skills, one tool.

### 2. You installed a de-AI-flavor tool and forgot about it

You remember it can flag words like "仿佛", "一丝", "缓缓" in Chinese prose. What else? No idea. When you installed it, why you stopped, also no idea.

Run it once, and you get this:

```
⚠️ Partially working. The core scanner runs fine, but the skill is disabled and won't trigger on its own, and the follow-up formatting step its docs mention isn't in the package.

A de-AI-flavor tool for Chinese prose. Detection, grading, rewriting. Strong on rule sets, hundreds of banned words plus six named techniques. Weak on automation, most edits need a human call.

What you can do

    "scan these chapters"         quantified report: banned-word density, parallel-structure runs, psych-verb ratio, graded light/medium/heavy
    "make this not read like AI"  three passes: strip generic words, strip written-language tone, put the natural feel back
    "something's off, can't name it"    deep layer names the problem type and gives a master-prose fix

What most people miss

    "rewrite this the way Yu Hua would"    six techniques you can name: image instead of interiority, action externalising emotion, plain description over adjectives, setting carrying mood, absence writing presence, action carrying speech
    "what can it fix by itself"            punctuation runs, overused time-freezes, stacked light verbs and stock phrases get auto-fixed; context-sensitive patterns are reported only, so nothing good gets damaged
    "how do I actually turn it on"         enable it in skill management first, and read the result yourself after auto-fix

If you remember one thing

    "scan this for AI flavor, fix the heavy parts"
```

Line one does not cover for it: the skill is disabled, you have to enable it before it triggers.

### 3. You want a deck and do not know who to ask

`slides`, `design`, `design-system`, `ui-ux-pro-max`. All four look relevant. You picked `slides` at random, shipped something passable, and never checked the rest.

Run it once, and you get this:

```
✅ Working. The built-in lookup libraries check out, style, colour and industry libraries all return real results. Generation needs an external service key, not exercised here.

A whole design pipeline. Brand tone, colour and type, logos, business cards, decks, banners, social images. You have 7 design skills that look related; they're parts of one thing.

What you can do

    Brand tone, voice, guidelines        brand
    Colour, type and spacing scales      design-system
    Frontend interfaces                  ui-styling
    Aesthetic review, kill the AI look   impeccable
    Generate a full design system        ui-ux-pro-max, 12 domains × 21 stacks
    Logos, icons, banners                built into design
    Full corporate identity              built into design, 50 deliverables
    Decks and pitches                    built into design, with charts

What most people miss

    "what colours should a coffee shop use"    a searchable industry library gives palette, type, symbols, and what to avoid
    "give me a design brief first"             one line produces a full brief: direction, palette, type, industry conventions
    "what industries suit this style"          every style lists where it fits and where it doesn't
    "do the whole corporate identity"          a built-in end-to-end flow, 50 deliverables in one go
    "make it bolder"                           three dials: visual variance, motion intensity, visual density, 1 to 10 each

If you remember one thing

    "design a visual system for my brand, brief first"
```

Seven design skills in one table. That last line about the dials, you would never have guessed.

All three cards in full are in [`examples/`](examples/).

## What a card looks like

No decorative symbols, just structure:

```
<✅ Working ｜ ⚠️ Partially working, reason ｜ ❌ Could not verify, reason>
<One line: what it's good at, what it isn't>

What you can do
    action      what you get
    action      what you get

What most people miss
    phrase      why it's worth knowing
    phrase      why it's worth knowing

If you remember one thing
    the shortest phrase
```

Two or more skills in one group become a family card, and the second heading becomes a "what do you want to do" list, grouped by what you would actually say.

No file paths, no filenames, no provenance anywhere in a card. You want the capability, not its address.

Format details and more samples in [`example.md`](example.md).

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

The three cards above are the Chinese output, which is what this machine is configured for. Set `language` to `en` and you get the same cards in English.

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
