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
###


{% endstep %}
{% endstepper %}

