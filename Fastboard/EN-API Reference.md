<PlatformWrapper platform="web">

This page provides the API reference for the Fastboard SDK.

## createFastboard

```typescript
createFastboard(options: FastboardOptions): Promise;
```

Creates a `FastboardApp` instance.

**Parameters**

- `options`：Object. Configuration options for the `FastboardApp` instance. See <a href="#fastboardoptions"><code>FastboardOptions</code></a>.

**Returns**

The `FastboardApp` instance when the method call succeeds.

## createUI

```typescript
createUI(app?: FastboardApp | null, div?: Element): UI;
```

Creates a set of built-in UI components for Fastboard.

**Parameters**

- `app`: Object. The `FastboardApp` instance.
- `div`: HTML Element. The HTML element to contain the `FastboardApp` object.

**Returns**

The `UI` component. See [`UI`](#ui).

## createReplayUI

```typescript
createReplayUI(player?: FastboardPlayer | null, div?: Element): ReplayUI;
```

Creates a set of built-in UI components that enables replay mode.

**Parameters**

- `player`: The `FastboardPlayer` instance.
- `div`: HTML Element. The HTML element to contain the `FastboardPlayer` object.

**Returns**

The `ReplayUI` component. See [`ReplayUI`](#replayui).

### canOperate

```typescript
get canOperate(): boolean 
```

Gets whether the room is operable.

Checks if the current room is in interactive mode (`writable`) and the room connection state is connected (`connected`).

## mount

```typescript
mount(app: FastboardApp, div: HTMLDivElement, options?: MountProps): {
 update(props?: MountProps | undefined): void;
 destroy(): void;
};
```

<div class="alert note">Agora does not recommend this method since v0.3.6. Use <a href="#createui"><code>createUI</code></a> instead.</div>

Mounts the `FastboardApp` object to the HTML element.

**Parameters**

- `app`: Object. The `FastboardApp` instance, which is returned by the `createFastboard` method.
- `div`: HTMLElement. The HTML element to contain the `FastboardApp` object.
- `options`: (Optional) Object. Configuration options for the whiteboard user interface (UI). See  <a href="#mountprops"><code>MountProps</code></a >.

**Returns**

The following functions when the method call succeeds:

- `update`: Updates the whiteboard UI, which has the following parameters:
  - `props`: Configuration options. See <a href="#mountprops"><code>MountProps</code></a >.
- `destroy`: Unmounts the `FastboardApp` object.

## dispatchDocsEvent

```typescript
  export function dispatchDocsEvent(
    fastboard: FastboardApp | WindowManager,
    event: "prevPage" | "nextPage" | "prevStep" | "nextStep" | "jumpToPage",
    options: DocsEventOptions = {}
  )
```

Send events to a specified doc.

This method only applies to docs inserted by [`insertDocs`](#insertdocs-13).

**Parameters**

- `fastboard`: [`FastboardApp`](#createfastboard) or [`WindowManager`](https://github.com/netless-io/window-manager/blob/master/docs/api.md#mount) object. The object you wish to send events to.
- `event`: String. The event type. Only the following values are allowed.
  - `prevPage`: To the previous page.
  - `nextPage`: To the next page.
  - `prevStep`: To the previous step. This event equals to `prevPage` when sent to static docs.
  - `nextStep`: To the next step. This event equals to `nextPage` when sent to static docs.
  - `jumpToPage`: To a specified pagecount. You need to specify the pagecount by passing in `options`.
- `options`: (Optional)`DocsEventOptions`. Event options, used to specify the pagecount and the target doc. See [`DocsEventOptions`](#docseventoptions). `options` is empty by default, meaning sending events to the docs with the focus.

**Returns**

- `true`: Success.
- `false`: Failure. The reason of failure

## FastboardApp class

The `FastboardApp` class provides methods to manage the `FastboardApp` object.

**Note**

Call methods in this class after successfully creating a `FastboardApp` object using `createFastboard`.

### undo

```typescript
undo(): void
```

Undoes the previous action.

### redo

```typescript
redo(): void
```

Redoes an undone action.

### moveCamera

```typescript
moveCamera(camera: Partial<Camera>): void
```

Adjusts the view.

**Parameters**

- camera: Object. The view configuration. See <a href="#camera"><code>Camera</code></a>.

**Example**

Move the view so that the center of the HTML element is exactly aligned with the center of the whiteboard and the scale is 100%:

```typescript
app.moveCamera({ centerX: 0, centerY: 0, scale: 1 });
```

### moveCameraToContain

```typescript
moveCameraToContain(rect: Rectangle): void;
```

Adjusts the view to ensure the complete display of the specified rectangle area.

**Parameters**

- `rect`: Settings of the rectangle area. See <a href="#rectangle"><code>Rectangle</code></a>.


### setAppliance

```
setAppliance(appliance: ApplianceNames, shape?: ShapeType): ``void``;
```

Sets the whiteboard tool currently in use.

**Parameters**

- `appliance`: The name of the whiteboard tool. See <a href="#appliance"><code>ApplianceNames</code></a>.
- `shape`: (Optional) The shape type. See <a href="#shape"><code>ShapeType</code></a>. You can use this parameter to choose a shape when setting `appliance` as `shape`.

### setStrokeWidth

```typescript
setStrokeWidth(strokeWidth: number): void
```

Sets the stroke width.

**Parameters**

- `strokeWidth`: Number. The stroke width (px).

### setStrokeColor

```typescript
setStrokeColor(strokeColor: Color): void
```

Sets the stroke color.

**Parameters**

- `strokeColor`: The stroke color in RGB format. For example, `[0, 0, 255]` represents blue. See <a href="#color"><code>Color</code></a>.


### setTextColor

```typescript
setTextColor(textColor: Color): void
```

Sets the text color.

**Parameters**

- `textColor`: The text color in RGB format. For example, `[0, 0, 255]` represents blue. See <a href="#color"><code>Color</code></a>.

### toggleDottedLine

```typescript
toggleDottedLine(force?: boolean)
```

Toggles the drawing style of the Pencil tool.

When `force` is not passed, the method toggles between drawing solid and dotted lines. For example, if the Pencil tool is currently drawing solid lines, calling `toggleDottedLine()` will switch it to drawing dotted lines; if it is currently drawing dotted lines, calling `toggleDottedLine()` will switch it to drawing solid lines.

**Parameters**

- `force`：Boolean (optional). Forces the drawing style to switch:
  - `true`: Switches to drawing dotted lines.
  - `false`: Switches to drawing solid lines.

### setPencilEraserSize

```typescript
setPencilEraserSize(size: number)
```

Sets the size of the Pencil Eraser tool.

**Parameters**

- `size`：Number. The size of the pencil eraser, supports the following values:
  - `1`: (Default)Small.
  - `2`: Medium.
  - `3`: Large.

### setTextSize

```typescript
setTextSize(textSize: number): void
```

Sets the font size of the text.

**Parameters**

- `textSize`: Number. The font size of the text.

### insertImage

```typescript
async insertImage(url: string, crossOrigin?: boolean | string)
```

Inserts an image.

This method can insert and display the specified network image on the current whiteboard page. The inserted image is centered by default in the current view.

**Parameters**

- `url`: String. The URL address of the image. Ensure your app clients can access the URL; otherwise, the image cannot be displayed.
- `crossOrigin`: Boolean (optional). Whether to enable Cross-Origin Resource Sharing (CORS) for the inserted image:
  - `true`: (Default) Enable CORS.
  - `false`: Disable CORS.

### insertMedia

```typescript
insertMedia(title: string, src: string): Promise<string | undefined>
```

Inserts and plays audio and video in the whiteboard sub-window.

**Parameters**

- `title`: The title of the sub-window.
- `src`: The URL address of the audio or video file. Make sure your app clients can access the URL; otherwise, the audio or video file cannot be loaded properly.

**Returns**

The identifier of the extension when the method call succeeds.

### insertDocs [1/2]

```typescript
insertDocs(title: string, response: ProjectorResponse): Promise<string | undefined>;
```

Since v0.3.8.

Inserts and displays a document in the whiteboard sub-window. This method applies to the [new file conversion service](../develop/file-conversion-overview).

After successfully launching a file conversion task and calling the [Query file conversion progress API](/interactive-whiteboard/reference/whiteboard-api/file-conversion#query-the-progress-of-a-file-conversion-task) to get the file conversion result, you can call this method and pass in the obtained file conversion result. After a successful call, the SDK automatically creates a sub-window to insert and display the converted document per page.

**Parameters**

- `title`: The title of the sub-window.
- `response`: The response body returned when the call of the [Query file conversion progress API](/interactive-whiteboard/reference/whiteboard-api/file-conversion#query-the-progress-of-a-file-conversion-task) succeeds.

**Returns**

The identifier of the extension when the method call succeeds.

### insertDocs [2/2]

```typescript
insertDocs(params: InsertDocsParams): Promise<string | undefined>;
```

Inserts and displays a document in the whiteboard sub-window.

After successfully [launching a file conversion task](/interactive-whiteboard/reference/whiteboard-api/file-conversion#start-file-conversion), you can call this method and pass in the parameters of the converted file. After a successful call, the SDK automatically creates a sub-window to insert and display the converted file per page.

**Note**
Compared with `insertDocs [1/2]`, `insertDocs [2/2]` requires passing in parameters manually instead of the response body acquired by calling the [Query file conversion progress API](/interactive-whiteboard/reference/whiteboard-api/file-conversion#query-the-progress-of-a-file-conversion-task).

**Parameters**

- `params`: Parameters of the converted file. If the file is a static type, see <a href="#docstatic"><code>InsertDocsStatic</code></a>; if the file is a dynamic type, see <a href="#docdynamic"><code>InsertDocsDynamic</code></a>.

### insertCodeEditor

```typescript
insertCodeEditor(): Promise<string | undefined>
```

<div class="alert note">This method is deprecated since v0.3.6. Use `fastboard.manager.addApp({ kind: 'Monaco' })<` instead.</div>

Inserts a code editor.

CodeEditor is a code editing extension developed based on Monaco Editor. By calling `insertCodeEditor`, you can quickly integrate CodeEditor to your whiteboard and use its functions, such as code editing, auto-completion, and debugging.

**Returns**

The identifier of the extension when the method call succeeds.


### insertCountdown

```typescript
insertCountdown(): Promise<string | undefined>
```

<div class="alert note">This method is deprecated since v0.3.6. Use `fastboard.manager.addApp({ kind: 'Countdown' })` instead.</div>

Inserts a timer.

Countdown is a timer extension developed by Agora. By calling `insertCountdown`, you can quickly integrate Countdown to your whiteboard and use it to set, pause, and reset a countdown timer.

**Returns**

The identifier of the extension when the method call succeeds.

### insertGeoGebra

```typescript
insertGeoGebra(): Promise<string | undefined>
```

<div class="alert note">This method is deprecated since v0.3.6. Use `fastboard.manager.addApp({ kind: 'GeoGebra' })` instead.</div>

Inserts a GeoGebra mathematical calculator.

GeoGebra is a mathematical calculator extension developed based on  [GeoGebra](https://www.geogebra.org/). By calling `insertGeoGebra`, you can quickly integrate the GeoGebra extension to your whiteboard and use its functions.

**Note**

The GeoGebra extension in the Fastboard SDK is for demonstration purposes only. For commercial use, contact GeoGebra to apply for a license.

**Returns**

The identifier of the extension when the method call succeeds.

### removePage

```
removePage(index?): Promise<boolean>
```

Removes the specified whiteboard page.

**Parameters**

- `index`: Number. The page number of the to-be-removed whiteboard page. If it is left blank, the current page is deleted by default.

**Returns**

`true`: Success.

`false`: Failure.

### jumpPage

```typescript
jumpPage(index: number)
```

Jumps to the whiteboard page with the specified page number.

**Parameters**

- `index`: Number. The expected whiteboard page number to jump to. Values greater than the current number of whiteboard pages cannot be passed in.

### destroy

```typescript
destroy(): void
```

Destroys the Fastboard instance.

### DocsEventOptions

`DocsEventOptions` includes the following properties:

- `appId`: (Optional) String. Specify the target doc to send events to. If not passed in, the target doc is the doc with the focus.
- `page`: (Optional) Number. The page number you wish to jump to. The value should be within the range of 1 to the maximum page count of the doc.

## AppsInToolbar class

The `AppsInToolbar` class provides methods to manage the extension buttons on the toolbar.

### push

```typescript
push(...data: AppInToolbar[]): void;
```

Adds a extension button at the end of the extension center.

This method supports adding multiple extension buttons at once. The new buttons are added at the end of the extension center.

**Parameters**

- `data`: The extension button. See <a href="#appintoolbar"><code>AppInToolbar</code></a >.

**Example**

```typescript
// Adds a YouTube button to the extension center.
// When the button is clicked, insert the Plyr player in the whiteboard and play the specified video.
apps.push({
    icon: "https://api.iconify.design/logos:youtube-icon.svg?color=currentColor",
    kind: "Plyr",
    label: "YouTube",
    onClick(app) {
        app.manager.addApp({
            kind: "Plyr",
            options: { title: "YouTube" },
            attributes: {
                src: "https://www.youtube.com/embed/bTqVqk7FSmY",
                provider: "youtube",
            },
        });
    },
});
```

### insert

```typescript
insert(data: AppInToolbar, index: number): void;
```

Adds a extension button at the specified position.

This method supports adding one button at a time and specifying the position for the new button.

**Parameters**

- `data`: The extension button. See <a href="#appintoolbar"><code>AppInToolbar</code></a >.
- `index`: The index of the button in the extension center. The value must be greater than or equal to 0.

### delete

```typescript
delete(filter: (data: AppInToolbar) => boolean): void;
```

Deletes a specified extension button.

**Parameters**

- `filter`: The `filter()` method, which returns all extension buttons that need to be deleted. You need to pass a callback function to this method to filter out the buttons to be deleted.
- data: The extension button. See <a href="#appintoolbar"><code>AppInToolbar</code></a >.

### clear

```typescript
clear(): void;
```

Deletes all extension buttons.

This method deletes all buttons in the extension center, but does not delete the extension center (**apps**) button on the toolbar. To hide the extension center button on the toolbar, you can use the `options` parameter in the `mount` method to set `config.toolbar.apps.enable` as `false`.

## Type definition

<a name="fastboardoptions"></a>
### FastboardOptions

`FastboardOptions` has the following properties:

- `sdkConfig`: (Required) Object. Configurations for the <Link to="{{Global.API_REF_WEB_WHITE}}/globals.html#whitewebsdkconfiguration">WhiteWebSdk</Link> object, in which you must pass the following parameters:
  - `appIdentifier`: String. The App Identifier of your Interactive Whiteboard project issued by Agora. See [Get security credentials for your whiteboard project](../develop/enable-whiteboard#get-security-credentials-for-your-whiteboard-project).
  - `region`: The data center, which must be the same as the data center you chose when [creating the whiteboard room](/interactive-whiteboard/reference/whiteboard-api/room-management#create-a-room-post). The supported values are as follows:
    - `cn-hz`: Hangzhou, China, which provides services to areas not covered by other data centers.
    - `us-sv`: Silicon Valley, United States, which provides services to North America and South America.
    - `sg`: Singapore, which provides services to Singapore, East Asia, and Southeast Asia.
    - `in-mum`: Mumbai, India, which provides services to India.
    - `gb-lon`: London, United Kingdom, which provides services to Europe.
- `joinRoom`: (Required) Object. Parameters for joining a room:
  - `uid`: String. The unique identifier of a user in string format. The maximum length is 1,024 bytes. Ensure that the `uid` of each user in the same room is unique.
  - `uuid`: String. The room UUID, that is, the unique identifier of a room. See the value of the `uuid` parameter in the response body after a successful call of [Create a room (POST)](/interactive-whiteboard/reference/whiteboard-api/room-management#create-a-room-post).
  - `roomToken`: String. The room token for user authentication, which can be obtained through one of the following methods:
    - Call the [Generate a room token (POST)](/interactive-whiteboard/develop/generate-token-rest#generate-a-room-token-post) RESTful API.
    - Build a token generator at your app server. See [Generate a Token at App Server](/interactive-whiteboard/develop/generate-token-app-server).
- `managerConfig`: (Optional) Object. Configuration options for [WindowManager](https://github.com/netless-io/window-manager/blob/master/docs/api.md#mount).
- `netlessApps`: (Optional) Object. Built-in Fastboard official apps or custom Fastboard apps. See [netless-app](https://github.com/netless-io/netless-app) for details about Fastboard official apps, and see [develop-apps](https://github.com/netless-io/window-manager/blob/master/docs/develop-app.md) for information on developing custom Fastboard apps.
- `enableAppliancePlugin`: (Optional) Enable the `appliance-plugin` plugin. See [`AppliancePluginOptions`](https://github.com/netless-io/fastboard/blob/main/docs/zh/appliance-plugin.md).

### ReplayUI

A set of UI components for replay mode.

```
export interface ReplayUI {
  mount(div: Element, props?: ReplayFastboardProps): ReplayUI;
  update(props?: ReplayFastboardProps): void;
  destroy(): void;
}
```

`ReplayUI` contains the following functions:

- `mount`: Mounts the `FastboardApp` object to the HTML element.
  - `div`: HTML Element. The HTML element to contain the `FastboardPlayer` object.
  - `props`: Object. UI configuration. See [`FastboardProps`](#fastboardprops).
- `update`: Updates the Fastboard UI when the UI configurations changes.
  - `props`: Object. UI configuration. See [`FastboardProps`](#fastboardprops).
- `destroy`: Removes the UI.

### UI

A set of built-in UI components for Fastboard.

```
export interface UI {
 mount(div: Element, props?: FastboardProps): UI;
 update(props?: FastboardProps): void;
 destroy(): void;
}
```

`UI` contains the following functions:

- `mount`: Mounts the `FastboardApp` object to the HTML element.
  - `div`: HTML Element。The HTML element to contain the `FastboardApp` object.
  - `props`: Object. UI configuration. See [`FastboardProps`](#fastboardprops).
- `update`: Updates the Fastboard UI when the UI configurations changes.
  - `props`: Object. UI configuration. See [`FastboardProps`](#fastboardprops).
- `destroy`: Removes the UI.


<a name="mountprops"></a>
### MountProps

```typescript
type MountProps = {
 app?: FastboardApp | null;
 theme?: Theme;
 language?: Language;
 containerRef?: (container: HTMLDivElement | null) => void;
 config?: FastboardUIConfig;
}
```

UI configuration options.

`MountProps` contains the following properties:

- `app`: The `FastboardApp` object.
- `theme`: Theme of the UI:
  - `dark`: The dark theme.
  - `light`: (Default) The light theme.
- `language`: Language of the UI text:
  - `en`: (Default) English.
  - `zh-CN`: Chinese.
- `containerRef`: The callback triggered when the `FastboardApp` object is successfully mounted to the HTML element:
  - `container`: The HTML element that contains the `FastboardApp` object.
- `config`: Configurations for the UI components. See <a href="#uiconfig"><code>FastboardUIConfig</code></a >.

<a name="uiconfig"></a>
### FastboardUIConfig

```typescript
type FastboardUIConfig = { toolbar?: { enable?: boolean; apps?: { enable?: boolean } }; redo_undo?: { enable?: boolean }; zoom_control?: { enable?: boolean }; page_control?: { enable?: boolean }; }
```

Configurations for the whiteboard UI components.

`FastboardUIConfig` has the following properties:

- `toolbar`: (Optional) The toolbar.
  - `enable`: (Optional) Whether to display the toolbar on the whiteboard UI:
    - `true`:  (default) Display.
    - `false`: Do not display.
- `apps`: The extension center.
  - `enable`: (Optional) Whether to display the extension center on the toolbar:
    - `true`: (Default) Display.
    - `false`: (Default) Do not display.
- `redo_undo`: The redo and undo buttons.
  - `enable`: (Optional) Whether to display the redo and undo buttons on the whiteboard UI:
    - `true`: (Default) Display.
    - `false`: (Default) Do not display.
- `zoom_control`: The zoom control.
  - `enable`: (Optional) Whether to display the zoom control on the Whiteboard UI:
    - `true`: (Default) Display.
    - `false`: (Default) Do not display.
- `page_control`: The page control.
  - `enable`: (Optional) Whether to display the page control on the Whiteboard UI:
    - `true`: (Default) Display.
    - `false`: (Default) Do not display.

### ToolbarConfig

```typescript
export interface ToolbarConfig {
  placement?: "left" | "right";
  items?: ToolbarItem[];
  collapsed?: boolean;
  apps?: { enable?: boolean };
  colors?: Color[];
}
```

`ToolbarConfig` contains the following properties:
- `placement`: (Optional) String. The position of the toolbar:
  - `left`: (Default) Left side.
  - `right`: Right side.
- `items`: (Optional) String[]. The tool buttons displayed on the toolbar. By default, all tools are displayed. The supported values are:
  - `clicker`: Click tool.
  - `selector`: Selection tool.
  - `pencil`: Pencil tool.
  - `text`: Text tool.
  - `shapes`: Shape tool.
  - `eraser`: Eraser tool.
  - `clear`: Clear tool.
  - `hand`: Hand tool.
  - `laserPointer`: Laser pointer tool.
- `collapsed`: (Optional) Boolean. Whether the toolbar is collapsed:
  - `true`: Collapsed.
  - `false`: (Default) Not collapsed.
- `apps`: (Optional) Object. Extension center:
  - `enable`: (Optional) Whether to display the extension center button on the toolbar:
    - `true`: (Default) Display.
    - `false`: Do not display.
- `colors`: (Optional) Color[]. The colors of UI components. See [`Color`](#color).

<a name="camera"></a>
### Camera

`Camera` has the following parameters:

- `centerX`: Number. The X coordinate of the center of the HTML element in the whiteboard coordinate system (taking the center of the HTML element as the origin). The default value is 0.
- `centerY`: Number. The Y coordinate of the center of the HTML element in the whiteboard coordinate system (taking the center of the HTML element as the origin). The default value is 0.
- `scale`: Number. The scale factor of the view. The default value is 1, which means the scale factor is 100%.


<a name="rectangle"></a>
### Rectangle

`Rectangle` has the following properties:

- `originX`: Number. The X coordinate of the top left corner of the rectangle area in the whiteboard coordinate system (taking the center of the HTML element as the origin).
- `originY`: Number. The Y coordinate of the top left corner of the rectangle area in the whiteboard coordinate system (taking the center of the HTML element as the origin).
- `width`: The width (px) of the rectangle area.
- `height`: The height (px) of the rectangle area.

<a name="appliance"></a>
### ApplianceNames

`ApplianceNames` has the following enumerators:

- `selector = "selector"`: Selector.
- `clicker = "clicker"`: Clicker, which can be used for clicking and selecting content on an HTML5 file.
- `laserPointer = "laserPointer"`: Laser pointer.
- `pencil = "pencil"`: Pencil.
- `rectangle = "rectangle"`: Rectangle.
- `ellipse = "ellipse"`: Ellipse.
- `shape = "shape"`: Shape.
- `eraser = "eraser"`: Eraser.
- `text = "text"`: Text.
- `straight = "straight"`: Straight line.
- `arrow = "arrow"`: Arrow
- `hand = "hand"`: Hand.

<a name="shape"></a>
### ShapeType

`ShapeType` has the following enumerators:

- `Triangle = "triangle"`: Triangle.
- `Rhombus = "rhombus"`: Rhombus.
- `Pentagram = "pentagram"`: Pentagram.
- `SpeechBalloon = "speechBalloon"`: Speech balloon.

<a name="color"></a>
### Color

`Color`: Number[]. The color in RGB format. For example, `[0, 0, 255]` represents blue.

<a name="docstatic"></a>
### InsertDocsStatic

```typescript
export interface InsertDocsStatic {
    readonly fileType: "pdf";
    readonly scenePath: string;
    readonly scenes: SceneDefinition[];
    readonly title?: string;
}
```

For example:

```typescript
await fastboard.insertDocs({
              title: 'test.pdf',
              fileType: 'pdf',
              scenePath: '/path/to/scene',
              scenes: [
                {
                  name: '1',
                  ppt: {
                    width: 734,
                    height: 950,
                    src: 'https://url/to/image.png',
                  }
                },
              ],
            });
```

`InsertDocsStatic` has the following properties:

- `fileType`: String. The file type. The supported value is `pdf`, which represents the static file type.
- `scenePath`: String. The path of the whiteboard scene. Agora suggests you use "`/pdf/uuid`", where `uuid` is the UUID of the file conversion task. You can get `uuid` from the response body when the [Start file conversion (POST) API](/interactive-whiteboard/reference/whiteboard-api/file-conversion#start-file-conversion) call succeeds.
- `scenes`: SceneDefinition[]. The content to be displayed on the whiteboard scene, that is, the converted file. The `SceneDefinition[]` consists of multiple `SceneDefinition` objects. Each `SceneDefinition` object represents a page of file and must contain the following parameters:
  - `name` : String. A name for this scene.
  - `ppt`: String. A JSON object containing the following:
    - `height`: Number. The height (px) of the file.
    - `width`: Number. The width (px) of the file.
    - `src`: String. The URL address of each page of file, which you can get from the field in the response body when the [Query file conversion progress](/interactive-whiteboard/reference/whiteboard-api/file-conversion#query-the-progress-of-a-file-conversion-task) API call succeeds.
- `title`: (Optional) String. The title of the sub-window.

<a name="docdynamic"></a>
### InsertDocsDynamic

```typescript
export interface InsertDocsDynamic {
    readonly fileType: "pptx";
    readonly scenePath: string;
    readonly taskId: string;
    readonly title?: string;
    readonly url?: string;
   }
```

`InsertDocsDynamic` has the following properties:

- `fileType`: String. The file type. The supported value is `pptx`, which represents the dynamic file type.
- `scenePath`: String. The path of the whiteboard scene. Agora suggests that you use "`/pptx/uuid`", where `uuid` is the UUID of the file conversion task. You can get `uuid` from the response body when the [Start file conversion API](/interactive-whiteboard/reference/whiteboard-api/file-conversion#start-file-conversion) call succeeds.
- `taskId`: String. The UUID of the file conversion task. You can get `uuid` from the response body when the [Start file conversion API](/interactive-whiteboard/reference/whiteboard-api/file-conversion#start-file-conversion) call succeeds.
- `title`: (Optional) String. The title of the sub-window.
- `url`: String. The path where you store the converted file. For example, `"https://docs-test-xxx.oss-cn-hangzhou.aliyuncs.com/dynamicConvert"`.

<a name="appintoolbar"></a>
### AppInToolbar

The extension button.

```typescript
interface AppInToolbar {
 kind: string;
 icon: string;
 label: string;
 onClick: (app: FastboardApp) => void;
}
```

`AppInToolbar` has the following properties:

- `kind`: String. The unique identifier of the extension button, which can be any string.
- `icon`: String. The URL of the button icon.
- `label`: String. The caption of the button, that is, the text displayed underneath the button. Agora recommends that the length should not exceed 12 characters; otherwise, the text cannot displayed completely.
- `onClick`: The callback triggered when the button is clicked.
  - `app`: the `FastboardApp` object.


</PlatformWrapper>