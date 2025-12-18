# Servify Express
[![Publish to GitHub Packages](https://github.com/Aarondoran/servify-express/actions/workflows/npm-publish-github-packages.yml/badge.svg)](https://github.com/Aarondoran/servify-express/actions/workflows/npm-publish-github-packages.yml)
![NPM Last Update](https://img.shields.io/npm/last-update/servify-express)
![GitHub last commit](https://img.shields.io/github/last-commit/Aarondoran/Servify-express)
![GitHub Repo stars](https://img.shields.io/github/stars/Aarondoran/servify-express?style=flat)
![GitHub watchers](https://img.shields.io/github/watchers/Aarondoran/servify-express?style=flat)
![GitHub forks](https://img.shields.io/github/forks/Aarondoran/servify-express?style=flat)
![GitHub License](https://img.shields.io/github/license/Aarondoran/servify-express)


A simple Node.js package to start an Express server and log the port it's running on.

## my website

[![Website](https://custom-icon-badges.demolab.com/badge/Aarondoran.me-blue?logo=aarondoran-pfp&labelColor=grey)](https://aarondoran.me)

## Installation

### From npm

To install the package from npm, run:

```bash
npm install servify-express
```

### From GitHub Packages

To install the package from GitHub Packages, first configure npm to use the GitHub Package Registry for the `@aarondoran` scope by adding a `.npmrc` file in your project:

```
@aarondoran:registry=https://npm.pkg.github.com
```

Then install the package:

```bash
npm install @aarondoran/servify-express
```

## Usage

After installing the package, you can start an Express server with a single function call. You can also optionally enable rate limiting if you want.

1. **Import the package** into your project.

```javascript
const StartServer = require('servify-express');
// OR if installed from GitHub Packages:
const StartServer = require('@aarondoran/servify-express');
```
2. **Call the ```listen``` method** and pass in the port number.
You may also pass an options object if you want to enable rate limiting.

### Basic example

```
const StartServer = require('servify-express');

StartServer.listen(3000);
```

With optional rate limiting:
```
const StartServer = require('servify-express');

StartServer.listen(3000, {
    rateLimit: {
        windowMs: 60000,
        max: 50
    }
});
```
if you dont add a port it will default to ```3000```.

## How It Works
```listen()``` starts an Express server and logs:
```Server is running on port <PORT_NUMBER>```

Rate limiting is only applied if you include the rateLimit option.
If you leave it out, no rate limiting will be used.

### **License**

This package is licensed under the MIT License.


