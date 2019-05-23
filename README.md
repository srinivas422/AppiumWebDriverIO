About | Getting Started | Installation | Run Tests | Page Objects | Finding Elements | Reports

About
Currently this framework has been developed to run scripts in ANDROID platform with real device.

The tests run on Android Native App.

Tech Stack
Appium - This is the node server which interacts with the mobile devices
WebdriverIO - It is the selenium webdriver api bindings for node.js, It has a very simple api which could be used to automate web & browser apps in a fast and scalable way.
Javascript - JavaScript, often abbreviated as JS, is a high-level, interpreted programming language that conforms to the ECMAScript specification. JavaScript has curly-bracket syntax, dynamic typing, prototype-based object-orientation, and first-class function

Getting Started
Pre-requisites
NodeJS installed globally in the system. https://nodejs.org/en/download/

JAVA(jdk) installed in the system.

Andriod(sdk) installed in the system.

Set JAVA_HOME & ANDROID_HOME paths correctly in the system.

Text Editor/IDE (Optional) installed-->Sublime/Visual Studio Code/Brackets.

Tip: Install npm install -g appium-doctor and run it from the command-line which checks if your java jdk and android sdk paths are set correctly or not.

Installation
Setup Scripts
Clone the repository into a folder
Go inside the folder and run following command from terminal/command prompt
All the dependencies from package.json and typescript typings would be installed in node_modules folder.
npm install webdriverio --> downloads the WebdriverIO into repository if we don't have it already.
Before installing the test runner, we need to initialize an empty NPM project (this will allow us to the cli to install needed dependencies).
npm init -y --> Use this command to initialise
$ npm i --save-dev @wdio/cli  --> we need to install the cli by running this command.
./node_modules/.bin/wdio config --> Run this command to generate a configuration file that stores all of our WebdriverIO settings

To write tests using next generation JavaScript features you can add Babel as compiler for your test files. For that first, install the necessary Babel dependencies using below command.
npm install --save-dev @babel/core @babel/cli @babel/preset-env @babel/register
Make sure your babel.config.js is configured properly.

Run Tests
First step is to start the appium server by using the command : npm run appium or appium Desktop app
Next you have to transpile/compile your typescript files to javascript files, you could do this by running the command -
npm run build
Next step is to execute the config files.

wdio.config.js - This config file is used to run tests in real mobile native apps. We will have to change the appium settings to run tests in your device.
capabilities: [
{
        platformName: "Android",
        platformVersion: "7.0",
        deviceName: "Samsung Galaxy S7",
        appPackage: "com.ebay.mobile",
        appActivity: "com.ebay.mobile.activities.MainActivity",
        automationName: "UiAutomator2",
        fullReset:false
}
],
To know the device name we just run the adb devices command which comes out of the box from Android SDK.
To Know the appActivity and appPackage, we need to connect to device to Android Studio and use the debugger to see the required details while running the App.

The node command to run Native app tests of this project is - Goto the project foder, open the terminal or commandline and use below command to run the wdio tests.
./node_modules/.bin/wdio wdio.conf.js

npm run app-test
The above command which is set in package.json internally calls the WebdriverIO's binary wdio ./config/wdio.config.js and runs the app config file.

Page Objects
This framework is strictly written using page-object design pattern.

class ebayhomepage{

    get registerbtn() { return $('id=button_register') }
    get registrationtitle_btn() { return $('id=title') }
    
    click_registerbtn() { 
        this.registerbtn.waitForDisplayed(30000)
        console.log("test")
        this.registerbtn.click();    
    }
    
    registrationTitle_Text(){
      return this.registrationtitle_btn.getText() 
    }
}
/*
Public Interface - export instances of classes
**/
export default new ebayhomepage()

Finding-Elements
Best way to find elements in native mobile apps is using UIAutomatorViewer or we can use Appium inspector.

Reports
Currently this project has just initial setup for Allure-Reports. WebdriverIO's wdio-allure-reporter helps us generate detailed reports of our mobile automated tests. Once the test execution is finished you would find the allure-results folder generated automatically. Then you would have to run the following command to generate HTML Report

npm run report