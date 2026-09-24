# research-report-summary

[English](./README.en.md) · **简体中文**

> 把研报、PDF、投资者交流会纪要，变成**结构化、可直接用于决策**的分析报告。

一个面向研报 / 交流会纪要 / 行业报告 PDF 的 Agent Skill（技能）。它的目标不是"把长文变短"，而是**把长文变成一张能拿去决策的判断清单**。

---

## 它解决什么问题

几十页的研报、两小时的电话会录音稿、一百多页的行业报告——读完记住的往往只有三五个点，而且散落各处、没有对立面、没有可跟踪的验证指标。这个技能强制执行一套可复现的分析框架：

1. **读全文** —— PDF、录音稿、网页长文
2. **聚类** —— 按**论证逻辑**分组，而不是按文档顺序罗列
3. **提取** —— 挑出 3–5 条信息量最高的**原声判断**，原句为证
4. **双向输出** —— 积极信号 ✅ 与风险关注 ⚠️ **缺一不可**，最后给明确的方向性结论
5. **客观性校验** —— 信息源与结论存在利益关联时，强制标注单方来源与置信度

适用场景：业绩说明会、投资者交流日、券商研报、第三方行业研究、公司高管长文。

## 安装

技能本体是仓库根目录的 [`SKILL.md`](./SKILL.md)，遵循标准 Agent Skill 约定（frontmatter 含 `name` + `description`，正文为 Markdown）。

### Claude Code / Claude.ai

```bash
git clone https://github.com/frank-l-mzd/research-report-summary.git \
  ~/.claude/skills/research-report-summary
```

也可以只把 `SKILL.md` 放到 `~/.claude/skills/research-report-summary/SKILL.md`。

### WorkBuddy

```bash
git clone https://github.com/frank-l-mzd/research-report-summary.git \
  ~/.workbuddy/skills/research-report-summary
```

### 其他运行时

任何支持 `SKILL.md` 约定的运行时都能直接加载。`description` 字段是自动触发的依据，**请勿删改**。

### 依赖

PDF 解析用 [`pdfplumber`](https://github.com/jsvine/pdfplumber)：

```bash
pip install pdfplumber
```

纯文本型 PDF 也可以用运行时自带的文件读取工具直接读，无需依赖。

## 使用

装好后，把文档交给 Agent 并说明意图即可：

```
用 research-report-summary 分析这份 PDF：D:\path\to\report.pdf
```

```
把这份投资者交流会录音稿总结一下，并给出投资建议。
```

触发条件是**意图**（总结 / 提炼要点 / 分析 / 投资建议）加上**材料**（研报、纪要、PDF）。

## 输出格式

| 章节 | 内容 |
|------|------|
| **核心命题** | 一句话概括全文主张 |
| **N 大核心观点** | 主题聚类的 `维度 / 核心判断` 表格 |
| **关键原声论断** | 3–5 条信息量最高的原句，附上下文 |
| **投资建议 — 积极信号 ✅** | 按重要性排序的利好因素 |
| **投资建议 — 风险关注 ⚠️** | 按重要性排序的风险因素 |
| **总体判断** | 明确的方向性结论 |

完整演示见 [`examples/demo-earnings-call.md`](./examples/demo-earnings-call.md)。

## 设计原则

- **天然双向** —— 只有利好或只有风险，视为不合格输出
- **原声为证** —— 承重结论直接引用原句，不做转述
- **事实与推断分离** —— 对带商业或监管议程的单方报告尤其重要
- **压缩而非截断** —— 口语内容按主题归并，不在半句话处切断
- **低置信度标注保留** —— 报告自标"低/中"可信度的结论，保留其原始标注
- **点名指控需交叉验证** —— 涉及具体国家、公司、个人的指控，必须标注需第三方核实

## 仓库结构

```
.
├── SKILL.md                        # 技能本体（会被加载的就是这个文件）
├── README.md                       # 本文件（简体中文）
├── README.en.md                    # English README
├── CHANGELOG.md                    # 版本变更记录
├── PITFALLS.md                     # 踩坑清单（自检时对照）
├── LICENSE                         # MIT
├── .gitignore
└── examples/
    └── demo-earnings-call.md       # 完整「输入 → 输出」演示
```

## 版本

当前 **v1.0.1**，变更详见 [`CHANGELOG.md`](./CHANGELOG.md)。使用中发现问题，先对照 [`PITFALLS.md`](./PITFALLS.md) 自检。

## License

[MIT](./LICENSE) © 2026 frank-l-mzd
