# Test server load 

## NPM libraries
- https://www.npmjs.com/package/loadtest

## Artillery - Test server load
- https://artillery.io/

## PM2
- https://github.com/Unitech/pm2/issues/2300

## MySql
- https://www.sitepoint.com/optimize-mysql-indexes-slow-queries-configuration/



```JavaScript
//TODO Send multiplayer request code to get game.
//TODO Send multiplayer score
//TODO Get multiplayer results.
const r = require("request-promise");

const apiBaseUrl = "https://aniversaredev.carrefour.ro/api"; //"https://party-dev.m75.ro/api";
const usersList = [];
const usersError = [];

const test = async () => {
  try {
    const user = {};
    //TODO Login with random number
    user.phoneNumber = generateRandomPhoneNumber();
    const testLogin = await r.post(apiBaseUrl + "/auth/login", {
      form: { phoneNumber: user.phoneNumber }
    });
    user.smsCode = JSON.parse(testLogin).response;

    // const tokenJson = await r.post(apiBaseUrl + "/auth/sms", {
    //   form: { phoneNumber: user.phoneNumber, code: user.smsCode }
    // });
    // user.token = JSON.parse(tokenJson).response;

    // //TODO Set username if not set
    // const patchUsername = await r.patch(apiBaseUrl + "/users", {
    //   form: { username: user.phoneNumber },
    //   auth: {
    //     bearer: user.token
    //   }
    // });
    // user.username = JSON.parse(patchUsername).response.user.username;

    // const tokenJsonRefresh = await r.post(apiBaseUrl + "/auth/refresh", {
    //   auth: {
    //     bearer: user.token
    //   }
    // });
    // user.token = JSON.parse(tokenJsonRefresh).response;

    usersList.push(user);
  } catch (err) {
    usersError.push(err);
    console.error(err);
  }
};

function generateRandomPhoneNumber() {
  const randNumber = String(Math.ceil(Math.random() * 100000000));
  const phoneNumber = "07" + formatNumber(randNumber, 8);
  return phoneNumber;
}

function formatNumber(num, size) {
  var s = "0000000000" + num;
  return s.substr(s.length - size);
}

const runAllTests = async () => {
  const testRequestList = [];
  for (let i = 0; i < 500; i++) {
    testRequestList.push(test());
    console.log("index", i);
  }
  const result = await Promise.all(testRequestList);
  console.log("Success: ", usersList.length);
  console.log("Error: ", usersError.length);
};

runAllTests();

```
