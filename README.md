# Hackcheck Private API Docs | Version 2.0
https://hackcheck.io - https://discord.gg/hackcheck - https://t.me/hackcheck

Documentation of our private API are found below.


### Endpoints
**Base URL:** dev.hackcheck.io
* /api/v2/lookup/ - Perform qeury searches 

### Authentication
Our private API is only accessible to those who purchase a _developer_ plan at https://hackcheck.io
To authenticate a request on our API you need two things
- API key
- whitelisted IP address
Once you purchase a developer plan you can navigate to https://hackcheck.io/profile, there you will be able to copy your `API key` and authorize whichever IP address you want.

### /api/v2/lookup/
This endpoint is used to perform various queries against our database to get the information you're looking for.

We currently limit responses to a maximum of 10,000 results, this is to ensure request time is reasonable and to prevent abuse.

#### Queires
Hackcheck currently offers six  queires.
- Email Address `email`
- Username      `username`
- Password      `password`
- IP Address    `ip`
- Phone Number  `phone`
- Domain Name   `domain`

Keep in mind that some plans cannot use all queries. 

### Response Handling
Our API consists of two response bodies.
#### Valid Response
```
{
    "found": 0,
    "results": [],
    "elapsed": "1ms",
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

#### Breakdown
`found` - The 'found' element is a INT that represents the number of results that were found for your query.

`results` - The 'results' element is a Array that contains all of the results found.

`elapsed` - The 'elapsed' element is a String that represents the milliseconds it took our server to return results for your query.

`success` - The 'success' element is a Boolean that represents if the API request was successful or failed

`message` - The 'message' element is a String that contains a message, this element is only returned if success is false.

#### Request Example
```
https://dev.hackcheck.io/api/v2/lookup/?key=0000000000000000000000&email=example@gmail.com
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
    "elapsed": "10ms",
    "success": true
}
```

More features are coming soon, stay updated!
