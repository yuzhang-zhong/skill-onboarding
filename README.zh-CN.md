<p align="center"><img src="assets/logo.jpg" alt="skill-onboarding 标志" width="144" /></p>

<div align="center">

# skill-onboarding

### skill 装好了，没发现的能力呢？

读完技能全文，跑一次低风险探测，把真正有用的发现收进一张用法卡。

**读 → 跑 → 卡 · 单技能 / 工具族 · Python 标准库**

[English](README.md) · **简体中文**

[安装试用](#安装试用) · [看一张真实卡片](#给你一张卡不是再写一本手册) · [配置](#配置) · [技能说明](SKILL.md)

</div>

![仓库现有 PDF 用法卡的节选排版：保留部分可用的验证警告，并展示两项容易忽略的能力](docs/pdf-card.svg)

很多 skill 靠名字和一句描述被发现。显眼的功能很容易用上，藏在正文和参考文件里的功能却很容易错过。skill-onboarding 不只看描述：它读全文，检查当前环境里哪些能力真的能跑，再给你下次可以直接说出口的用法。

它做的是**用法发现，不是质量打分**。状态脚本只负责记录和配置；阅读、探测与写卡由 Agent 完成。

## 安装试用

以 WorkBuddy 技能目录为例：

```bash
git clone https://github.com/yuzhang-zhong/skill-onboarding.git \
  ~/.workbuddy/skills/skill-onboarding
cd ~/.workbuddy/skills/skill-onboarding
python scripts/onboarding_state.py --help
```

换成宿主实际支持的技能目录即可，例如 Claude Code 使用 `~/.claude/skills/`。保留技能与脚本的相对位置。脚本需要 Python 3，不依赖 pip 包；目标技能可能需要另外安装依赖。技能加载和重载方式由宿主决定。

然后对 Agent 说：

> 对我刚用过的技能运行 skill-onboarding。读完全文，做一次安全的只读探测，给我一张卡，写出我可能没发现的能力。没能验证的部分请标清楚。

卡片默认使用中文。如需英文，在克隆目录中运行：

```bash
python scripts/onboarding_state.py config set language en
```

## 给你一张卡，不是再写一本手册

| 部分 | 回答什么 |
| --- | --- |
| 状态 + 一句话说明 | 可用、部分可用或未验证，原因是什么 |
| 能干什么 | 一个动作，可以得到什么 |
| 几个多半不知道的 | 哪句可复制的口令，能让你换一种用法 |
| 记不住就存这句 | 最短、最实用的一句 |

上图是**仓库现有 [PDF 卡片](examples/pdf.md)的节选排版**，不是新跑出来的测试，也不是产品界面截图。原记录里的限制同样重要：那次验证检查了核心命令，但没有安装 OCR 和格式转换的系统依赖。历史样例不证明这些工具在你现在的环境里全部可用。

<details>
<summary>展开查看节选原文</summary>

```text
⚠️ 部分可用。核心命令实测正常，50 个命令全部注册成功。OCR 和格式转换要另外装系统工具，本次没装。

几个多半不知道的

    这张纸是扫描件还是电子件    一条命令逐页判断，后面该走哪条路就不用猜了
    这两个版本的合同差在哪      直接对比两个 PDF 的结构和文字，出差异清单

记不住就存这句

    这个 PDF 帮我处理一下，先看看是电子件还是扫描件
```

</details>

### 三个已记录的案例

| 案例 | 容易漏掉的能力 | 证据边界 |
| --- | --- | --- |
| [编程助手](examples/claude-code.md) | 后台任务、子智能体、记忆与钩子 | 记录的是原验证环境，不代表所有 Agent 宿主 |
| [PDF 工具](examples/pdf.md) | 先分类型再操作；表单、脱敏、版本比较 | 当次未安装 OCR / 格式转换依赖 |
| [选股工具](examples/stock-screener.md) | 先圈定范围，再排序；多种查询入口 | 未配置行情服务时，仍需另接数据源 |

完整卡片保留在原文件中。它们展示的是卡片写法，本仓库并不附带这些 PDF、编程或金融工具，也不提供投资建议。

## 怎么工作

1. **定对象。** 一个 skill、一个功能很多的工具，或共用服务的一组 skill。
2. **读和探。** 读完整技能与相关参考文件名；按需选择低成本的只读帮助、状态、自检、dry-run 或假数据测试。
3. **出一张卡。** 分清验证成功与受阻的部分，用自然语言口令表达，写到一口气读完为止。

同一个工具拆成十几个 skill，不该再变成十几张互不相干的卡。工具族卡按「你想做什么」组织能力，再比较底层工具的能力清单与本地已封装的技能，找出漏掉的部分。前提是能读取能力清单；缺工具、缺权限的情况必须明说。

## 配置

在仓库目录运行，或使用脚本的完整路径：

```bash
python scripts/onboarding_state.py config
python scripts/onboarding_state.py config set <key> <value>
python scripts/onboarding_state.py config reset
```

| 键 | 默认 | 作用 |
| --- | --- | --- |
| `language` | `zh` | 卡片语言：`zh`、`en` 或 `auto` |
| `auto_trigger` | `true` | 首次使用后补一张卡 |
| `max_lines` | `40` | 单卡行数上限 |
| `family_max_lines` | `60` | 工具族卡行数上限 |
| `exclude` | `[]` | 跳过的技能 |
| `pair_with_skill_creator` | `true` | 建完、改完技能后补一次验证 |

脚本校验支持的配置值与类型。配置、状态和卡片位于 `~/.workbuddy/skill-onboarding/`，**即使技能安装在其他宿主目录，存储位置也不变**。自动触发和协同依赖兼容 Agent 遵循技能说明，本仓库不会安装后台守护进程。

### 避免反复引导

```bash
python scripts/onboarding_state.py check pdf
python scripts/onboarding_state.py list --json
python scripts/onboarding_state.py new
```

`check` 返回 `NEW`、`SEEN` 或 `SKIP`。流程先写卡，再用 `mark <skill-name>` 标记。`reset <skill-name>` 移除该技能的引导记录，`reset --all` 清空记录。所有命令支持 `--json`。状态脚本本身不会生成卡片。

## 与 skill-creator 配套

**建 / 改技能 → 安全验证 → 写卡 → 把发现反馈给技能。**

建、改、删归 skill-creator，首次运行验证和用法卡归这里。质量打分两边都不做。协同在默认配置中开启。

## 边界

- 优先只读探测与假数据。演示不是发送消息、下单、修改生产数据或公开私人资料的授权。
- 必须触达第三方或产生实质后果才能验证时，先停在准备好的请求，并标注未执行，除非宿主授权规则允许执行。
- 未验证不能写成「已验证」。区分缺依赖、环境问题与工具本身失败。
- 卡片只留使用者需要的信息，详细格式见 [`example.md`](example.md)。行数是上限，不是凑字数的指标。

## 许可证

[MIT](LICENSE)。
