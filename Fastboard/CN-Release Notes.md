本文提供声网 Fastboard SDK for Web 的发版说明。

声网 Fastboard SDK 是为帮助开发人员快速构建白板应用推出的新一代白板 SDK。Fastboard SDK 基于互动白板 SDK （`white-web-sdk`）开发，对复杂的 API 进行封装，简化了接口调用逻辑，并提供核心功能的实现和默认 UI；此外，Fastboard SDK 还集成窗口管理器（[Window Manager](https://github.com/netless-io/window-manager)）和插件中心（[Netless App](https://github.com/netless-io/netless-app)），方便开发者快速添加插件，轻松扩展白板应用的功能。使用 Fastboard SDK，你无需深入学习互动白板复杂的概念，只需几行代码即可加入白板房间，并立即使用丰富的工具体验实时互动协作。

## 0.3.6 版

该版本于 2022 年 10 月 28 日发布。

#### 新增特性

**注册 Fastboard 插件**

该版本在[` FastboardOptions`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#fastboardoptions) 接口中新增可选属性 `netlessApps`，用于注册 Fastboard 官方内置或由你自定义的 Fastboard 插件，详见[注册和使用 app](https://github.com/netless-io/fastboard/blob/main/README-zh.md#注册与使用-apps)。

**创建 UI 组件**
该版本新增了 [`createUI`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#createui) 和 [`createReplayUI`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#createreplayui) 方法分别用于创建 Fastboard 内置的一套 UI 组件和回放模式的一套 UI 组件。

**删除白板页**
该版本新增了 [`removePage`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#removepage) 方法用于删除指定白板页。

#### 改进

该版本进行了如下改进：

- 点击插件按钮后自动隐藏插件菜单。
- 向白板日志提交 Fastboard 信息。
- 优化 UI 在 React 下使用时的性能。

#### 修复问题

该版本修复了如下问题：

- 白板在某些设备上可能失焦。
- 用户自定义热键的 UI 显示错误。

#### API 变更

**新增**

- [`removePage`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#removepage)
- [`createUI`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#createui)
- [`createReplayUI`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#createreplayui)

**废弃**

- `insertCodeEditor`：改用 `fastboard.manager.addApp({ kind: 'Monaco' })` 实现。
- `insertCountdown`：改用 `fastboard.manager.addApp({ kind: 'Countdown' })` 实现。
- `insertGeoGebra`：改用 `fastboard.manager.addApp({ kind: 'GeoGebra' })` 实现。
- [`mount`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#mount)：现在推荐用 [`createUI`](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#createui)。

## 0.3.2 版

该版本于 2022 年 4 月 29 日发布。

#### 升级必看

该版本替换了构建白板用户界面使用的框架。集成该版本的 Fastboard SDK，无需再添加 `react` 和 `react-dom` 依赖项。详见[添加依赖项](https://docs.agora.io/cn/whiteboard/join_whiteboard_room_web_fastboard?platform=Web#添加依赖项)。

#### 新增特性

**1. 白板用户界面配置**

该版本在 [`mount`](https://docs-preprod.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#mount) 方法中新增 `options` 参数，用于配置白板用户界面。你可以通过该参数设置白板用户界面的主题、语言和每个组件的显示状态等。

同时，该版本还将调用 `mount` 方法后返回的 `update` 方法的 `theme` 和 `language` 变更为 `props` 参数。通过 `props` 参数可以更新白板用户界面的主题、语言和每个组件的显示状态等。

**2. 字体设置**

该版本在 `FastboardApp` 类中新增 [`setTextColor`](https://docs-preprod.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#settextcolor) 和 [`setTextSize`](https://docs-preprod.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#settextsize) 方法，用于设置字体的颜色和大小，方便你自行开发文本编辑功能。

**3. 管理插件按钮**

该版本新增 `AppsInToolbar` 类，提供管理工具条上插件按钮方法，具体如下：

- [`push`](https://docs-preprod.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#push)：在插件中心的末尾添加插件按钮。
- [`insert`](https://docs-preprod.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#insert)：在指定位置添加一个插件按钮。
- [`delete`](https://docs-preprod.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#delete)：删除指定的插件按钮。
- [`clear`](https://docs-preprod.agora.io/cn/whiteboard/fastboard_api_web?platform=Web#clear)：删除所有插件按钮。

#### 改进

该版本进行了如下改进：

- 优化了用户界面的样式。
- 当用户以只读模式加入白板房间时，SDK 自动隐藏用户界面上的所有组件，以避免用户点击却不生效。

## 0.2.8 版

该版本于 2022 年 3 月 7 日发布，是 Fastboard SDK 首个版本。

#### 功能特性

**1. 白板核心功能的默认实现和 UI**

该版本直接实现了互动白板的核心基础功能，并提供默认的 UI。集成 Fastboard SDK 并调用 `createFastboard` 方法加入白板房间后，即可使用如下功能：

- 白板工具栏，包括铅笔、文本编辑、图形工具等所有白板基础编辑工具，并支持设置线条粗细、字体大小和颜色。
- 页面管理，包括新增页面和页面跳转。
- 视角管理，包括页面缩放和视角调整。
- 撤销、重做

同时，Fastboard SDK 还提供了如下 API，方便你自行开发这些功能并自定义 UI：

- `setAppliance`
- `setStrokeWidth`
- `setStrokeColor`
- `moveCamera`
- `moveCameraToContain`
- `undo`
- `redo`

**2. 添加和使用插件**

Fastboard SDK 集成了窗口管理器（[Window Manager](https://github.com/netless-io/window-manager)）和插件中心（[Netless App](https://github.com/netless-io/netless-app)），用于在白板应用中快速添加和使用插件，扩展白板的功能。该版本默认提供代码编辑器（Code Editor）、计时器（Countdown）、数学计算器（GeoGebra）插件，加入房间即可使用。此外，你还可以根据业务需求开发并添加自定义插件。

<div class="alert note">GeoGebra 数学计算器仅作为示例插件，如需商用，请联系 GeoGebra 获取许可。</div>

**3. 展示文件**

Fastboard SDK 支持在白板中插入和展示多种形式的文件，例如，PNG、JPG 格式的图片，MP3、MP4 格式的音视频，以及 PPT、PPTX、DOC、DOCX、PDF 等格式的文档。具体实现步骤参考[展示文件](./present_files)。

#### 相关文档

你可以参考以下文档使用 Fastboard SDK 实现相应的互动白板功能：

- [加入白板房间（使用 Fastboard SDK）](./join_whiteboard_room_web_fastboard)：快速集成 Fastboard SDK，加入白板房间，并立即使用丰富的编辑工具体验实时互动协作。
- [展示文件](./present_files)：介绍如何在白板应用中插入图片、播放音视频和演示文档。
- [API 参考](https://docs.agora.io/cn/whiteboard/fastboard_api_web?platform=Web)：提供 Fastboard SDK 核心 API 的详细描述。