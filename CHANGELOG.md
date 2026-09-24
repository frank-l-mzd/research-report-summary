# Changelog

本项目的所有重要变更都记录在此文件。

格式遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，
版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [Unreleased]

### Added

- 英文版 README（`README.en.md`），`README.md` 调整为中文主文件并增加语言切换入口

## [1.0.1] - 2026-09-24

### Added

- `CHANGELOG.md` —— 版本变更记录
- `PITFALLS.md` —— 实战踩坑清单，供自检对照

### Changed

- `SKILL.md` 增加「自检」章节，指向 `PITFALLS.md`

### Fixed

- README / LICENSE 中的 GitHub 用户名拼写（`frank-I-mzd` → `frank-l-mzd`）

## [1.0.0] - 2026-09-24

首次发布。

### Added

- `SKILL.md` —— 技能本体，五步工作流：
  1. 读取 PDF 全文（大文件优先落盘为 txt 后分段精读）
  2. 全文通读与主题聚类（按论证逻辑分组，而非文档顺序）
  3. 结构化输出（核心命题 / 主题聚类表 / 原声论断 / 双向投资建议 / 总体判断）
  4. 语言与风格规范（默认简体中文、善用表格、双向建议缺一不可）
  5. **客观性校验** —— 单方来源标注、点名指控需第三方交叉验证、保留原始置信度标注、区分事实与推断
- `README.md` —— 中英双语安装与使用说明
- `examples/demo-earnings-call.md` —— 完整「输入 → 输出」演示
- `LICENSE` —— MIT
- `.gitignore`

### Notes

- 移除了技能末尾残留的构建期指令段「清除非必要资源」（skill-creator 脚手架遗留，不应留在成品技能中）

<!--
版本号约定：
- Added / Changed / Deprecated / Removed / Fixed / Security 六类
- 新增能力（如新的输出章节、新的校验规则）→ MINOR
- 修正措辞、文档、拼写、示例 → PATCH
-->
