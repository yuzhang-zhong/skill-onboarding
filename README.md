<div align="center">

<img src="assets/logo.jpg" alt="skill-onboarding logo" width="96" />

# skill-onboarding

**Discover what an installed skill can do in your environment.**

An Agent Skill and Python state helper (pairing with `skill-creator`) that runs a safe read-only probe right after you install or build a skill and hands back a concise one-page usage card of hidden capabilities and prompts.<br>
在刚安装好或用 `skill-creator` 建完 Agent Skill（技能）后自动做安全只读探测、挖掘文档隐藏功能与用法并生成一页「用法卡」的工具 Skill。

[![Python](https://img.shields.io/badge/Helper-Python_standard_library-3776AB)](scripts/onboarding_state.py)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

**English** · [简体中文](README.zh-CN.md)

[Install](#install-and-try-it) · [Usage card](#a-card-not-another-manual) · [Examples](#explore-the-three-recorded-examples) · [Configure](#configuration)

</div>

> **Quick answer:** Only using 10% of a newly installed AI skill? `skill-onboarding` is a meta-skill and Python state helper (pairing with `skill-creator`) that safely tests a newly installed or newly built skill in your setup with read-only probes and prints a short one-page **cheat sheet / usage card** of hidden features, advanced commands, and copyable example prompts. / 每次装完新的 AI 技能都只会用最表面的一两个功能？`skill-onboarding` 专门对新装或新建的技能做安全只读测试，把文档里藏着的进阶用法与隐藏命令总结成一页**速查卡片（用法卡）**。

Skills are often discovered through a name and a short description. That makes the obvious feature easy to find and the rest easy to miss. skill-onboarding reads beyond the description, checks what can actually run in the current environment, and gives you phrases you can use next time.

It is **usage discovery, not a quality score**. The state helper tracks onboarding and configuration; an agent performs the reading, probing, and card writing.

## Install and try it

Example for a WorkBuddy skills directory:

```bash
git clone https://github.com/yuzhang-zhong/skill-onboarding.git \
  ~/.workbuddy/skills/skill-onboarding
cd ~/.workbuddy/skills/skill-onboarding
python scripts/onboarding_state.py --help
```

Use your host's actual skills directory instead; for example, Claude Code uses `~/.claude/skills/`. Keep the scripts with the skill. The helper needs Python 3 and no pip dependencies; each target skill may have its own prerequisites. Host support and reload behavior vary.

Then ask your agent:

> Use skill-onboarding on the skill I just used. Read the full instructions, try a safe read-only probe, and give me one card with the useful capabilities I missed. Mark anything you could not verify.

The default card language is Chinese. For English cards, run this from the cloned directory:

```bash
python scripts/onboarding_state.py config set language en
```

<a id="a-card-not-another-manual"></a>
## The usage card

![Excerpt from the repository's recorded Chinese PDF usage card, including its partial-verification warning and two overlooked capabilities](docs/pdf-card.svg)

A card answers four questions:

| Part | What you learn |
| --- | --- |
| Status + short description | Working, partially working, or unverified, with the reason |
| What you can do | Actions and their useful outputs |
| What most people miss | Copyable phrases that reveal a different way to use the tool |
| If you remember one thing | The shortest useful prompt |

The illustration above is a **typeset excerpt of the existing [PDF card](examples/pdf.md)**, not a new test or a product screenshot. Its recorded warning is important: core commands were checked in that run, but OCR and conversion dependencies were not installed. Historical examples do not prove that those tools work in your environment today.

<details>
<summary>Read the excerpt in English</summary>

Translation of selected lines from the recorded card:

```text
Partially working. Core commands were tested; all 50 commands registered.
OCR and format conversion need additional system tools, not installed in that run.

What most people miss
    Is this a scan or a digital PDF?
    Classify each page first, then choose the right path.

    How do these two versions of the contract differ?
    Compare PDF structure and text to produce a change list.

If you remember one thing
    Help me handle this PDF. First check whether it is digital or scanned.
```

</details>

### Explore the three recorded examples

| Example | Hidden capability to look for | Evidence caveat |
| --- | --- | --- |
| [Coding assistant](examples/claude-code.md) | Background work, sub-agents, memory, and hooks | Records the original environment, not every agent host |
| [PDF tool](examples/pdf.md) | Classify before acting; forms, redaction, and version comparison | OCR / conversion prerequisites were not installed |
| [Stock screener](examples/stock-screener.md) | Narrow a universe, then rank; multiple query entry points | A separate market-data source is still needed in an unconfigured environment |

The full cards remain in their original files. They are examples of the output style, not bundled PDF, coding, or finance tools, and not investment recommendations.

## How it works

1. **Choose the scope.** One skill, one overloaded tool, or a family that shares a service.
2. **Read and probe.** Read the full skill and relevant reference filenames; try low-cost, read-only help, status, dry-run, or synthetic-input checks where appropriate.
3. **Write one card.** Separate verified and blocked capabilities, use natural-language prompts, and keep the result short.

A dozen skills for one tool should not become a dozen disconnected cards. A family card groups capabilities by what you want to accomplish, then looks for the gap between the underlying tool's capability list and locally wrapped skills. This comparison depends on an inspectable capability list; missing tools or permissions remain explicit limitations.

Full instructions: [`SKILL.en.md`](SKILL.en.md). The [probe boundaries](#boundaries) apply to both single-skill and tool-family cards.

## Configuration

Run from this repository's directory, or use the script's full path:

```bash
python scripts/onboarding_state.py config
python scripts/onboarding_state.py config set <key> <value>
python scripts/onboarding_state.py config reset
```

| Key | Default | Effect |
| --- | --- | --- |
| `language` | `zh` | Card language: `zh`, `en`, or `auto` |
| `auto_trigger` | `true` | Offer a card after a first run |
| `max_lines` | `40` | Single-card line cap |
| `family_max_lines` | `60` | Tool-family card line cap |
| `exclude` | `[]` | Skills to skip |
| `pair_with_skill_creator` | `true` | Verify after creating or editing a skill |

The script validates supported values and types. Configuration, state, and cards use `~/.workbuddy/skill-onboarding/`, **even if the skill itself is installed under another host's directory**. Auto-trigger and pairing are instructions for a compatible agent to follow, not a background daemon installed by this repository.

### Avoid repeat onboarding

```bash
python scripts/onboarding_state.py check pdf
python scripts/onboarding_state.py list --json
python scripts/onboarding_state.py new
```

`check` returns `NEW`, `SEEN`, or `SKIP`. The workflow writes a card before marking it with `mark <skill-name>`. Use `reset <skill-name>` to remove that onboarding record, or `reset --all` to clear the records. All commands support `--json`. The helper does not generate cards by itself.

## Pairs with skill-creator

**Create / edit → run a safe check → write the card → feed discoveries back into the skill.**

Creation, editing, and deletion belong to skill-creator. First-use verification and usage cards belong here. Quality scoring belongs to neither. Pairing is enabled in the default configuration.

## Boundaries

- Prefer read-only probes and synthetic data. Do not use a demonstration as permission to send messages, place orders, change production data, or expose private material.
- When verification would require a consequential external action, stop at a prepared request and label it unexecuted unless the host's authorization rules permit execution.
- Do not call an untested capability verified. Distinguish missing dependencies, environment problems, and tool failures.
- Keep cards brief and user-facing; detailed format guidance is in [`example.md`](example.md). No feature inventory needs to be padded to hit a line count.

## 中文简介

`skill-onboarding` 是一款面向 Claude Code、Codex、GitHub Copilot、Cursor 与 WorkBuddy 的**已安装 Agent Skill 能力发现与首跑验证工具**（与 `skill-creator` 配套组成「建 → 跑 → 卡 → 反馈」闭环）。当用户第一次用上某个 Skill 或刚用 `skill-creator` 建完/改完 Skill 后，它会通读完整说明文档、在当前环境中执行安全的只读探测命令，并生成一张精炼的**「用法卡」（Usage Card）**——标明可用/受限状态、容易被忽略的隐藏功能与可复制自然语言提示词，还能将同一底层 CLI 被拆散的多个子技能合并成一张工具族卡片。详见[简体中文说明](README.zh-CN.md)与 [`SKILL.md`](skills/skill-onboarding/SKILL.md)。

## License

[MIT](LICENSE).
