# research-report-summary

**English** · [简体中文](./README.md)

> Turn research reports, PDFs, and investor-call transcripts into **structured, decision-ready** analysis.

An Agent Skill for equity and industry research workflows. The point is not to make long documents shorter — it is to turn them into **a checklist of judgements you can actually act on**.

---

## What it does

A 50-page sell-side report, a two-hour earnings call transcript, a 150-page industry study — what you retain afterwards is usually three or four points, scattered, with no counter-argument and no trackable verification signal. This skill enforces a repeatable framework:

1. **Read** the whole document — PDF, transcript, or long-form web article
2. **Cluster** the content by *argument logic*, not document order
3. **Extract** the 3–5 highest-information **verbatim judgements** — the quote is the evidence
4. **Output two-sided** — upside signals ✅ and risk factors ⚠️, **neither may be omitted**, closing with a directional conclusion
5. **Sanity-check objectivity** — when the source has a stake in the conclusion, it must be labelled, along with its confidence level

Built for: earnings calls, investor days, sell-side research, third-party industry studies, and long-form essays by company executives.

## Installation

The skill body is [`SKILL.md`](./SKILL.md) at the repository root, following the standard Agent Skill convention (frontmatter with `name` + `description`, Markdown body).

### Claude Code / Claude.ai

```bash
git clone https://github.com/frank-l-mzd/research-report-summary.git \
  ~/.claude/skills/research-report-summary
```

Or simply drop `SKILL.md` into `~/.claude/skills/research-report-summary/SKILL.md`.

### WorkBuddy

```bash
git clone https://github.com/frank-l-mzd/research-report-summary.git \
  ~/.workbuddy/skills/research-report-summary
```

### Other runtimes

Any runtime supporting the `SKILL.md` convention can load this directly. The `description` field is what triggers auto-activation — **keep it intact**.

### Dependencies

PDF extraction uses [`pdfplumber`](https://github.com/jsvine/pdfplumber):

```bash
pip install pdfplumber
```

A simple text-based PDF can also be read with the runtime's native file-read tool — no dependency required.

## Usage

Once installed, hand the agent a document and state your intent:

```
用 research-report-summary 分析这份 PDF：D:\path\to\report.pdf
```

```
Summarize this investor call transcript and give me an investment view.
```

The trigger is **intent** (summarize / extract key points / analyze / investment recommendation) paired with **material** (a report, transcript, or research PDF).

> The skill outputs in **Simplified Chinese by default**. Ask for English explicitly if you need it.

## Output format

| Section | Content |
|---------|---------|
| **Central thesis** | The document's core claim in one paragraph |
| **N core viewpoints** | Theme clusters as a `dimension / judgement` table |
| **Key verbatim judgements** | 3–5 highest-signal quotes with context |
| **Upside signals ✅** | Beneficial factors, ordered by materiality |
| **Risk factors ⚠️** | Risk factors, ordered by materiality |
| **Overall conclusion** | An explicit directional view |

See [`examples/demo-earnings-call.md`](./examples/demo-earnings-call.md) for a full worked example.

## Design principles

- **Two-sided by construction** — output with only upside, or only risk, is treated as a failure
- **Quote, don't paraphrase, the load-bearing claims** — the verbatim sentence is the evidence
- **Separate fact from inference** — especially for single-source documents with a commercial or regulatory agenda
- **Compress, don't truncate** — colloquial transcripts get merged by topic, never cut mid-thought
- **Preserve low-confidence labels** — if a report marks its own conclusion as low/medium confidence, keep that label
- **Flag named accusations** — claims naming specific countries, companies, or individuals must be marked as requiring third-party verification

## Repository layout

```
.
├── SKILL.md                        # the skill (this is what gets loaded)
├── README.md                       # Simplified Chinese README
├── README.en.md                    # this file
├── CHANGELOG.md                    # version history
├── PITFALLS.md                     # field-tested pitfalls, for self-checking
├── LICENSE                         # MIT
├── .gitignore
└── examples/
    └── demo-earnings-call.md       # full input-to-output worked example
```

## Version

Currently **v1.0.1**. See [`CHANGELOG.md`](./CHANGELOG.md). If you hit a problem, check [`PITFALLS.md`](./PITFALLS.md) first.

## License

[MIT](./LICENSE) © 2026 frank-l-mzd
