## v0.3.8

v0.3.6 was released on August xx, 2023.


#### New features

**Insert PDF/PPTX docs**

This release adds the `insertDocs [2/3]` method to insert PDF/PPTX docs converted by the [New file conversion service](https://docs.agora.io/en/interactive-whiteboard/develop/file-conversion-overview?platform=web).

**Control PDF/PPTX docs**

This release adds the `dispatchDocsEvent` method to send events to specified PDF/PPTX docs inserted in the whiteboard. This enables page turning, page jumping, and slide animation playback to be controlled programmatically.

#### Bugfixes

This release fixed the intermittent packaging failure issue when using an older version of the packager.

#### API Changes

**Added**

- [`insertDocs [2/3]`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk?platform=web#insertdocs-23)
- [`dispatchDocsEvent`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk?platform=web#dispatchdocsevent)
- [`DocsEventOptions`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk?platform=web#docseventoptions)

## v0.3.6

v0.3.6 was released on October 28, 2022.

#### New features

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

- Whiteboard was sometimes out of focus on some devices.
- The UI for user-defined hot keys displayed incorrectly.

#### API changes

**Added**

- [`removePage`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#removepage)
- [`createUI`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#createui)
- [`createReplayUI`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#createreplayui)

**Deprecated**

- `insertCodeEditor`: Use `fastboard.manager.addApp({ kind: 'Monaco' })` instead.
- `insertCountdown`: Use `fastboard.manager.addApp({ kind: 'Countdown' })` instead.
- `insertGeoGebra`: Use `fastboard.manager.addApp({ kind: 'GeoGebra' })` instead.
- [`mount`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#mount): Use [`createUI`](https://docs.agora.io/en/interactive-whiteboard/reference/uikit-sdk#createui) instead. 