---
icon: node-js
---

# Node.js Installation

### For Linux (Using NVM)

{% stepper %}
{% step %}
### Install NVM (Node Version Manager)

1. Open a terminal and install NVM:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
```

2. Restart the terminal or run:

```bash
source ~/.bashrc
```
{% endstep %}

{% step %}
### Install Node using NVM

1. Install Node.js LTS version

```bash
nvm install --lts
```

2. Set the default Node.js verison (optional)

```bash
nvm use --lts
```


{% endstep %}

{% step %}
### Verify Installation

1. Check the Node.js Version:

```bash
node -v
```

output should be similar to:

```bash
v22.12.0
```

2. Check the `npm` version:

```bash
npm -v
```

Output should be similar to:

```bash
10.9.0
```
{% endstep %}
{% endstepper %}

### For Windows and MacOS



{% stepper %}
{% step %}
### Download Node.js

1. Visit the [Node.js Download Page](https://nodejs.org/en/download/prebuilt-installer).
2. Download the **Windows Installer** (`.msi)` or **macOS Installer** (`.pkg`) fir the desired version (LTS or Current)
{% endstep %}

{% step %}
### Install Node.js

1. Open the downloaded `.msi` or `.pkg` file.
2. Follow the installation wizard, ensure `npm` is selected for installation.
{% endstep %}

{% step %}
### Verify Installation

1. Open Command Prompt, Powershell or Terminal and run:

```bash
node -v
npm -v
```
{% endstep %}
{% endstepper %}
