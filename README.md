# Setup-Electrons

Install electron. Open Terminal -> Go to project root directory and run below command
                npm i -D electron@latest

      2. Create a main.js file in the root of project’s directory (Page 2)

      3. Next, update your project’s package.json file so that it can look for our Electron file as the main entry point.

{
 "name": "app-name",
 "version": "0.0.0",
 "main": "main.js", 
 ...

     4. Add an npm script to build the Angular app and then launch the Electron app


"scripts": {
  "electron": "electron .",

 "electron-aot": "ng build --prod && electron ."

  ...

     5. Once everything is done run

     npm run electron


Reference : https://coursetro.com/posts/code/125/Angular-5-Electron-Tutorial



main.js

const {app, BrowserWindow} = require('electron')

const path = require('path')

const url = require('url')

let win

function createWindow () {

win = new BrowserWindow({width: 800, height: 600})

// load the dist folder from Angular

win.loadURL(url.format({

  // pathname: path.join(__dirname, 'dist/ktd-web/index.html'),

  pathname: 'http://ipaddress'

  // protocol: 'file:',

  // slashes: true

}))

// Open the DevTools optionally:

// win.webContents.openDevTools()

win.on('close', function(e){

  var choice = require('electron').dialog.showMessageBox(this,

      {

        type: 'question',

        buttons: ['Yes', 'No'],

        title: 'Confirm',

        message: 'Are you sure you want to quit?'

     });

     if(choice == 1){

       e.preventDefault(); }

  });

win.on('closed', () => {

    console.log("KTD Closed");

    mainWindow = null;

  })

}

app.on('ready', createWindow)

app.on('window-all-closed', () => {

if (process.platform !== 'darwin') {

  app.quit()}

})

app.on('activate', () => {

if (win === null) {

  createWindow()

}})



InnoSetup: Create execute file for Windows OS 


Run the above commands to create an installer for mac and windows os, the release-builds folder is created in the root folder.
Download inno setup compiler from http://www.jrsoftware.org/isinfo.php
Get script (UI to develop script is available. It is better to go for available .iss) or create a new script
Compile the script.
Run the EXE installer. The installer will be available inside o/p directory specified in the script.
Note : It is advisable to generate AppID manually to ensure unique signature.
optional : Tools>Generate GUID/ctl+shift+G
