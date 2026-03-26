<div align="center">

# 🦞 ResearchClaws

**你的 AI 论文助手 | Your AI Research Companion**

*由 [OpenClaw](https://openclaw.ai) 驱动 · Powered by OpenClaw*

[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blue?style=flat-square)](https://openclaw.ai)
[![arXiv](https://img.shields.io/badge/arXiv-Free%20API-red?style=flat-square)](https://arxiv.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)
[![Demo](https://img.shields.io/badge/Demo-GitHub%20Pages-green?style=flat-square)](https://syr-cn.github.io/ResearchClaws/)

<br>

**每天 5 分钟，掌握最新 AI 进展。不需要 API Key，开箱即用。**

*Stay on top of AI research in 5 minutes a day. No API key needed. Works immediately.*

<br>

[🌐 在线演示 Demo](https://syr-cn.github.io/ResearchClaws/) · [📖 安装指南](#一句话安装) · [⚙️ 配置](docs/config.md) · [🐛 Issues](https://github.com/syr-cn/ResearchClaws/issues)

</div>

---

## ✨ 两大功能 | Two Features

<table>
<tr>
<td width="50%">

### 📚 每日论文推荐
**Daily Paper Scout**

每天自动从 arXiv 抓取最新论文，按你的研究兴趣排序，推送 Top 5。

- 🔍 覆盖 LLM、RL、多模态等方向
- 🎯 按相关度自动排分
- ⏰ 支持每日定时推送（9AM）
- 🆓 完全免费，基于 arXiv 公开 API

**触发方式：** 说 `推荐今日论文`

</td>
<td width="50%">

### 📝 论文速读笔记
**Paper Quick Notes**

发一个 arXiv 链接，30 秒内生成结构化阅读笔记。

- 📌 动机 · 方法 · 结果 · 局限
- 💡 一句话核心要点
- 📄 基于原始 PDF 智能分析
- 🇨🇳 中英双语友好

**触发方式：** 发 arXiv 链接 或 说 `帮我读一下这篇`

</td>
</tr>
</table>

---

## 🚀 一句话安装

把这句话发给你的 OpenClaw 代理：

```
帮我安装 ResearchClaws：https://raw.githubusercontent.com/syr-cn/ResearchClaws/main/docs/install.md
```

> **就这一句话。** 代理会自动下载安装，无需任何手动操作。

**没有 OpenClaw？** 先访问 [openclaw.ai](https://openclaw.ai) 安装，然后再运行上面这句话。

---

## 💬 快速上手 | Quick Start

安装完成后，直接跟代理说：

```
推荐今日论文
```

> 📚 今日论文推荐 | Daily Paper Scout
> ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
> 🗓️ 2026-03-26 | 基于你的兴趣: LLM · RL · Agents
>
> 1️⃣ **RLVR: Reinforcement Learning with Verifiable Rewards**
>    👤 Zhang et al.
>    💡 通过可验证奖励信号大幅提升 LLM 的数学推理能力
>    🎯 Why relevant: 直接结合 RL + LLM reasoning，核心方向
>    🔗 https://arxiv.org/abs/2503.XXXXX
> ...

---

```
帮我读一下这篇：https://arxiv.org/abs/2503.19823
```

> 📝 论文速读 | Paper Quick Notes
> ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
> 📌 **AutoRefine: Search and Refine During Think**
> 👤 Shi et al. | 📅 2025
> 🔗 https://arxiv.org/abs/2503.19823
>
> 🔍 **Motivation**
> LLM 在复杂推理任务中容易陷入错误路径...
>
> ⚙️ **Method**
> 在推理过程中动态触发搜索并对中间结果进行精炼...
>
> 📊 **Results** · 87.3% on MATH · 72.1% on HotpotQA
>
> ✨ **One-line Takeaway**: 推理时检索比推理后检索更有效

---

## 🎬 在线演示 | Live Showcase

访问 [syr-cn.github.io/ResearchClaws](https://syr-cn.github.io/ResearchClaws/) 查看完整演示：

| 案例 | 预览 |
|------|------|
| [每日信号简报](https://syr-cn.github.io/ResearchClaws/showcase/case1-daily-signal-brief.html) | 多源信号聚合每日推送 |
| [论文阅读笔记](https://syr-cn.github.io/ResearchClaws/showcase/case2-paper-reading-notes.html) | 结构化深度阅读笔记 |
| [研究方向分析](https://syr-cn.github.io/ResearchClaws/showcase/case3-research-proposal.html) | 自动生成研究方向建议 |
| [多智能体协作](https://syr-cn.github.io/ResearchClaws/showcase/case4-multi-agent-codebase.html) | Multi-agent 代码库分析 |

---

## ⚙️ 自定义兴趣方向

安装后，直接告诉代理：

```
我主要研究强化学习和多模态，帮我更新 ResearchClaws 配置
```

或手动编辑 `~/.openclaw/workspace/research-claws-config.md`：

```yaml
INTERESTS:
  - reinforcement learning
  - multimodal models
  - long context reasoning
DAILY_COUNT: 5
LANGUAGE: zh
```

详见 [配置指南](docs/config.md)

---

## 📦 设置每日自动推送

对代理说：

```
帮我设置每天早上 9 点自动推荐论文
```

代理会自动创建 OpenClaw cron 任务。✅

---

## 🔧 工作原理 | How It Works

```
用户: 推荐今日论文
  ↓
代理读取 SKILL.md（ResearchClaws 技能说明）
  ↓
调用 arXiv 公开 API（免费，无需 Key）
  ↓
按用户兴趣评分排序
  ↓
返回 Top 5 论文速览
```

```
用户: 帮我读一下 arxiv.org/abs/XXXXX
  ↓
代理提取 arXiv ID
  ↓
下载 PDF（内置 pdf 工具）
  ↓
智能提取：动机 · 方法 · 结果 · 局限
  ↓
输出结构化速读笔记（30秒内）
```

**零依赖**：只需 OpenClaw + 网络连接，不需要任何 API Key。

---

## 🤝 Credits

- 🦞 Built with [OpenClaw](https://openclaw.ai) — AI assistant platform
- 📄 Paper data from [arXiv](https://arxiv.org) (free open-access API)
- 🧠 Created by [@syr-cn](https://github.com/syr-cn) (Yaorui Shi, USTC)

---

## English Quick Reference

**Install** (one line, send to your OpenClaw agent):
```
帮我安装 ResearchClaws：https://raw.githubusercontent.com/syr-cn/ResearchClaws/main/docs/install.md
```

**Usage:**
- Daily papers: say `推荐今日论文` or `recommend today's papers`
- Quick notes: paste an arXiv link or say `帮我读一下 [link]`

**No API key needed.** Uses arXiv's free public API + OpenClaw's built-in PDF tool.

---

<div align="center">

Made with ❤️ for researchers · MIT License · [syr-cn.github.io/ResearchClaws](https://syr-cn.github.io/ResearchClaws/)

</div>
