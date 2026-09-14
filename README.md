<p align="center">
  <img src="assets/logo.jpg" alt="skill-onboarding" width="200" />
</p>

<p align="center">
  <strong>However well a skill is written, you only ever use the first two lines.</strong>
</p>

<p align="center">
  Run it once. Dig out the rest.
</p>

<p align="center">
  <strong title="English">🇬🇧</strong> ·
  <a href="README.zh-CN.md" title="简体中文">🇨🇳</a>
</p>

## You have a pile of skills and use one of them

Skills don't load all at once. When a session starts, only the name and a one-line description make it into context. The rest of the file gets read later, and only if something actually matches. A skill can document eight features and you'll only ever touch the first two. The other six stay invisible.

That's the gap this skill closes. The first time you genuinely use a skill, it runs the thing for real, reads the whole file, and hands you a card covering the part you never found.

## Three steps

1. **Pick the target** one skill, or a group
2. **Probe** read it in full, run read-only probes. Real calls, not guesses
3. **Write the card** one card you can finish in a sitting

## A group of skills is usually one thing

One tool often gets split across a dozen skills. It goes the other way too: a single skill can hold fifty commands.

Split, and you're holding a dozen faces with no picture of the whole. Crammed into one file, you only remember the one path you use most. Both cost you. So they get merged into one card.

Then it subtracts. What the tool supports, minus what you already have installed. Whatever's left is the part you never knew about.

## Three real cases

The three cards below came out of real runs. Not mock-ups. Reproduced word for word.

### 1. You use a coding assistant every day and only two of its features

Edit code, run commands. That's it. It can also run jobs in the background, spin up sub-agents, compact its own context, and fire scripts on hooks. You never touched any of that, because the description doesn't mention it.

Run it once and you get this:

```
✅ Working. Core capabilities all verified: context compaction, sub-agents, memory files, hooks.

The coding assistant you're already in. Most people use two things: edit code, run commands. The rest (background jobs, parallel sub-agents, automatic context compaction, scripts that fire on set moments) rarely gets touched.

What you can do

    Edit code, run commands     the basics, you use these daily
    Run long jobs in the background     builds, installs, test runs — no waiting, you get notified
    Parallel sub-agents     several directions at once, independent context, no crowding the main one
    Compact context automatically     it tidies up before hitting the ceiling; long sessions don't break
    Write memory files     project conventions and your preferences on disk, loaded into the next session
    Hooks     scripts that fire at set moments: pre-commit checks, auto-format after an edit

What most people miss

    "run this in the background, tell me when it's done"     no babysitting a long command
    "send three agents at this in parallel"     parallel exploration, far faster than one at a time
    "remember this rule for the project"     write it to memory, stop repeating yourself
    "walk me through this project's conventions"     reads memory and config, states it once
    "run the tests automatically after every edit"     hooks, for anything you keep doing by hand
    "context is getting full, clean it up"     trigger compaction yourself instead of waiting

If you remember one thing

    "run this in the background and ping me when it's done"
```

The last line alone is worth the whole card. Nobody made you sit and wait.

### 2. You treat the PDF skill as a text reader

You've used it to pull text and convert pages to images. Then what? Nothing. You assumed "reading" was the whole of it, so tables, forms and redaction never crossed your mind as its job.

Run it once and you get this:

```
⚠️ Partially working. Core commands verified, all 50 registered. OCR and format conversion need system tools installed separately, not done here.

An all-in-one PDF tool. 50 commands in six groups: read, edit, convert, forms, encrypt, structure. You thought it read text. It also edits scans, fills forms, redacts, and diffs two versions.

What you can do

    Read           text, tables, images, formulas, layout, reading order
    Edit           replace, add, delete text; swap images — both text-layer and pure scans
    Convert        to and from Word / HTML / Markdown / images, plus compress, split, merge, crop, rotate
    Forms          detect fields, fill fields, fill coordinate-based ones with no fields at all, then flatten
    Encrypt        password on, password off, redact, stamp a signature
    Structure      export to JSON for the full picture, rebuild from it, diff two versions

What most people miss

    "is this page a scan or a real PDF"     one command, per page — tells you which path to take
    "stitch these pages into one long image"     fixed-height screenshots, chat archives, social posts
    "chunk this for my AI"     four strategies — paragraph, page, fixed, semantic — built for retrieval
    "black out the ID numbers"     by text, by region, or by regex; clears the text layer underneath too
    "what changed between these two contracts"     diffs structure and text of two PDFs into a change list
    "don't let anyone edit this filled form"     one flatten, fields and annotations baked into the page

If you remember one thing

    "handle this PDF — check first whether it's a real PDF or a scan"
```

Line two gives it away: 50 commands. The first buried capability tells you to classify before acting, which plenty of people get backwards.

### 3. You only know one way to screen stocks

You know it can "find me some stocks", so you write conditions. The four other entry points (strategies, labels, events, rankings) and several hundred ready-made categories have been sitting there the whole time.

Run it once and you get this:

```
⚠️ Partially working. All six query entry points verified, every `--list` returns real results. Without a market data service wired up, results need another source.

Screens stocks and funds across the whole market. You thought it was "find me some stocks". It has six screening modes, each with hundreds to thousands of parameters. Most people know one of them.

What you can do

    By condition     write an expression, e.g. PE under 20 and ROE over 15
    By strategy      ready-made signals: golden cross, oversold, master strategies, candlestick patterns
    By label         central SOEs, below-book, recent IPOs, thousand-yuan stocks — hundreds of categories
    By event         unlocking soon, buying back, joining an index — dozens of event types
    By ranking       score, limit-up, margin, capital flow leaderboards — and rank within a subset
    Funds            the same two entry points, switched to ETFs: theme pools and size rankings

What most people miss

    "highest-scoring central SOEs"     narrow the universe, then sort — its most useful move, barely known
    "lowest valuation among golden crosses"     re-rank inside a strategy result, no manual re-filtering
    "what's unlocking soon"     events find a stock pool; a calendar finds dates. Different things
    "margin up five days straight"     a threshold, not a top-N cut. Different business meaning entirely
    "where does this valuation sit historically"     percentile rankings for funds beat absolute numbers
    "what did this look like last week"     query a historical date, or a range, to see a list change

If you remember one thing

    "screen me some stocks by condition — show me what conditions exist first"
```

"Narrow the universe, then sort" is the classic buried capability: it's in the docs, but nobody reads that section.

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

When two or more skills belong together, you get a family card instead. The second heading turns into a list of what you might want to do, grouped by how you'd actually ask for it.

No file paths, no filenames, no provenance anywhere in a card. You want the capability, not its address.

Format details and more samples in [`example.md`](example.md).

## Pairs with skill-creator

```
skill-creator      create a skill, edit a skill
skill-onboarding   verify the first run afterwards, hand back one card
```

Build, run, card, then take whatever the card exposed back to the skill. A missing dependency. Docs that disagree with the code. An ability nobody wrote down clearly. That's what the next round fixes.

Pairing is on by default. After skill-creator creates or edits something, run this before moving on.

The split is simple. Creating, editing, and deleting belong to skill-creator. Running and writing cards belong here. Scoring quality belongs to neither.

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

Those three cards above are in Chinese, because that's what this setup is configured for. Set `language` to `en` and you get English cards instead.

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
