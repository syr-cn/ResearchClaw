---
name: research-claws
description: >
  Research assistant for paper discovery and reading notes. Use this skill when the user mentions:
  论文推荐, paper recommendation, arXiv, 读论文, paper notes, DNL, 推荐今日论文, 每日论文,
  帮我读一下, paper scout, 论文速读, 帮我安装 ResearchClaws, research claws, researchclaws.
  Two modes: (1) Daily Paper Scout — find and rank today's arXiv papers by user interests;
  (2) Paper Quick Notes — given an arXiv link, produce a structured reading note.
metadata:
  openclaw:
    homepage: https://github.com/syr-cn/ResearchClaws
    version: "1.0.0"
    author: syr-cn
---

# ResearchClaws — Agent Usage Guide

ResearchClaws has **two modes**. Choose based on the user's request:

| Trigger | Mode |
|---|---|
| "推荐今日论文" / "每日论文" / "paper scout" / daily cron | **Mode 1: Daily Paper Scout** |
| arXiv link / "帮我读一下" / "paper notes" / "论文速读" | **Mode 2: Paper Quick Notes** |

---

## ⚙️ User Config (read first)

Before running either mode, check if the user has set their research interests. Look for a config block in their message or in `~/.openclaw/workspace/research-claws-config.md`. If not found, use these **default interests**:

```
DEFAULT_INTERESTS:
  - large language models
  - reinforcement learning
  - agentic AI / AI agents
  - retrieval-augmented generation
  - multimodal models
```

If the user wants to customize, they can edit `~/.openclaw/workspace/research-claws-config.md` (see docs/config.md).

---

## Mode 1: Daily Paper Scout

**Goal**: Find today's top arXiv papers matching user interests. Output Top 5 with quick summaries.

### Step 1 — Fetch papers from arXiv

For each interest area, fetch recent papers using the arXiv API. Use `web_fetch` with this URL pattern:

```
http://export.arxiv.org/api/query?search_query=all:{KEYWORD}&sortBy=submittedDate&sortOrder=descending&max_results=20&start=0
```

Example keywords to search (adapt to user interests):
- `LLM+agent`
- `reinforcement+learning+reasoning`
- `retrieval+augmented+generation`
- `multimodal+language+model`

Fetch 2–3 keyword queries. Parse the XML response — each `<entry>` has:
- `<title>` — paper title
- `<author><name>` — first author
- `<summary>` — abstract
- `<id>` — arXiv URL (e.g., `http://arxiv.org/abs/2503.XXXXX`)
- `<published>` — date

**Only keep papers published in the last 3 days** (compare `<published>` to today's date).

### Step 2 — Score and rank

For each paper, score relevance (1–5) based on:
- How closely the title/abstract matches the user's interest areas
- Novelty signal words: "new", "novel", "propose", "outperform", "state-of-the-art", "benchmark"
- Penalize: "survey", "review", "analysis of existing" (lower priority)

### Step 3 — Output Top 5

Format the output exactly like this:

```
📚 今日论文推荐 | Daily Paper Scout
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🗓️ {DATE} | 基于你的兴趣: {INTEREST_TAGS}

1️⃣ **{Title}**
   👤 {First Author} et al.
   💡 {One-sentence summary in Chinese or English}
   🎯 Why relevant: {1 sentence reason}
   🔗 {arXiv URL}

2️⃣ ... (repeat for top 5)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💡 想深读某篇？发我链接说"帮我读一下" | Want deep notes? Send me the link!
```

### Cron setup (optional)

If the user wants daily delivery, they can set up a cron in OpenClaw:
- Time: 9:00 AM daily
- Prompt: "推荐今日论文"
- Channel: their preferred channel (Discord, Telegram, etc.)

---

## Mode 2: Paper Quick Notes

**Goal**: Given an arXiv paper URL or ID, produce a short structured reading note.

### Step 1 — Extract arXiv ID

From the user's message, extract the arXiv paper ID. Patterns to recognize:
- Full URL: `https://arxiv.org/abs/2503.XXXXX` → ID = `2503.XXXXX`
- PDF URL: `https://arxiv.org/pdf/2503.XXXXX` → ID = `2503.XXXXX`
- Bare ID: `2503.XXXXX`

### Step 2 — Fetch metadata

Use `web_fetch` to get the abstract page:
```
https://arxiv.org/abs/{ARXIV_ID}
```

Extract: title, authors, abstract.

### Step 3 — Analyze the PDF

Use the `pdf` tool to analyze the paper:
```
pdf: https://arxiv.org/pdf/{ARXIV_ID}
prompt: "Please extract: (1) the core motivation/problem being solved, (2) the key method or technical contribution in 2-3 sentences, (3) main quantitative results (numbers from experiments), (4) limitations or failure cases mentioned by the authors, (5) one-sentence takeaway."
```

### Step 4 — Output Quick Note

Format the output exactly like this:

```
📝 论文速读 | Paper Quick Notes
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📌 **{Title}**
👤 {Authors (first 3)} | 📅 {Year}
🔗 https://arxiv.org/abs/{ID}

🔍 **Motivation**
{1-2 sentences: what problem does this paper solve?}

⚙️ **Method**
{2-3 sentences: what is the key technical idea?}

📊 **Results**
{Key numbers / benchmark scores — be specific}

⚠️ **Limitations**
{What the paper admits it can't do well}

✨ **One-line Takeaway**
{The single most important thing to remember}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💾 Want to save this note? Say "保存笔记" | Say "推荐今日论文" for today's papers!
```

### Notes on PDF analysis

- If the PDF is very long (>50 pages), focus on: Abstract, Introduction, Method section headers, Results tables, Conclusion.
- If `pdf` tool times out, fall back to analyzing only the abstract from `web_fetch`.
- Keep the note SHORT. This is a quick digest, not a full review.

---

## Error Handling

- **arXiv API down**: Retry once with `https://arxiv.org/search/?query={KEYWORD}&searchtype=all&start=0`
- **PDF not accessible**: Use abstract-only mode, note it in output
- **No papers in last 3 days**: Extend to last 7 days and note it
- **User has no config**: Use defaults silently, mention at end: "💡 想定制推荐兴趣？编辑 research-claws-config.md"

---

## Install

This skill was installed from: https://raw.githubusercontent.com/syr-cn/ResearchClaws/main/docs/install.md

To install: tell your OpenClaw agent:
> 帮我安装 ResearchClaws：https://raw.githubusercontent.com/syr-cn/ResearchClaws/main/docs/install.md
