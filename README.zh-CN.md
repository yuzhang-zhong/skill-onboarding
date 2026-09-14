<p align="center">
  <img src="assets/logo.jpg" alt="skill-onboarding" width="200" />
</p>

<p align="center">
  <strong>skill 第一次用完之后，跑一遍，给一张卡。</strong>
</p>

<p align="center">
  <a href="README.md" title="English">🇬🇧</a> ·
  <strong title="简体中文">🇨🇳</strong>
</p>

## 装了一堆 skill，然后只用最显眼那一个

这事怪不到你头上。

skill 是渐进加载的。会话开始时，它只把名字和描述带进来，正文要等匹配上才读。于是文档里写了八个功能，你只会碰上最前面那两个。剩下六个，你根本不知道它们存在。

这个 skill 就干一件事：第一次真用上某个 skill 之后，跑一遍，看一眼，给你一张卡。卡上写的是你大概率不知道的那部分。

## 三步

1. **定对象** 一个 skill，还是一组
2. **探测** 读全文，跑只读探针。真跑，不猜
3. **出卡** 一张能一口气读完的卡

## 一组 skill，其实是同一件事

飞书那 21 个技能，底层是一个命令。设计那 7 个，是一个东西的不同部位。

逐个出卡没用。你会收到 21 张碎片，还是拼不出全貌。所以合并成一张。

顺便算个差集：工具本身支持的，减去你本地已经装的。差出来的，就是你完全不知道的部分。

## 三个真实场景

### 一、你有 21 个飞书技能

<table>
<tr>
<td width="50%">

**跑之前**

要做个表格，你翻了半天，在 `lark-sheets`、`lark-base`、`lark-drive` 之间来回试。

想发个消息，不确定走 `lark-im` 还是 `lark-unified`。

这 21 个名字你都见过，但从来没搞清楚谁管谁。

</td>
<td width="50%">

**跑之后**

一张卡。

开头一句：这 21 个底下是一个 `lark-cli`，26 个域。

然后你才知道，它还管着思维笔记、斜杠命令，本地根本没对应技能，但直接说就能用。还知道所有操作都能先预演一遍再决定发不发。

</td>
</tr>
</table>

### 二、你装过一个去 AI 味的工具，然后就忘了

<table>
<tr>
<td width="50%">

**跑之前**

你记得它能在文本里挑出"仿佛""一丝""缓缓"这类词。

别的呢？想不起来了。

它是什么时候装的、为什么后来没用过，也记不清。

</td>
<td width="50%">

**跑之后**

第一行先告诉你实话：这技能是停用状态，得先启用才会自动触发。

然后你发现它还藏着六套大师手法，可以点名指定，"按余华的路子改这段"。

还知道哪些能自动改，哪些必须人工判断，不用一个个试。

</td>
</tr>
</table>

### 三、你想做个 PPT，但不知道找谁

<table>
<tr>
<td width="50%">

**跑之前**

`slides`、`design`、`design-system`、`ui-ux-pro-max`，四个都沾边。

你随手挑了 `slides`，做了个能看的版本。至于另外三个是不是更合适，你懒得查。

</td>
<td width="50%">

**跑之后**

一张卡把七个设计技能理成一张表：定调性找 `brand`，配颜色字号找 `design-system`，做 Logo 和 PPT 是 `design` 自带。

还告诉你 `ui-ux-pro-max` 能调三个旋钮，视觉变化度、动效强度、视觉密度，各十档。这个你原本绝对猜不到。

</td>
</tr>
</table>

## 卡片长什么样

```
可用。CLI 本体没问题，自检全过。

飞书全家桶。26 个业务域，你本地那 21 个飞书技能，底层都是它一个。

能干什么

    聊消息、管群   发消息、搜记录、拉群、加急
    写文档        建文档、读内容、插图、搜文档、回滚
    做表格        读写单元格、公式校验、图表、透视表、导入导出
    管云盘        上传下载、复制移动、评论、协作权限、双向同步
    排日程、开会   看日程、查忙闲、找会议室、智能推荐时间
    记待办        建任务、标完成、提醒、清单、附件

几个多半不知道的

    先预览，别真发      所有操作都能先跑一遍看结果
    自查一下飞书        一条命令查版本、授权、身份、网络
    日程和待办一起给我   一句话出当天或本周的安排
    整个文件夹同步上去   目录级镜像，不用一个个传

记不住就存这句

    飞书那边帮我……，先预览一遍
```

卡里不该出现文件路径、文件名、来源。你要的是能干什么，不是它在哪。

更多样例在 [`example.md`](example.md)。

## 和 skill-creator 是一对

```
skill-creator      建 skill、改 skill
skill-onboarding   建完之后跑一遍，验证第一次运行，给一张卡
```

建，跑，出卡，然后拿卡上暴露的问题回去改 skill。缺依赖、文档和实现对不上、能力没写清楚，都是这一轮该修的。

默认开着协同。用 skill-creator 建完或者改完一个 skill，接着跑一遍这个，别建完就走。

分工也简单：建改删归 skill-creator，跑和出卡归这里，质量打分两边都不做。

## 安装

```bash
git clone https://github.com/yuzhang-zhong/skill-onboarding.git \
  ~/.workbuddy/skills/skill-onboarding
```

换成你自己的 skills 目录就行，Claude Code 用 `~/.claude/skills/`。状态脚本只用 Python 标准库，不用装东西。

## 配置

```bash
python scripts/onboarding_state.py config                # 查看
python scripts/onboarding_state.py config set <key> <v>  # 修改
python scripts/onboarding_state.py config reset          # 恢复默认
```

| 键 | 默认 | 作用 |
|---|---|---|
| `language` | `zh` | 卡片语言，`zh` / `en` / `auto` |
| `auto_trigger` | `true` | 首跑后是否自动补卡 |
| `max_lines` | `40` | 单卡行数上限 |
| `family_max_lines` | `60` | 族卡行数上限 |
| `exclude` | `[]` | 不引导的 skill |
| `pair_with_skill_creator` | `true` | 建完改完 skill 后自动补一次验证 |

填错的值当场拒绝，实在乱了 `config reset` 回到默认，写不坏。

## 谁该用它

| | 面向 | 产出 |
|---|---|---|
| `skill-creator` | 作者 | 新建、迭代 skill |
| `skill-tester` 一类 | 作者 | 结构校验、质量分级 |
| **本 skill** | **使用者** | **首次使用后的用法卡** |

判断一个 skill 好不好用是别人的事。这里只管你该怎么用它。

## 许可证

MIT。
