# PhotoSwipe

> Tinder 风格的四向滑动照片整理工具，几分钟内清理多年积累的相册。

<p align="center">
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-22D3EE"></a>
  <img alt="Platform: Android" src="https://img.shields.io/badge/platform-Android%208%2B-3DDC84">
  <img alt="Language: Kotlin" src="https://img.shields.io/badge/language-Kotlin-7F52FF">
  <img alt="UI: Jetpack Compose" src="https://img.shields.io/badge/UI-Jetpack%20Compose-4285F4">
  <img alt="Material 3" src="https://img.shields.io/badge/Material%20You-EAB308">
  <a href="PRIVACY.md"><img alt="Privacy: 100% local" src="https://img.shields.io/badge/privacy-100%25%20local-0EA5E9"></a>
</p>

<p align="center">
  <a href="README.en.md">English</a>
</p>

PhotoSwipe 是一款开源的 Android 应用，将相册清理变成令人满意的卡片堆叠滑动游戏。相册中的每张照片就是一张卡片。向四个方向滑动以**删除**、**保留**、**收藏**或**移动到自定义文件夹**，然后继续下一张。删除操作会批量处理，Android 每批只要求确认一次，而不是每张照片都确认。

项目刻意保持精简、依赖轻量、100% 本地运行——无账户、无分析、无网络请求。

---

## 目录

- [功能](#功能)
- [滑动操作说明](#滑动操作说明)
- [界面截图](#界面截图)
- [安装](#安装)
- [从源码构建](#从源码构建)
- [配置](#配置)
- [权限](#权限)
- [架构](#架构)
- [项目结构](#项目结构)
- [常见问题](#常见问题)
- [路线图](#路线图)
- [参与贡献](#参与贡献)
- [隐私](#隐私)
- [安全](#安全)
- [许可证](#许可证)

---

## 功能

- **四向滑动手势**，带颜色编码的拖动覆盖层，随手势增长并锁定到主轴。
- **批量删除** — 左滑照片进入队列，每批提交一次 Android 删除请求（默认 10 张，可配置 1–50）。
- **应用管理的文件夹** — 按名称创建新相册文件夹，无需 SAF 选择器，无需权限操作。新文件夹出现在 `Pictures/PhotoSwipe/<name>/`（或 `DCIM/PhotoSwipe/<name>/`），在所有相册应用中可见。
- **内部收藏文件夹**，首次启动时自动创建，上滑立即可用。
- **安静的撤销药丸** — 不再每次滑动都弹出 snackbar。每次滑动后滑入一个临时药丸，3.5 秒后自动消失。
- **长按预览** — 按住卡片可在提交前全屏查看照片。
- **会话统计** — 队列清空时，显示本次会话中删除、保留、收藏和分类的照片数量。
- **日期范围和排序过滤**，专注于重要内容：最新、最早、最大、最小、随机或固定时间窗口。
- **Material 3 + 动态颜色**（Android 12+），支持手动系统/浅色/深色覆盖和 Material You 壁纸颜色开关。
- **主题单色图标**，适用于 Android 13+ 主题图标系统设置。
- **边缘到边缘 UI**，在所有设备上正确处理状态栏/导航栏内边距。
- **平板和横屏友好** — 卡片堆叠宽度受限，不会过度拉伸。
- **预测性返回手势**支持（Android 13+）。
- **备份感知** — 云备份和设备迁移保留设置和文件夹列表，但不保留每次会话的已审阅状态。
- **无障碍** — 支持 TalkBack 的卡片语义，可选的**减少动画**开关。
- **细粒度设置**：触觉反馈、方向提示、元数据叠加、拖动灵敏度、卡片堆叠深度、批次大小、文件夹根目录。
- **隐私优先**：无互联网权限、无分析、无崩溃报告器、无追踪。见 [PRIVACY.md](PRIVACY.md)。
- **重置所有内容**，随时从设置恢复默认值。

## 滑动操作说明

| 方向 | 操作 |
| ---- | ---- |
| ← 左 | 将照片加入删除队列。批次填满时出现 Android 删除提示。 |
| → 右 | 保留照片并标记为已审阅，下次会话不再出现。 |
| ↑ 上 | 将照片复制到**收藏**文件夹。 |
| ↓ 下 | 打开底部文件夹选择器；将照片移动到所选文件夹。 |

阈值（默认 96 dp）和活动卡片下方的预览卡片数量均可在设置中调整。

## 界面截图

截图将在后续版本中添加。目前，应用内界面包含三个标签页：

- **滑动** — 全屏卡片堆叠，带进度条、待删除横幅和撤销药丸。
- **文件夹** — 已管理文件夹列表，支持创建、重命名、删除、标记收藏和标记默认向下操作，以及添加新文件夹的 FAB。
- **设置** — 分组、图标着色的行，用于筛选、行为、存储、外观、数据和关于。

## 安装

从 [**Releases**](https://github.com/Leonxlnx/image-sorter-app/releases/latest) 页面获取最新预构建 APK：

- **[`PhotoSwipe-v1.3.1-release.apk`](https://github.com/Leonxlnx/image-sorter-app/releases/download/v1.3.1/PhotoSwipe-v1.3.1-release.apk)** — 推荐用于侧载。包名 `com.leonxlnx.imagesorter`，使用仓库稳定的 `distribution` 密钥签名，同时支持 APK 签名方案 v1 + v2 + v3，可在 Samsung、OnePlus、Xiaomi 等仍要求 JAR (v1) 签名的设备上正常安装。
- **[`PhotoSwipe-v1.3.1-debug.apk`](https://github.com/Leonxlnx/image-sorter-app/releases/download/v1.3.1/PhotoSwipe-v1.3.1-debug.apk)** — 调试版本（`com.leonxlnx.imagesorter.debug`），用于开发。

F-Droid 元数据包含在 [`fastlane/metadata/android/en-US/`](fastlane/metadata/android/en-US/) 下，PhotoSwipe 已准备好提交到 F-Droid 目录。

> **Samsung 注意：** 如果安装失败并提示"Package appears to be invalid"或"App not installed"，请检查**设置 → 安全和隐私 → Auto Blocker** 并禁用它。Samsung 的 Auto Blocker 在 One UI 6+ 上默认启用，会阻止所有侧载 APK，无论签名如何。

侧载步骤：

1. 从上面的链接下载 APK 到手机。
2. 点击文件，如果提示允许浏览器/文件管理器的"安装未知应用"。
3. 首次启动时，授予照片访问权限（`READ_MEDIA_IMAGES`，如果选择视频则还需 `READ_MEDIA_VIDEO`）。

目前不提供 Google Play 版本；建议从源码构建。

## 从源码构建

### 前置条件

- JDK 17（Temurin、OpenJDK 或 Zulu）
- Android SDK，已安装 platform 34 和 build-tools 34
- ANDROID_HOME / ANDROID_SDK_ROOT 指向 SDK 目录
- Android 8.0（API 26）或更高版本的设备或模拟器

### 构建调试 APK

```bash
git clone https://github.com/Leonxlnx/image-sorter-app.git
cd image-sorter-app
./gradlew :app:assembleDebug
```

生成的 APK 位于 `app/build/outputs/apk/debug/app-debug.apk`。

### 代码检查和测试

```bash
./gradlew :app:lintDebug
./gradlew :app:testDebugUnitTest    # 如果添加了单元测试
```

### 安装到已连接设备

```bash
./gradlew :app:installDebug
```

## 配置

所有选项位于**设置**下。每个部分反映一个独立关注点：

| 部分 | 可调内容 |
| ---- | -------- |
| **筛选** | 日期范围（全部、今天、7 天、30 天、一年）、排序方式、包含视频、跳过已审阅 |
| **行为** | 删除批次大小、拖动灵敏度、卡片堆叠深度、触觉反馈、方向提示、元数据叠加、减少动画 |
| **存储** | 文件夹根目录（`Pictures/PhotoSwipe` 或 `DCIM/PhotoSwipe`） |
| **外观** | 主题（系统/浅色/深色）、Material You 动态颜色开关 |
| **数据** | 重置已审阅列表、重置所有设置 |
| **关于** | 版本、许可证信息、GitHub 仓库链接 |

设置通过 Jetpack DataStore（`Preferences`）持久化。

## 权限

PhotoSwipe 只请求所需的权限。

| 权限 | 用途 |
| ---- | ---- |
| `READ_MEDIA_IMAGES`（Android 13+） | 读取相册中的照片 |
| `READ_MEDIA_VIDEO`（Android 13+，可选） | 仅在启用"包含视频"时需要 |
| `READ_EXTERNAL_STORAGE`（Android ≤ 12） | 读取 MediaStore 的旧版回退 |
| `WRITE_EXTERNAL_STORAGE`（Android ≤ 9） | 在 pre-Q 设备上创建文件夹的旧版回退 |

**没有 `INTERNET` 权限**。应用无法联网。

## 架构

PhotoSwipe 是单模块 Compose 应用，围绕三个仓库和一个 Application 级服务构建：

```
MainActivity ──> AppRoot (Compose 导航宿主)
                   ├── SwipeScreen ────── SwipeViewModel ──┐
                   ├── FoldersScreen                       │
                   └── SettingsScreen                      │
                                                           ▼
ImageSorterApp ─┬─ PhotoRepository       (MediaStore 查询)
                ├─ FolderRepository      (DataStore 支持的 SortFolder 列表)
                ├─ ReviewedRepository    (DataStore 支持的 ID 集合)
                ├─ SettingsRepository    (DataStore 支持的偏好设置)
                └─ SortActions           (Keep / EnqueueDelete / CopyTo / MoveTo)
```

关键决策：

- **无 DI 框架。** `ImageSorterApp` 延迟构造每个仓库并作为属性暴露。ViewModel 通过 `CreationExtras` 读取。
- **无 SAF。** 所有文件夹写入通过 `MediaStore` 的 `RELATIVE_PATH`（API 29+），旧版本使用 `File` + `MediaScannerConnection` 回退。
- **批量删除。** `SortActions` 维护内存中的待处理列表。UI 在达到批次阈值或用户点击"立即删除"时自动刷新；刷新调用 `MediaStore.createDeleteRequest(...)` 并为整批发出单个 `IntentSender`。
- **Compose 导航。** 三个标签页通过 `NavHost` + Material 3 `NavigationBar` — 无 Fragment 或每屏 Activity。

## 项目结构

```
app/src/main/kotlin/com/leonxlnx/imagesorter/
├── ImageSorterApp.kt        # Application 类，拥有仓库
├── MainActivity.kt          # 边缘到边缘 Compose 宿主，应用主题
├── data/                    # MediaStore + DataStore 支持的仓库
│   ├── DateRange.kt
│   ├── FolderRepository.kt
│   ├── Photo.kt
│   ├── PhotoRepository.kt
│   ├── ReviewedRepository.kt
│   ├── SettingsRepository.kt
│   ├── SortActions.kt
│   └── SortOrder.kt
└── ui/
    ├── AppRoot.kt           # NavHost + 底部导航
    ├── folders/             # 文件夹管理界面 + 名称对话框
    ├── permission/          # 运行时权限门
    ├── settings/            # 设置界面，分组行
    ├── swipe/               # 卡片堆叠、拖动检测、视图模型
    └── theme/               # Material 3 配色方案 + ThemeMode
```

## 常见问题

**PhotoSwipe 能否在没有 Android 系统提示的情况下永久删除照片？**
不能。Android 11+ 要求对任何非你自己创建的媒体进行系统删除提示。PhotoSwipe 通过批量删除来减少摩擦——每 N 张照片一次提示——但无法完全绕过系统提示。

**会意外删除我的照片吗？**
只有在确认系统提示后，删除才是真删除。在批次刷新之前，队列中的照片位于内存队列中，你可以通过杀死应用、撤销上一次滑动或继续不刷新来清除。

**文件夹在哪里？**
默认在 `Pictures/PhotoSwipe/<文件夹名>/`。你可以在设置 → 存储中切换到 `DCIM/PhotoSwipe/`。

**为什么应用需要视频权限？**
只有在设置 → 筛选中启用"包含视频"时才需要。否则，应用永远不会请求此权限。

**是否支持设备间同步？**
不支持。PhotoSwipe 设计为单设备、离线运行。

## 路线图

未来版本可能包含的想法：

- 每个文件夹的颜色标签/图标
- 可选的审阅日志（CSV 导出分类位置）
- 滑动屏幕上最近使用文件夹的快速选择芯片
- 平板/折叠屏双窗格布局
- 英文之外的本地化
- 使用 Compose + Maestro 的自动化 UI 测试
- F-Droid 目录提交

如果你对某个想法感兴趣，请参见 [参与贡献](#参与贡献)。

## 参与贡献

欢迎贡献。在开始非平凡的更改之前，请开 issue 描述你的想法，以便我们确认方案。

Pull request 简要清单：

1. Fork 仓库并从 `main` 创建功能分支。
2. 本地运行 `./gradlew :app:lintDebug :app:assembleDebug` 确保两者都成功。
3. 保持更改最小化，符合现有 Compose / Material 3 风格。
4. 在 `Unreleased` 部分更新 [CHANGELOG.md](CHANGELOG.md)。
5. 按照模板开 PR — 描述**更改内容**和**原因**。

详见 [CONTRIBUTING.md](CONTRIBUTING.md)，社区准则见 [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)。

## 隐私

PhotoSwipe 100% 本地运行。无分析、无遥测、无广告、无互联网权限。见 [PRIVACY.md](PRIVACY.md) 了解完整政策。

## 安全

发现安全问题？**请勿**开公开 GitHub issue。请按照 [SECURITY.md](SECURITY.md) 中描述的披露流程。

## 许可证

PhotoSwipe 基于 [MIT License](LICENSE) 发布。你可以自由使用、修改和再分发，包括商业用途。欢迎署名。
