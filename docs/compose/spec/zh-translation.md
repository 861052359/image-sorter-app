---
feature: zh-translation
status: designed
updated: 2025-01-20
branch: zh-translation
commits:
---

# 中文翻译

## Report

## [S1] Problem
项目所有面向用户的文本（UI 字符串、README）均为英文，中文用户理解成本高。需要提供中文版本作为默认语言，同时保留英文版本。

## [S2] Design
- **Android 字符串**：`values/strings.xml` 改为中文（默认），`values-en/strings.xml` 保留英文。设备语言为中文时显示中文，其他语言显示英文。
- **README**：`README.md` 改为中文（默认），`README.en.md` 保留英文。GitHub 默认展示中文 README。
- **其他文档**：CHANGELOG、CONTRIBUTING、PRIVACY、SECURITY 保持英文，不翻译。

## [S3] Out of Scope
- 不翻译代码注释
- 不翻译其他文档（CHANGELOG、CONTRIBUTING、PRIVACY、SECURITY）
- 不修改应用逻辑或 UI 布局

## Tasks
- [ ] T1: 翻译 strings.xml 为中文 — acceptance: values/strings.xml 所有用户可见字符串为中文 (covers: S2)
- [ ] T2: 创建 values-en/strings.xml 英文版本 — acceptance: values-en/strings.xml 包含与 values/strings.xml 相同 key 的英文翻译 (covers: S2; depends: T1)
- [ ] T3: 翻译 README.md 为中文 — acceptance: README.md 为中文，内容完整 (covers: S2)
- [ ] T4: 创建 README.en.md 英文版本 — acceptance: README.en.md 包含与 README.md 相同结构的英文内容 (covers: S2; depends: T3)
- [ ] T5: 验证构建 — acceptance: ./gradlew :app:assembleDebug 成功 (covers: S2; depends: T1, T2)
