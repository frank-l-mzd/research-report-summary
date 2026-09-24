# research-report-summary

> An Agent Skill that turns research reports, PDFs, and investor-call transcripts into structured, decision-ready analysis.

**一个用于研报 / 投资者交流会纪要 / 行业报告 PDF 深度分析与结构化总结的 Agent Skill。**

[中文说明](#中文说明) · [Installation](#installation) · [Usage](#usage) · [Output format](#output-format)

---

## What it does

Instead of dumping a wall of text, this skill forces a repeatable analysis framework:

1. **Read** the full document (PDF, transcript, or web article)
2. **Cluster** the content into themes by *argument logic*, not document order
3. **Extract** the 3–5 highest-information verbatim judgements
4. **Output** a two-sided investment view — upside signals ✅ and risk factors ⚠️ — plus a directional conclusion
5. **Sanity-check** objectivity when the source has a stake in the conclusion

Built for equity/industry research workflows: earnings calls, investor days, sell-side reports, third-party industry studies, and long-form essays from company executives.

## Installation

This repository follows the standard Agent Skill layout — the skill body lives in [`SKILL.md`](./SKILL.md) at the repository root.

### Claude Code / Claude.ai

Copy the repository into your skills directory:

```bash
git clone https://github.com/frank-I-mzd/research-report-summary.git \
  ~/.claude/skills/research-report-summary
```

Or drop `SKILL.md` into `~/.claude/skills/research-report-summary/SKILL.md`.

### WorkBuddy

```bash
git clone https://github.com/frank-I-mzd/research-report-summary.git \
  ~/.workbuddy/skills/research-report-summary
```

### Other agent runtimes

Any runtime that supports the `SKILL.md` convention (frontmatter with `name` + `description`, Markdown body) can load this directly. The `description` field is what triggers auto-activation — keep it intact.

### Dependencies

PDF extraction uses [`pdfplumber`](https://github.com/jsvine/pdfplumber):

```bash
pip install pdfplumber
```

A simple text-based PDF can also be read with any native file-read tool — no dependency required.

## Usage

Once installed, just hand the agent a document and ask:

```
用 research-report-summary 分析这份 PDF：D:\path\to\report.pdf
```

```
Summarize this investor call transcript and give me an investment view.
```

The skill triggers on intent — *summarize*, *extract key points*, *analyze*, *investment recommendation* — when paired with a report, transcript, or research PDF.

## Output format

| Section | Content |
|---------|---------|
| **核心命题** | The document's central thesis in one paragraph |
| **N 大核心观点** | Theme clusters as a `维度 / 核心判断` table |
| **关键原声论断** | 3–5 highest-signal verbatim quotes with context |
| **投资建议 — 积极信号 ✅** | Upside factors, ordered by materiality |
| **投资建议 — 风险关注 ⚠️** | Risk factors, ordered by materiality |
| **总体判断** | Directional conclusion |

See [`examples/demo-earnings-call.md`](./examples/demo-earnings-call.md) for a full worked example.

## Design principles

- **Two-sided by construction.** Every output must carry both upside and risk. One-sided output is treated as a failure mode.
- **Quote, don't paraphrase, the load-bearing claims.** The verbatim sentence is the evidence.
- **Separate fact from inference.** Especially for single-source documents with a commercial or regulatory agenda.
- **Compress, don't truncate.** Colloquial transcripts get merged by topic, not cut mid-thought.
- **Flag low-confidence attributions.** When a report names specific countries, companies, or individuals, mark it as requiring third-party verification.

## Repository layout

```
.
├── SKILL.md                        # the skill (this is what gets loaded)
├── README.md                       # you are here
├── LICENSE                         # MIT
├── .gitignore
└── examples/
    └── demo-earnings-call.md       # worked example: input → output
```

## License

[MIT](./LICENSE) © 2026 frank-I-mzd

---

## 中文说明

### 它解决什么问题

把一份几十页的研报、交流会录音稿或行业报告，变成一份**能直接用于决策**的结构化分析——而不是一段没有重点的长文。

技能强制执行一套可复现的框架：

1. **读全文** — PDF / 录音稿 / 网页长文
2. **聚类** — 按**论证逻辑**分组，而不是按文档顺序罗列
3. **提取** — 挑出 3–5 条信息量最高的原声判断
4. **双向输出** — 积极信号 ✅ 与风险关注 ⚠️，缺一不可，最后给明确的方向性结论
5. **客观性校验** — 当信息源与结论存在利益关联时，强制标注

适用场景：业绩说明会、投资者交流日、券商研报、第三方行业研究、公司高管长文。

### 安装

```bash
# Claude Code
git clone https://github.com/frank-I-mzd/research-report-summary.git \
  ~/.claude/skills/research-report-summary

# WorkBuddy
git clone https://github.com/frank-I-mzd/research-report-summary.git \
  ~/.workbuddy/skills/research-report-summary
```

同时建议安装 PDF 解析依赖：

```bash
pip install pdfplumber
```

### 使用

安装后，直接把文档丢给 Agent 并说明意图即可：

```
用 research-report-summary 分析这份 PDF：D:\path\to\report.pdf
```

### 设计原则

- **天然双向** — 只有利好或只有风险，视为不合格输出
- **原声为证** — 承重结论直接引用原句，不做转述
- **事实与推断分离** — 对带商业或监管议程的单方报告尤其重要
- **压缩而非截断** — 口语内容按主题归并，不在半句话处切断
- **低置信度标注保留** — 报告自标"低/中"可信度的结论，保留其原始标注

### 更多

- 技能本体：[`SKILL.md`](./SKILL.md)
- 完整演示：[`examples/demo-earnings-call.md`](./examples/demo-earnings-call.md)
