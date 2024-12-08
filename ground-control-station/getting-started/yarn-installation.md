---
icon: yarn
---

# Yarn Installation

By default node uses `npm` as package manager of installing and managing node packages, which are basically libraries for JavaScript to provide functionality that I am too lazy to implement on my own. I am not going to use `npm` as it is slow as compared to `yarn` , another node package manager made by facebook.&#x20;

### Limitations of npm over Yarn

1. **Speed and Performance -** `npm`  is slower than `yarn` , `yarn`  uses caching mechanism and parallel installation, making it much faster than `npm` .
2. **Offline Mode -** `Yarn`  offers offline support, once a package has been installed, it is cached locally, and it can be installed offline without fetching it again.
3. **Lockfile Management -** the `yarn.lock` file is more robust, stable and reliable when managing dependency versions

{% stepper %}
{% step %}
### Install Yarn globally using npm

1. install `Yarn` globally using `npm`:

```bash
npm install --global yarn
```

2. Verify the installation:

```bash
yarn -v
```
{% endstep %}
{% endstepper %}

