# Servify Express
[![Node.js Package](https://github.com/Aarondoran/servify-express/actions/workflows/npm-publish.yml/badge.svg?branch=main)](https://github.com/Aarondoran/servify-express/actions/workflows/npm-publish.yml)
![GitHub Repo stars](https://img.shields.io/github/stars/Aarondoran/servify-express?style=flat)
![GitHub watchers](https://img.shields.io/github/watchers/Aarondoran/servify-express?style=flat)
![GitHub forks](https://img.shields.io/github/forks/Aarondoran/servify-express?style=flat)
![GitHub License](https://img.shields.io/github/license/Aarondoran/servify-express)



A simple Node.js package to start an Express server and log the port it's running on.

## Installation

To install the package, run:

`npm install servify-express`


## Usage

After installing the package, you can use it to easily start an Express server and log the port it is running on. Here’s how to use it in your Node.js application:

1. **Import the package** into your project.

`const StartServer = require('servify-express');`


2. **Call the `use` method** on the `StartServer` object and pass in the port number. The server will automatically start and log the port to the console.

Example usage:

`const StartServer = require('servify-express');`

`// Start server on port 3000`
`StartServer.listen(3000);`

If you don’t pass a port, it will default to port `3000`.

### **How it Works**

- The `listen()` method will start an Express server and log a message to the console: "Server is running on port `<PORT_NUMBER>`".
- You can specify a custom port number, or leave it blank for the default of `3000`.

  
### **License**

This package is licensed under the MIT License.


