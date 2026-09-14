<p align="center">
  <strong>用户第一次用上某个 skill 之后，跑一次、给一张卡。</strong>
</p>

<p align="center">
  <a href="README.md" title="English">🇬🇧</a> ·
  <strong title="简体中文">🇨🇳</strong>
</p>

## 为什么需要它

Skill 是渐进加载的：会话开始时只有 `name` 和 `description` 进上下文，正文按需加载。

结果是**用户永远只用得到最显眼的 1–2 个功能**，文档里其余的部分等于不存在。

这个 skill 就干一件事：在用户第一次真正用上某个 skill 之后，**跑一次、看一眼、给一张卡。**

## 三步

1. **定对象** — 单个 skill，还是一组？
2. **探测** — 读全文 + 跑只读探针。真跑，不靠推理
3. **出卡** — 一张能一口气读完的用法卡

## 一组 skill 合并成一张

同一个命令行工具常被拆成十几个 skill —— 飞书有 21 个 `lark-*`，底层只对应一个 `lark-cli`。
逐个出卡等于制造碎片，用户照样拼不出全貌，所以合并成一张「能力地图」。

同时做差集：**工具支持的范围 − 本地已装的 skill**，差出来的就是用户完全不知道的能力。

## 卡片长什么样

```
✅ 可用。CLI 本体正常，自检全部通过。

飞书全家桶——一个命令覆盖 26 个业务域。你本地那 21 个飞书技能，底层都是它一个。

🧭 你想做什么

· 聊消息 / 管群  → 发消息、搜聊天记录、拉群、加群成员、置顶收藏、电话/短信加急
· 写文档        → 建文档、读内容、插图插文件、搜文档、历史版本回滚
· 做表格        → 读写单元格、公式校验、图表、透视表、条件格式、导入导出 Excel/CSV
...

💡 你可能不知道还能这样用

- 「先预览一下，别真发」→ 所有操作都支持预演模式，涉及发消息、改文档时能先看结果再决定
- 「你自查一下飞书这边有没有问题」→ 一条命令做全身体检：版本、授权、身份、网络
...

🔑 记不住就存这句

「飞书那边帮我……，先预览一遍」
```

全程**不出现任何文件路径、文件名、来源**。用户要的是能力，不是定位。

更多样例见 [`example.md`](example.md)。

## 与 skill-creator 是一对

```
skill-creator     →  建 / 改 skill
skill-onboarding  →  建完后跑一次真实验证，给一张用法卡
```

闭环是 **建 → 跑 → 卡 → 反馈**。用法卡暴露出来的问题（缺依赖、文档与实现不一致、能力没写清），
就是下一轮该改 skill 的地方。

## 安装

```bash
git clone https://github.com/yuzhang-zhong/skill-onboarding.git \
  ~/.workbuddy/skills/skill-onboarding
```

换成你自己的 skills 目录即可（Claude Code 用 `~/.claude/skills/`）。状态脚本只用 Python 标准库，零依赖。

## 配置

```bash
python scripts/onboarding_state.py config                # 查看
python scripts/onboarding_state.py config set <key> <v>  # 修改
python scripts/onboarding_state.py config reset          # 恢复默认
```

| 键 | 默认 | 作用 |
|---|---|---|
| `language` | `zh` | 卡片语言：`zh` / `en` / `auto` |
| `auto_trigger` | `true` | 首跑后是否自动补卡 |
| `max_lines` | `40` | 单卡行数上限 |
| `family_max_lines` | `60` | 族卡行数上限 |
| `exclude` | `[]` | 不引导的 skill |
| `pair_with_skill_creator` | `true` | 建 / 改完 skill 后自动补一次首跑验证 |

非法值当场拒绝，乱了就 `config reset` —— 写不坏。

## 定位边界

| | 面向 | 产出 |
|---|---|---|
| `skill-creator` | 作者 | 新建 / 迭代 skill |
| `skill-tester` 一类 | 作者 | 结构校验、质量分级 |
| **本 skill** | **使用者** | **首次使用后的用法卡** |

判"这个 skill 有没有用"是别人的事；这里只判**用户该怎么用**。

## 许可证

MIT。
