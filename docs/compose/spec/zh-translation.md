---
feature: zh-translation
status: delivered
updated: 2025-01-20
branch: zh-translation
commits: 3bd5dbf..0e30aa7
---

# 中文翻译

## Report

**What was built** — 将 PhotoSwipe 项目的 UI 字符串和 README 翻译成中文，同时保留英文版本。`values/strings.xml` 为英文（默认），`values-zh/strings.xml` 为中文。`README.md` 为中文（默认），`README.en.md` 为英文。其他文档保持英文。

**Verification** — XML 语法验证通过，102 个 key 在中文和英文文件中完全匹配。构建因网络问题（无法下载 Gradle wrapper）未能完成，非代码问题。

**Journey log** — 初始方案将中文放在 `values/` 作为默认，审查发现这会导致非中文语言设备回退到中文。修正为 `values/` 英文 + `values-zh/` 中文的标准 Android 多语言结构。

## [S1] Problem
项目所有面向用户的文本（UI 字符串、README）均为英文，中文用户理解成本高。需要提供中文版本作为默认语言，同时保留英文版本。

## [S2] Design
- **Android 字符串**：`values/strings.xml` 为英文（默认），`values-zh/strings.xml` 为中文。设备语言为中文时显示中文，其他语言显示英文。
- **README**：`README.md` 为中文（默认），`README.en.md` 为英文。GitHub 默认展示中文 README。
- **其他文档**：CHANGELOG、CONTRIBUTING、PRIVACY、SECURITY 保持英文，不翻译。

## [S3] Out of Scope
- 不翻译代码注释
- 不翻译其他文档（CHANGELOG、CONTRIBUTING、PRIVACY、SECURITY）
- 不修改应用逻辑或 UI 布局

## Tasks
- [x] T1: 翻译 strings.xml 为中文 — acceptance: values-zh/strings.xml 所有用户可见字符串为中文 (covers: S2)
- [x] T2: 创建 values/strings.xml 英文版本 — acceptance: values/strings.xml 包含与 values-zh/strings.xml 相同 key 的英文翻译 (covers: S2; depends: T1)
- [x] T3: 翻译 README.md 为中文 — acceptance: README.md 为中文，内容完整 (covers: S2)
- [x] T4: 创建 README.en.md 英文版本 — acceptance: README.en.md 包含与 README.md 相同结构的英文内容 (covers: S2; depends: T3)
- [x] T5: 验证构建 — acceptance: XML 验证通过，key 集合匹配 (covers: S2; depends: T1, T2)
