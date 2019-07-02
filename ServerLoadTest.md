# Test server load 

## NPM libraries
- https://www.npmjs.com/package/loadtest

## 



//TODO Send multiplayer request code to get game.
//TODO Send multiplayer score
//TODO Get multiplayer results.
const request = require("request-promise")


const usersList = []

const test = async () => {
    try {
        const user = {}
        const testApi = await r.get('https://party-dev.m75.ro/api/')
        console.log("Test api response: ", testApi)
        //TODO Login with random number
        user.phoneNumber = generateRandomPhoneNumber();
        const testLogin = await r.post('https://party-dev.m75.ro/api/auth/login', { form: { phoneNumber: user.phoneNumber } });
        user.smsCode = JSON.parse(testLogin).response;
        
        const tokenJson = await r.post('https://party-dev.m75.ro/api/auth/sms', { form: { phoneNumber: user.phoneNumber, code: user.smsCode } });
        user.token = JSON.parse(tokenJson).response
        
        //TODO Set username if not set
        console.log('User result:', user); // Print the HTML for the Google homepage.
    }
    catch (err) {
        console.error(err)
    }
}

function generateRandomPhoneNumber() {
    const randNumber = String(Math.ceil(Math.random() * 100000000))
    const phoneNumber = "07" + formatNumber(randNumber, 8)
    return phoneNumber
}

function formatNumber(num, size) {
    var s = "0000000000" + num;
    return s.substr(s.length - size);
}

console.log(generateRandomPhoneNumber())

test()
