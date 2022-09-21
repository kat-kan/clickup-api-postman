# clickup-api-postman

![](https://img.shields.io/badge/Tools-Postman-informational?style=flat&logo=postman&logoColor=white&color=blueviolet)

![postman-run-folder](https://user-images.githubusercontent.com/17500766/191484957-e40bfa50-3e73-412a-b0fa-780b70e679f9.gif)


Collections of requests in Postman created during the learning process. Include dynamic variables, tests, Postman environment. 

App links : [ClickUp](https://clickup.com/), [ClickUp API Docs](https://clickup.com/api )

This README also documents some issues that I found during testing. 

## Installation

You can download Postman using this [link](https://www.postman.com/). Postman is an API client that makes it easy to test HTTP requests.

# Authentication

ClickUp offers 2 ways of autentication: 
* API Key
* Oauth 2.0

My Postman collection can be used either with API Key or Oauth 2.0 tokens. 

To generate your API Key, login to ClickUp and navigate to Profile -> **Apps**. Then copy and paste the key as value of environment variable `key`. After saving the environment all requests should be correctly authenticanted.

Generating Oauth 2.0 token is more complicated. Here are the steps:
* In ClickUp navigate to **Integrations** and select **ClickUp API**
* Enter **App name** of your choice and **Redirect URI** `https://oauth.pstmn.io/v1/browser-callback`
* Copy and paste **Client ID** and **Client Secret** into matching environment variables
* You need also authorization code from the user (a.k.a. you) to get Oauth 2.0 token on their account. To get the code, paste in the browser `https://app.clickup.com/api?client_id={YOUR_CLIENT_ID}&redirect_uri=https://oauth.pstmn.io/v1/browser-callback` and select **Connect workspace**. When you approve, you will be redirected to success page and your code will be available in URL after `code=`. Copy and paste it as value of environment variable `authorizationCode`
* Finally, to get token, you need to send reqeust `Get Access Token` from Authorization folder. Token from the body will be automatically saved as environment variable `oauthToken`. To start using Oauth 2.0 please change Authorization type on collection level. I set API Key auth as default one as it's easier to obtain.





