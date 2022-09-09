# clickup-api-postman

![](https://img.shields.io/badge/Tools-Postman-informational?style=flat&logo=postman&logoColor=white&color=blueviolet)


Collections of requests in Postman created during the learning process. Include dynamic variables, tests, Postman environment. 

App tested : [ClickUp](https://clickup.com/), [ClickUp API Docs](https://clickup.com/api )

This README also documents API issues that I found during testing. 

## Installation

You can download Postman using this [link](https://www.postman.com/). Postman is an API client that makes it easy to test HTTP requests.

## Issues found

*Attachments*
* Attachment can be created for non existing task (200 OK response; you can also GET/PUT/DELETE such attachment)
* 200 response for PUT with invalid body (I modified values in body for some fields not allowed to be changed. However only response code is incorrect, they are not changed for attachmebnt as a result)
* Misconfigured OPTIONS for Attachments endpoint (for example returns PATCH which returns 404)
* ClickUp API docs describes only `POST attachment`. From the UI, user can also view, delete, change the attachment's name. After some digging I managed to include these endpoints in my collection as well. They have different base URL and don't use personal token to authenticate.


