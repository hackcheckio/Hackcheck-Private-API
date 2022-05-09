# Hackcheck Private API Docs | Version 2.0
[hackcheck.io](https://hackcheck.io) - [discord.gg/hackcheck](https://discord.gg/hackcheck) - [t.me/hackcheck](https://t.me/hackcheck)

Documentation of our private API are found below.


### Endpoints
**Base URL:** api.hackcheck.io
* /api/v2/lookup/ - Perform query searches 

### Authentication
Our private API is only accessible to those who purchase a _developer_ plan at [hackcheck.io](https://hackcheck.io)
To authenticate a request on our API you need two things
- API key
- whitelisted IP address


Once you purchase a developer plan you can navigate to your [profile](https://hackcheck.io/profile), there you will be able to copy your `API key` and authorize whichever IP address you want.

---
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
`found` - A INT that represents the number of results that were found for your query.

`results` - A Array that contains all of the results found.

`elapsed` - A String that represents the milliseconds it took our server to return results for your query.

`success` - A Boolean that represents if the API request was successful or failed

`message` - A String that contains a message, this element is only returned if success is false.

#### Request Example
```
https://api.hackcheck.io/api/v2/lookup/?key=0000000000000000000000&email=example@gmail.com
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
---
### Regex

Our API provides Regex support to help you find what you're looking for easier.

`*` - Represents zero or more characters.

`_` - Represents a single character.

If you want to use regex you need to enable the `regex` parameter like as follows.

`https://api.hackcheck.io/api/v2/lookup/?key=0000000000000000000000&regex=true&email=example_@gmail.com`

#### Examples
   
`Query:` example*@gmail.com

`Response:` example-1234@gmail.com, exampletexts@gmail.com, examplesalad@gmail.com, etc


`Query:` example_@gmail.com

`Response:` examples@gmail.com, example1@gmail.com, example2@gmail.com, etc

---
### Rate Limits

A rate limit is the allowed requests per second someone is allowed to send requests & receive a response to our API. Different developer plans get different rate limits, some better than others. We rate limit by API key.

If you want to have insight on your current rate limit you can use our two custom headers.

```hc-allowed-rate``` - This number represents the requests per second you are allowed to send using the current API key.

```hc-current-rate``` - This number represents the current requests per second you are sending.

More features are coming soon, stay updated!
