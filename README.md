# Hackcheck Private API docs | Version 1.0
https://hackcheck.io - https://discord.gg/hackcheck - https://t.me/hackcheck

Documentation of our private API are found below.


### Endpoints
**Base URL:** hackcheck.io
* /api/v1/lookup/ - Perform qeury searches 
* /api/v1/ip/ - Returns IP address

### Authentication
Our private API is only accessible to those who purchase a *developer* plan at https://hackcheck.io
Once you purchase a developer plan you can navigate to https://hackcheck.io/profile, your API key will be displayed on the page.
To authorize yourself on our private API you need to use the `key` parameter as seen below.
`/api/v1/lookup/?key=0000-000-000-00000000&email=example@gmail.com`

### /lookup
This endpoint is used to perform various queries against our database to get the information you're looking for.

#### Queires
Hackcheck currently offers six queires
- Email Address `email`
- Username      `username`
- Password      `password`
- IP Address    `ip`
- Phone Number  `phone`
- Domain Name   `domain`

Keep in mind that some plans cannot use curtain queires.
There are also security measures in place to prevent these queires being abused.

### Response Handling
Our API consists of two response bodies
#### Valid Response
```
{
    "found": 0,
    "results": [],
    "elapsed": "10ms",
    "success": true
}
```
#### Error Response
```
{
    "message": "error message",
    "success": false
}
```
These two body structures make it easy for developers to parse our responses with efficiency and ease. 


### Request Example
```
https://hackcheck.io/api/v1/lookup/?key=0000-000-000-00000000&email=example@gmail.com
```
#### Response Example
```
{
    "found": 2,
    "results": [
        {
            "email": "example@gmail.com",
            "password": "StrongPassword123!",
            "username": "johnsmith",
            "ip": "1.1.1.1",
            "phone": "7777777777",
            "Source": {
                "date": "2022-04",
                "name": "Realwebsite.com",
                "description": "This is real data from a real breach."
            }
        },
        {
            "email": "example@gmail.com",
            "password": "p@ssword!",
            "username": "crazymike",
            "ip": "2.2.2.2",
            "phone": "3333333333",
            "Source": {
                "date": "2019-11",
                "name": "Realwebsitetwo.com",
                "description": "This is real data from another real breach."
            }
        }
    ],
    "elapsed": "106ms",
    "success": true
}
```
