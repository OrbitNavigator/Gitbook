---
description: This page guides how to setup a react app using Vite as bundler
icon: react
---

# React Application



{% stepper %}
{% step %}
### Initialize a Vite React Application

1. Open a terminal in the directory where you want to create your project:
2. Use the yarn create command to create a new Vite Project:

```bash
yarn create vite
```

Enter the project name and framework when prompted

```bash
√ Project name: ... OrbitNavigator
√ Package name: ... orbitnavigator
√ Select a framework: » React
√ Select a variant: » JavaScript
```
{% endstep %}

{% step %}
### Navigate to the Project Directory

```bash
cd OrbitNavigator
```
{% endstep %}

{% step %}
### Install Dependencies

Run the following command to install all the required dependencies:

```bash
yarn install
```
{% endstep %}

{% step %}
### Start the Development Server

1. Start the Vite development server:

```bash
yarn dev
```

2. Press `O + enter`  on the terminal, this will open a browser window with an example react application loaded.
{% endstep %}
{% endstepper %}

### Project Structure

The Project Structure should look like this

```bash
my-react-app/
├── node_modules/
├── public/
├── src/
│   ├── App.jsx
│   ├── main.jsx
│   ├── app.css
│   └── index.css
├── .gitignore
├── index.html
├── package.json
├── vite.config.js
└── yarn.lock
```
