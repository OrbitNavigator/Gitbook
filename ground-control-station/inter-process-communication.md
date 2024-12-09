---
description: >-
  This page describes step by step how to setup IPC between main and renderer
  processes
---

# Inter-Process Communication

### Preload Scripts

Preload Scripts contain code that is executed in the renderer process. These scripts run in renderer context but have more privileges by having access to Node.js APIs, allowing them to have access to the OS functions.

Lets start by adding a Preload Script to our application

{% stepper %}
{% step %}
### Create a Preload Script

In the main directory create `preload.mjs`&#x20;

{% code title="preload.mjs" %}
```javascript
import { contextBridge, ipcRenderer } from "electron";

// Exposing methods using contextBridge
contextBridge.exposeInMainWorld("mavlink", {
});
```
{% endcode %}


{% endstep %}

{% step %}
### Import Preload Script in main

{% code title="main.js" %}
```javascript
import { BrowserWindow, app, ipcMain } from "electron";
import path from "path";
import { fileURLToPath } from "url";

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

let win;

const createWindow = () => {
  win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, "preload.mjs"),
      contextIsolation: true,
      nodeIntegration: true,
    },
  });

  if (process.env.NODE_ENV === "development") {
    win.loadURL("http://localhost:5173");
  } else {
    win.loadFile(path.join(__dirname, "../../build/renderer/index.html"));
  }
};

app.whenReady().then(() => {
  createWindow();

  app.on("activate", () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow();
    }
  });
});

app.on("window-all-closed", () => {
  if (process.platform !== "darwin") {
    app.quit();
  }
});
```
{% endcode %}
{% endstep %}
{% endstepper %}

### Using Inter-Process Communication

#### Renderer to Main (One-Way)

{% stepper %}
{% step %}
### Listen for event on Main

{% code title="main.js" %}
```javascript
import { app, BrowserWindow, ipcMain } from "electron";

const handler = (event,data) => {
    // Callback function to handle data
    }

app.whenReady().then()(() => {
    ipcMain.on("foo", handler);
    createWindow();
})
```
{% endcode %}
{% endstep %}

{% step %}
### Expose `ipcRenderer.send` via Preload

{% code title="preload.mjs" %}
```javascript
import { contextBridge, ipcRenderer } from "electron";

// Exposing methods using contextBridge
contextBridge.exposeInMainWorld("electronAPI", {
    bar: (data) => ipcRenderer.send("foo",data);
});
```
{% endcode %}
{% endstep %}

{% step %}
### Call the function in Renderer

{% code title="App.jsx" %}
```javascript
const buttonHandler = () => {
    window.electronAPI.bar(data);
}
```
{% endcode %}
{% endstep %}
{% endstepper %}

#### Renderer to Main (Two-Way)

{% stepper %}
{% step %}
### Listen for events with `ipcMain.handle`&#x20;

{% code title="main.js" %}
```javascript
import { app, BrowserWindow, dialog, ipcMain } from "electron";

const handler = async () => {
    return data;
}

app.whenReady().then(() => {
    ipcMain.handle("requestData", handler);
    createWindow();
})
```
{% endcode %}


{% endstep %}

{% step %}
### Expose `ipcRenderer.invoke` via Preload

{% code title="preload.js" %}
```javascript
import { contextBridge, ipcRenderer } from "electron";

// Exposing methods using contextBridge
contextBridge.exposeInMainWorld("electronAPI", {
    request: () => ipcRenderer.invoke("requestData");
});
```
{% endcode %}
{% endstep %}

{% step %}
### Request data from Renderer

{% code title="App.jsx" %}
```javascript
const buttonHandler = () => {
    data = await window.electronAPI.request();
}
```
{% endcode %}
{% endstep %}
{% endstepper %}

#### Main to Renderer (One-Way)

{% stepper %}
{% step %}
### Send message from Main

{% code title="main.js" %}
```javascript
import { app, BrowserWindow, ipcMain } from "electron"
const senderFunction = () =>{
    win.webContnets.send()
}
```
{% endcode %}
{% endstep %}

{% step %}
### Expose `ipcRenderer.on` via Preload

{% code title="preload.js" %}
```javascript
const { contextBridge, ipcRenderer } = require('electron')

contextBridge.exposeInMainWorld('electronAPI', {
  onData: (callback) => ipcRenderer.on('update-Data', (event, value) => callback(value))
})
```
{% endcode %}
{% endstep %}

{% step %}
### Handle Data request in Renderer

{% code title="App.jsx" %}
```javascript
window.electronAPI.onData((value) =>{
    //handle value here
})
```
{% endcode %}
{% endstep %}
{% endstepper %}

