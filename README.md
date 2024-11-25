---
# **Appium WebDriverIO Project Setup and Usage Guide**

This guide provides all necessary steps for setting up an Appium WebDriverIO project, installing dependencies, running tests, and using Appium Web Inspector to inspect your app.

## **Prerequisites**

Before you begin, ensure the following tools are installed:

- **Node.js** (v14 or later): [Download Node.js](https://nodejs.org/)
- **Appium**: Install globally via npm
- **Appium Inspector**: For inspecting UI elements in your app

---

## **Step 1: Install Node.js and Appium**

1. **Install Node.js**  
   Check if Node.js is installed:
   ```bash
   node -v
   npm -v
   ```
   If not installed, download and install from the [official Node.js website](https://nodejs.org/).

2. **Install Appium Globally**  
   Install Appium via npm:
   ```bash
   npm install -g appium
   ```
   Verify the installation:
   ```bash
   appium -v
   ```

---

## **Step 2: Set Up Your Appium WebDriverIO Project**

1. **Create a New Project Folder**
   Create a new folder for your project and navigate into it:
   ```bash
   mkdir appium-webdriverio
   cd appium-webdriverio
   ```

2. **Initialize a Node.js Project**
   Initialize a new Node.js project:
   ```bash
   npm init -y
   ```

3. **Install Required Dependencies**
   Install **Appium**, **WebDriverIO**, and **Mocha** for testing:
   ```bash
   npm install --save-dev appium webdriverio mocha
   ```

4. **Install Appium WebDriverIO Service**
   Install the Appium service for WebDriverIO to communicate with the Appium server:
   ```bash
   npm install --save-dev wdio-appium-service
   ```

5. **Install Babel (Optional)**
   If you want to use modern JavaScript features (ES6+), install Babel:
   ```bash
   npm install --save-dev @babel/core @babel/cli @babel/preset-env
   ```

---

## **Step 3: Configure WebDriverIO**

1. **Generate WebDriverIO Configuration**
   Run the following command to generate the WebDriverIO configuration file:
   ```bash
   npx wdio config
   ```
   Answer the prompts with the following options:
   - **Test framework**: Choose `Mocha`.
   - **Where are your tests located?**: Choose `./test/specs/`.
   - **Do you want to use a reporter?**: Choose `Allure` or any other reporter.
   - **Which services do you want to use?**: Choose `Appium`.

2. **Create Test Folder**
   Create a `test/specs` directory where you will place your test files:
   ```bash
   mkdir -p test/specs
   ```

3. **Add Your Test Script**
   In the `test/specs` folder, create a file called `dialog.test.js` and add the following test example:

   ```javascript
   const { expect } = require('chai');

   describe('Dialog', () => {
       it('should display a dialog', async () => {
           const button = await $('~Accessibility');  // Example selector from Appium Inspector
           await button.click();

           const result = await $('~ResultID');  // Example result element
           const resultText = await result.getText();
           expect(resultText).to.equal('Expected Result');
       });
   });
   ```

---

## **Step 4: Open Appium Server and Inspector**

1. **Start Appium Server**
   Start the Appium server with the following command:
   ```bash
   appium
   ```
   This will start the server at the default URL: `http://127.0.0.1:4723`.

2. **Open Appium Inspector**
   - Download **Appium Inspector** from [here](https://github.com/appium/appium-inspector).
   - Launch the Appium Inspector.
   - Set the desired capabilities:
     ```json
     {
       "platformName": "Android",
       "platformVersion": "11",
       "deviceName": "emulator-5554",
       "app": "/path/to/your/app.apk",
       "automationName": "UiAutomator2"
     }
     ```
   - Click **Start Session** to connect to the app and begin inspecting elements.

   **Note**: If you're using the browser version of Appium Inspector, run the server with the `--allow-cors` flag:
   ```bash
   appium --allow-cors
   ```

---

## **Step 5: Run Tests**

Once the Appium server is running and the app is connected, you can run your tests using WebDriverIO's test runner:

1. **Run Tests with Mocha**  
   Execute the following command to run the test:
   ```bash
   npx wdio run wdio.conf.js
   ```

   If you configured the test script correctly, WebDriverIO will run the test, interact with the app, and print the results.

---

## **Step 6: Debugging and Logs**

- **Check Appium Logs**: The Appium server logs will display detailed information about interactions between WebDriverIO and the Appium server.
- **WebDriverIO Logs**: WebDriverIO will provide additional logs for the test execution.

To check the logs of your Appium server:
```bash
appium
```

---

## **Step 7: Closing the Appium Server**

Once your tests are completed, you can stop the Appium server by pressing `Ctrl+C` in the terminal where it is running.

---
## **Step 8: Appium Inspector
https://inspector.appiumpro.com/


## **Troubleshooting**

- **Error: Could not connect to Appium server**  
  Make sure the Appium server is running and accessible at the specified URL (`http://localhost:4723/` or your custom port).
  
- **Error: Cannot find desired elements**  
  Use Appium Inspector to validate the locators. Ensure that the element is accessible and visible on the screen.

---

## **Additional Resources**

- [Appium Documentation](http://appium.io/docs/en/about-appium/intro/)
- [WebDriverIO Documentation](https://webdriver.io/docs/gettingstarted/)
- [Appium Inspector GitHub](https://github.com/appium/appium-inspector)

---