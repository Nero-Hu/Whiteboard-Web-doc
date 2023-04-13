This page contains Fastboard Web API changes starting from v0.3.6 and beyond.

## createUI

```
createUI(app?: FastboardApp | null, div?: Element): UI;
```

Creates a set of built-in UI components for Fastboard.

**Parameters**

- `app`: Object. The `FastboardApp` instance. 
- `div`: HTML Element. The HTML element to contain the `FastboardApp` object.

**Returns**

The `UI` component. See [`UI`](#ui). 

## createReplayUI

```
createReplayUI(player?: FastboardPlayer | null, div?: Element): ReplayUI;
```

Creates a set of built-in UI components that enables replay mode.

**Parameters**

- `player`: The `FastboardPlayer` instance. 
- `div`: HTML Element. The HTML element to contain the `FastboardPlayer` object.

**Returns**

The `ReplayUI` component. See [`ReplayUI`](#replayui). 

## mount

```typescript
mount(app: FastboardApp, div: HTMLDivElement, options?: MountProps): {
 update(props?: MountProps | undefined): void;
 destroy(): void;
};
```

<div class="alert note">Agora does not recommend this method since v0.3.6. Use <a href="#createui"><code>createUI</code></a> instead.</div>

Mounts the `FastboardApp` object to the HTML element.



### insertCodeEditor

```typescript
insertCodeEditor(): Promise<string | undefined>
```

<div class="alert note">This method is deprecated since v0.3.6. Use <code>fastboard.manager.addApp({ kind: 'Monaco' })</code> instead.</div>

Inserts a code editor.

CodeEditor is a code editing extension developed based on Monaco Editor. By calling `insertCodeEditor`, you can quickly integrate CodeEditor to your whiteboard and use its functions, such as code editing, auto-completion, and debugging.

**Returns**

The identifier of the extension when the method call succeeds.

### insertCountdown

```typescript
insertCountdown(): Promise<string | undefined>
```

<div class="alert note">This method is deprecated since v0.3.6. Use <code>fastboard.manager.addApp({ kind: 'Countdown' })</code> instead.</div>

Inserts a timer.

Countdown is a timer extension developed by Agora. By calling `insertCountdown`, you can quickly integrate Countdown to your whiteboard and use it to set, pause, and reset a countdown timer.

**Returns**

The identifier of the extension when the method call succeeds.

### insertGeoGebra

```typescript
insertGeoGebra(): Promise<string | undefined>
```

<div class="alert note">This method is deprecated since v0.3.6. Use <code>fastboard.manager.addApp({ kind: 'GeoGebra' })</code> instead.</div>

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



## Type definition

<a name="fastboardoptions"></a>
### FastboardOptions

`FastboardOptions` has the following properties:

- `sdkConfig`: (Required) Object. Configurations for the [`WhiteWebSdk`](https://docs.agora.io/en/whiteboard/API%20Reference/whiteboard_web/globals.html#whitewebsdkconfiguration) object, in which you must pass the following parameters:
  - `appIdentifier`: String. The App Identifier of your Interactive Whiteboard project issued by Agora. See [Get security credentials for your whiteboard project](https://docs.agora.io/en/whiteboard/enable_whiteboard?platform=Web#get-security-credentials-for-your-whiteboard-project).
  - `region`: The data center, which must be the same as the data center you chose when [creating the whiteboard room](https://docs.agora.io/en/whiteboard/whiteboard_room_management?platform=RESTful#create-a-room-post). The following values are supported:
    - `cn-hz`: Hangzhou, China, which provides services to areas not covered by other data centers.
    - `us-sv`: Silicon Valley, United States, which provides services to North America and South America.
    - `sg`: Singapore, which provides services to Singapore, East Asia, and Southeast Asia.
    - `in-mum`: Mumbai, India, which provides services to India.
    - `gb-lon`: London, United Kingdom, which provides services to Europe.
- `joinRoom`: (Required) Object. Parameters for joining a room:
  - `uid`: String. The unique identifier of a user in string format. The maximum length is 1,024 bytes. Ensure that the `uid` of each user in the same room is unique.
  - `uuid`: String. The room UUID, that is, the unique identifier of a room. See the value of the `uuid` parameter in the response body after a successful call of [Create a room (POST)](https://docs.agora.io/en/whiteboard/whiteboard_room_management?platform=RESTful#create-a-room-post).
  - `roomToken`: String. The room token for user authentication, which can be obtained through one of the following methods:
    - Call the [Generate a room token (POST)](https://docs.agora.io/en/whiteboard/generate_whiteboard_token?platform=RESTful#generate-a-room-token-post) RESTful API.
    - Build a token generator at your app server. See [Generate a Token at App Server](https://docs.agora.io/en/whiteboard/generate_whiteboard_token_at_app_server?platform=RESTful).
- `managerConfig`: (Optional) Object. Configuration options for [WindowManager](https://github.com/netless-io/window-manager/blob/master/docs/api.md#mount).
- \- `netlessApps`: (Optional) Object. Built-in Fastboard official apps or custom Fastboard apps. See [netless-app](https://github.com/netless-io/netless-app) for details about Fastboard official apps, and see [develop-apps](https://github.com/netless-io/window-manager/blob/master/docs/develop-app.md) for information on developing custom Fastboard apps. 

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

