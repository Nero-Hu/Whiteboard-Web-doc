<PlatformWrapper platform="web">


The <Vg k="FAST_SDK" /> is the latest generation of the whiteboard SDK launched by Agora to help developers quickly build whiteboard applications. It simplifies the APIs of the <Vg k="WHITE_SDK" /> and implements the core functionality with a default user interface (UI). In addition, the <Vg k="FAST_SDK" /> integrates [window-manager](https://github.com/netless-io/window-manager) and extensions from [netless-app](https://github.com/netless-io/netless-app) to allow developers to easily add extensions and thus extend the functionality of their whiteboard applications. With the <Vg k="FAST_SDK" />, you do not need to learn the complex concepts of the interactive whiteboard; you can join a whiteboard room with a few lines of code and instantly use the rich editing tools to start real-time interactive collaboration.

## v1.0.0

This version was released on November xx, 2024.

#### New features

**Full package reference**

Starting from this version, Fastboard SDK adds full package files `@netless/fastboard/full` and `@netless/fastboard-react/full` to solve the dependency conflict problem. When using the full package reference, you do not need to install `@netless/window-manager` and `white-web-sdk` dependencies.

<div class="alert note">
Using the full package reference, you need to remove the `@netless/window-manager`, `white-web-sdk`, and `jspdf` dependencies from your project.
</div>

More information about full package and partial package reference, see [Fastboard installation and use](https://github.com/netless-io/fastboard/blob/main/README.md#install).

**High-performance whiteboard drawing tool**

This version adds the `appliance-plugin` plugin, which implements a high-performance whiteboard drawing tool and supports use in multi-window mode. After installing `@netless/appliance-plugin`, you can enable this plugin by using the `FastboardOptions.enableAppliancePlugin` or `managerConfig.supportAppliancePlugin` configuration item. In addition, when turning on appliance plugin, Fastboard UI adds a `laserPen` tool. For more information, see [`appliance-plugin`](https://github.com/netless-io/fastboard/blob/main/docs/en/appliance-plugin.md).

<div class="alert note">
`@netless/appliance-plugin` is a required external dependency and is not included in the full package. You need to install it separately.
</div>

#### Improvements

**Custom UI component color**

The `ToolbarConfig` interface adds the `colors` property, which is used to set the color of the UI components. Starting from this version, the colors of the toolbar and floatbar are consistent by default, and the application uses a unified color set. You can also set the color set of the two by using [`joinRoomParams.floatbarOptions.colors`](/api-ref/whiteboard/javascript/globals#floatbaroptions) and [`ToolbarConfig.colors`](/api-ref/fastboard/javascript/fastboard-api#toolbarconfig).

**Other improvements**

- This version updates @netless/window-manager to v1.0.0.

#### API Changes

**Added**

- `FastboardOptions.enableAppliancePlugin`
- `ToolbarConfig.colors`

## v0.3.16

This version was released on September xx, 2024.

#### New features

**Get whether the room is operable**

This version adds the `canOperate` method, which is used to get whether the room is in an operable state, that is, whether the current room is in interactive mode (`writable`) and the room connection state is connected (`connected`).


#### Improvements

This version has the following improvements:

- In multi-window mode, the small window application inserted supports dragging the upper right corner of the window to adjust the window size.
- Supports accessing the value of the state after calling `destroy` to destroy the state (`state.value`).
- The `insertDocs` method supports passing in the response body of the static conversion with the `prefix` field.

#### Fixed issues

This version fixes the following issues:

- Using `insertDocs` to insert a document converted from a static file fails to return the `appId`.
- An error occurs when `FatboardUIConfig` is updated to `{ toolbar: undefined }`.
- Listening to some states (such as `camera.value`) returns an outdated value.
- Some components are invalid when the room connection state (`room.phase`) is not connected.

#### API Changes

**Added**
- `canOperate`

## v0.3.10

v0.3.10 was released on Febrary xx, 2024.

#### New features

**New features for whiteboard tools**

This version adds new features to the following whiteboard tools：

- Pencil Tool: Added `toggleDottedLine` method to the Pencil tool to switch to drawing dotted lines.
- Pencil Eraser Tool: Added `setPencilEraserSize` method to the Pencil Eraser tool to change the size of the pencil eraser.

#### Improvements

This version has the following ：

- Added `crossOrigin` parameter to the `insertImage` method to enable Cross-Origin Resource Sharing (CORS) for inserted images.
- Added `jumpPage` method to jump to a specified whiteboard page.

#### API Changes

**Added**

- `toggleDottedLine`
- `setPencilEraserSize`
- Added a new parameter `crossOrigin` in `insertImage` 
- `jumpPage`

## v0.3.8

v0.3.8 was released on January 19, 2024.

#### New features

**Insert PDF/PPTX docs**

This release adds the `insertDocs [2/3]` method to insert PDF/PPTX docs converted by the [New file conversion service](https://docs.agora.io/en/interactive-whiteboard/develop/file-conversion-overview?platform=web).

**Control PDF/PPTX docs**

This release adds the `dispatchDocsEvent` method to send events to specified PDF/PPTX docs inserted in the whiteboard. This enables page turning, page jumping, and slide animation playback to be controlled programmatically.

**Register Fastboard apps**

This release adds a new optional attribute `netlessApps` in the [`FastboardOptions`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#fastboardoptions) interface to register built-in Fastboard official apps and custom Fastboard apps. See [netless-app](https://github.com/netless-io/netless-app) for more official apps, and see [develop-apps](https://github.com/netless-io/window-manager/blob/master/docs/develop-app.md) for information on developing custom Fastboard apps.

You have two ways to register Fastboard apps:

- Before entering a whiteboard room:

    ```typescript
    import { register } from "@netless/fastboard";
    import MyApp from "my-app";

    register({ kind: MyApp.kind, src: MyApp });
    ```

- When calling `createFastboard`:

   ```typescript
   createFastboard({
     ..., // other configurations
     netlessApps: [MyApp],
   });
   ```

After registering the app, call the following interface to insert it when in a whiteboard room:

```typescript
fastboard.manager.addApp({ kind: MyApp.kind });
```

**Create UI components**

This release adds the  [`createUI`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#createui) and [`createReplayUI`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#createreplayui) methods to create a set of UI components for Fastboard and the playback mode, respectively.

**Delete whiteboard pages**

This release adds the [`removePage`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#removepage) method to delete the specified whiteboard pages.

#### Improvements

This release provides the following improvements:

- The Fastboard app pannel automatically hides after a user clicks one of its buttons.
- Fastboard-related information is now recorded and submitted to the whiteboard log.
- UI performance is optimized when used under React.

#### Fixed issues

This release fixed the following issues:

- The intermittent packaging failure issue when using an older version of the packager.
- Whiteboard was sometimes out of focus on some devices.
- The UI for user-defined hot keys displayed incorrectly.

#### API Changes

**Added**

- [`insertDocs [2/3]`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk?platform=web#insertdocs-23)
- [`dispatchDocsEvent`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk?platform=web#dispatchdocsevent)
- [`DocsEventOptions`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk?platform=web#docseventoptions)
- [`removePage`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#removepage)
- [`createUI`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#createui)
- [`createReplayUI`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#createreplayui)

**Deprecated**

- `insertCodeEditor`: Use `fastboard.manager.addApp({ kind: 'Monaco' })` instead.
- `insertCountdown`: Use `fastboard.manager.addApp({ kind: 'Countdown' })` instead.
- `insertGeoGebra`: Use `fastboard.manager.addApp({ kind: 'GeoGebra' })` instead.
- [`mount`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#mount): Use [`createUI`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#createui) instead.


## v0.3.2
v0.3.2 was released on April 29, 2022.

#### Compatibility changes
This release replaces the framework used to build the whiteboard UI. As of this release, you do not need to add `react` and `react-dom` dependencies when integrating the SDK. For detailed SDK integration steps, see [Add dependencies](/interactive-whiteboard/get-started/get-started-uikit).

#### New features
**1. Configurations for the whiteboard user interface (UI)**

This release adds the `options` parameter to the `mount` method for configuring the whiteboard UI. You can use this parameter to set the theme, language, and each component's display state on the whiteboard UI.

In addition, for the `update` method returned by the the `mount` method, this release changes the theme and language parameters to the `props` parameter. You can use the `props` parameter to update the theme, language, and each component's display state on the whiteboard UI.

**2. Text settings**

This release adds the `setTextColor` and `setTextSize` methods in the `FastboardApp` class for setting the text color and font size. You can use these methods to implement your own text editing functions.

**3. Manage extension buttons**

This release adds the `AppsInToolbar` class, which provides the following methods to manage extension buttons on the toolbar:

- `push`: Adds an extension button at the end of the extension center.

- `insert`: Adds an extension button at the specified position.

- `delete`: Deletes a specified extension button.

- `clear`: Deletes all extension buttons.

#### Improvements
This release has the following improvements:

- Optimizes the style of the whiteboard UI.

- Automatically hides all components on the whiteboard UI when a user joins a whiteboard room in read-only mode to avoid having a user click on unresponsive components.

## v0.2.8

v0.2.8 was released on March 7, 2022. This is the first official release of the UI Kit.

#### Features

**Implementations of the core whiteboard functionality and user interface (UI)**

This release directly implements the basic functions of the interactive whiteboard with a default UI. After integrating the UI Kit and calling `createFastboard` to join the whiteboard room, you can use the following functions:

- The whiteboard toolbar, which includes all basic whiteboard editing tools, such as pencil, text editor, and shape tools. It also supports setting stroke width, font size, and stroke color.

- The whiteboard page control, which enables you to add and switch whiteboard pages.

- The view control, which you can use to zoom in and out of the current whiteboard page and adjust the view.

- Undo and redo an action.

In addition, the UI Kit provides the following APIs to enable you to implement these functions with customized UIs:

- `setAppliance`

- `setStrokeWidth`

- `setStrokeColor`

- `moveCamera`

- `moveCameraToContain`

- `undo`

- `redo`

#### Adding and using extensions

The UI Kit integrates [window-manager](https://github.com/netless-io/window-manager) and extensions from [netless-app](https://github.com/netless-io/netless-app) to enable you to quickly add and use extensions in the whiteboard application. This release provides the following extensions with UI:

- Code editor: A code editing extension developed based on Monaco Editor.

- Countdown: A timer extension developed by Agora.

- GeoGebra: A mathematical calculator extension developed based on GeoGebra.

Users can use these extensions immediately after joining the whiteboard room. This release also integrates the following extensions without UI and provides APIs for you to use them:

- Media player: An extension for playing audio and video. You can call `insertMedia` to use this extension.

- Docs viewer: An extension for displaying static documents. You can call `insertDocs` to use this extension.

- Slide: An extension for displaying dynamic document. You can call `insertDocs` to use this extension.

In addition, you can develop and add custom extensions to your whiteboard application according to your business needs.

<div class="alert note">The GeoGebra extension in the UI Kit is for demonstration purposes only. For commercial use, contact GeoGebra to apply for a license.</div>

#### Display files

The UI Kit supports inserting and displaying files in multiple formats on the whiteboard, such as images in PNG and JPG formats, audio and video in MP3 and MP4 formats, and documents in PPT, PPTX, DOC, DOCX, and PDF formats. For detailed implementation steps, see [Display Files](/interactive-whiteboard/develop/scenes/display-files-fast).

#### Reference

Refer to the following documentation to integrate the UI Kit and add the whiteboard functionality to your project:

- [Join a Whiteboard Room](/interactive-whiteboard/get-started/get-started-sdk): Describes how to quickly join a whiteboard room and experience interactive whiteboard features using the UI Kit.

- [Display Files](/interactive-whiteboard/develop/scenes/display-files-fast): Describes how to call the UI Kit's APIs to insert images, play audio and video, and present documents on the whiteboard.

- [API Reference](/interactive-whiteboard/reference/uikit-sdk): Provides a detailed API reference for the UI Kit.


</PlatformWrapper>