## ResearchClaws 安装指南

**此文档由 OpenClaw 代理读取，用于自动安装技能。**

---

### 自动安装（推荐）

对你的 OpenClaw 代理说：

```
帮我安装 ResearchClaws：https://raw.githubusercontent.com/syr-cn/ResearchClaws/main/docs/install.md
```

代理将自动执行以下步骤（无需手动操作）：

---

### 安装步骤（代理执行）

#### Step 1 — 确认 OpenClaw 已安装

```bash
openclaw --version
```

如果未安装，请先访问 https://openclaw.ai 安装 OpenClaw。

#### Step 2 — 安装技能文件

将 SKILL.md 下载到用户技能目录：

```bash
mkdir -p ~/.openclaw/skills/research-claws
curl -fsSL https://raw.githubusercontent.com/syr-cn/ResearchClaws/main/SKILL.md \
  -o ~/.openclaw/skills/research-claws/SKILL.md
```

#### Step 3 — 创建默认配置文件

```bash
cat > ~/.openclaw/workspace/research-claws-config.md << 'EOF'
# ResearchClaws 用户配置
# 编辑此文件来自定义你的论文推荐兴趣

## 研究兴趣（每行一个，用英文写效果更好）
INTERESTS:
  - large language models
  - reinforcement learning
  - agentic AI
  - retrieval-augmented generation
  - multimodal models

## 每日推荐设置
DAILY_COUNT: 5          # 每次推荐几篇（3-10）
DAYS_BACK: 3            # 查找最近几天的论文（1-7）
LANGUAGE: zh            # 摘要语言：zh（中文）或 en（英文）
EOF
```

#### Step 4 — 验证安装

安装完成后，测试技能是否正常工作：

```
推荐今日论文
```

或者：

```
帮我读一下这篇：https://arxiv.org/abs/2503.19823
```

---

### 手动安装

如果自动安装失败，手动步骤：

1. 下载 SKILL.md：https://raw.githubusercontent.com/syr-cn/ResearchClaws/main/SKILL.md
2. 保存到 `~/.openclaw/skills/research-claws/SKILL.md`
3. 重启 OpenClaw 代理

---

### 卸载

```bash
rm -rf ~/.openclaw/skills/research-claws
rm -f ~/.openclaw/workspace/research-claws-config.md
```

---

### 故障排除

| 问题 | 解决方法 |
|------|----------|
| 代理不识别"推荐今日论文" | 确认 SKILL.md 已在 `~/.openclaw/skills/research-claws/` 目录 |
| arXiv 无法访问 | 检查网络连接，代理会自动重试 |
| PDF 分析超时 | 代理会回退到仅分析摘要模式 |

---

项目主页：https://github.com/syr-cn/ResearchClaws  
在线 Demo：https://syr-cn.github.io/ResearchClaws/
