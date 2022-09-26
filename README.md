# clickup-api-postman

![](https://img.shields.io/badge/Tools-Postman-informational?style=flat&logo=postman&logoColor=white&color=blueviolet)

![postman-run-folder](https://user-images.githubusercontent.com/17500766/191484957-e40bfa50-3e73-412a-b0fa-780b70e679f9.gif)


Collection of requests in Postman created during the learning process. Includes dynamic variables, tests, Postman environment. 

App links : [ClickUp](https://clickup.com/), [ClickUp API Docs](https://clickup.com/api )

This README also documents some issues that I found during testing. 

## Installation

You can download Postman using this [link](https://www.postman.com/). Postman is an API client that makes it easy to test HTTP requests.

Then you need to import collection and environment from this repository into Postman. Please clone the repo, select *Import* in your Postman's workspace and choose collection and environment files. You're all set! 

Well.. almost :wink: Please read Authentication part of this README to start sending requests. 

## Features

This collection interacts with following resources: 

Attachments :purple_circle: Authorization :purple_circle: Checklists :purple_circle: Dependencies :purple_circle: Lists :purple_circle: Spaces :purple_circle: Tasks :purple_circle: Folders 

Right now collection contains 66 requests. The whole run takes less than 30 seconds.

![image](https://user-images.githubusercontent.com/17500766/192369606-bc7e6749-3e35-40d2-b74b-d1b1a7912dcb.png)


:white_check_mark: you can run specific request, folder or the whole collection

:white_check_mark: each folder creates its own test data and deletes them at the end 

:white_check_mark: environment variables are used to keep data related to environment (like url, API key)

:white_check_mark: collection variables are used to keep resources data so they can be passed between requests

![image](https://user-images.githubusercontent.com/17500766/192370181-33dcc666-8b2b-4f16-8b1d-0c03f77497d2.png)


:white_check_mark: each request is tested for response code and time. I decided not to write more specific tests (like comparing request body and response body data) in Postman. I believe there are better tools for that purpose. 

## Authentication

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

### Authentication in Attachments

ClickUp API V2 docs describes only `POST attachment`. From the UI, user can also view, delete, change the attachment's name. After some digging I managed to include these methods in my collection as well. They have different base URL and don't use API Key or Oauth token to authenticate. It appears that they use token set by `cu_jwt` cookie during login. Unfortunately I was not able to recreate login action in Postman due to usage of Recaptcha V3. If you want to run these 3 requests, please add your `cu_jwt` cookie in collection variables.

### Team ID

For some requests you need to provide team ID. You will find it as part of the URL after login. This value should be copied and pasted in environment variable `teamId` 

![26 09 2022_22 24 42_REC](https://user-images.githubusercontent.com/17500766/192373451-8bc338cf-974d-4171-83b1-5d7882ca19e3.png)

## Issues found

During creation of this collection I found several API bugs. I will not post here any details as I don't find it fair to the company. So far I reported 3 of them to ClickUp's Tech Support. 


![clickup-bug](https://user-images.githubusercontent.com/17500766/191612855-b84f3ff5-e0ec-4749-873f-1eb3329a3e4a.png)

