---
icon: react
---

# Electron Installation

Electron Application contain 2 major type of processes: **Main Process** and the **Renderer Process.**

### Main Process

The **Main Process** in electron controls the lifecycle of the application, manages creation of windows and handles communication with the operating system. It is kind of like the back end of the application.

### Renderer Process

The **Renderer Process** is where the app's UI runs. Each windows in electron app is managed by Renderer Process, Similar to how Chrome tabs operate, The Main Process is responsible for launching the renderer process.

### How they Communicate

The **Main Process** and **Renderer Process** in electron communicate using a process called **Inter-Process-Communication (IPC)** to exchange data between the processes.

#### Preload Script in IPC

The Preload Script (`preload.js`) act as a bridge for the IPC communication, enabling Renderer process to communicate with the Main process. It uses context Isolation, meaning the web page can not directly interact with the Node.js APU, it only exposes the APIs to the renderer specified in the Preload Script.

### Installation

{% stepper %}
{% step %}
### Install Electron

Navigate to your project's root directory and install Electron:

```bash
yarn add electron --dev
```
{% endstep %}

{% step %}
### Restructure the React Application

1. Create a `main.js`  and `preload.mjs` file

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

2. Move the folders of the application in the following order

```bash
src/
├── main/                 # Main process files
│   ├── main.js           # Electron Main Process entry
│   └── preload.mjs        # Preload script
├── renderer/             # Renderer process files
│   ├── index.html        # Entry HTML for the UI
│   └── main.jsx          # Main React/JSX entry point
└── ui/                   # UI components and styles
    ├── app.jsx           # Main UI component
    ├── app.css           # Styles for the app
    └── index.css         # Global styles

```
{% endstep %}

{% step %}
### Create/edit vite.config.js

For Vite to recognize the new file structure create/edit the `vite.config.js` file

{% code title="vite.config.js" %}
```javascript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

// https://vite.dev/config/
export default defineConfig({
  root: "./src/renderer",
  plugins: [react()],
  publicDir: "../ui/public",
  build:{
    outDir:"../../build/renderer"
  },
  base: "./",
});
```
{% endcode %}
{% endstep %}

{% step %}
### Configure `package.json` to launch electron

1. Install additional dependencies

<pre><code><strong>yarn add concurrently wait-on
</strong></code></pre>

These packages allow node to run Vite and electron together through one command.

2. Update the `package.json` file to launch electron application

{% code title="package.json" %}
```json
"type": "module",
  "scripts": {
    "electron:start": "electron ./src/main/main.js",
    "renderer:dev": "vite",
    "renderer:build": "vite build",
    "renderer:preview": "vite preview",
    "dev": "concurrently --kill-others \"yarn renderer:dev\" \"wait-on http://localhost:5173 && cross-env NODE_ENV=development yarn electron:start\"",
  },
  "main": "./src/main/main.js",
```
{% endcode %}


{% endstep %}

{% step %}
### Launch the electron application

In a terminal run:

```
yarn dev
```

This should start the react application in an electron window.
{% endstep %}
{% endstepper %}

This is the basic setup for an electron application along with react, in following section I will discuss how to setup Inter Process Communication (IPC) between the main process and the renderer process.
