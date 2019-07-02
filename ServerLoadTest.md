# Test server load 

## NPM libraries
- https://www.npmjs.com/package/loadtest

## 


//TODO Set username if not set
//TODO Send multiplayer request code to get game.
//TODO Send multiplayer score
//TODO Get multiplayer results.
const request = require("request-promise")


const test = async () => {
    try {
        const testApi = await r.get('https://party-dev.m75.ro/api/')
        console.log("Test api response: ", testApi)
        //TODO Login with random number
        const testLogin = await r.post('https://party-dev.m75.ro/api/auth/login', { form: { phoneNumber: "0738334197" } });
        console.log(JSON.parse(testLogin))
        // console.log('Test login:', { phoneNumber: "0738334197", code: JSON.parse(testLogin).response }); // Print the HTML for the Google homepage.

        const testSms = await r.post('https://party-dev.m75.ro/api/auth/sms', { form: { phoneNumber: "0738334197", code: JSON.parse(testLogin).response } });
        console.log('Test sms:', testSms); // Print the HTML for the Google homepage.
    }
    catch (err) {
        console.error(err)
    }
}

test()
