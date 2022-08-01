# Endpoints
**Base URL:** api.hackcheck.io
* /api/v2/lookup - Perform query searches 

### Requirements
Anybody who purchase a plan is allowed to use our on-site search functionality, however, only those who purchase a _developer_ plan have access to use our private API.

## Authentication
To authenticate a request on our API you need the following
- API Key
- Whitelisted IP Address

If you are having trouble authenticating your IP address, visit [here](https://api.hackcheck.io/api/v2/ip) and make sure the IP you are entering on your [profile](https://hackcheck.io/profile) matches the IP you are shown.
Once you've purchase a developer plan you can navigate to your [profile](https://hackcheck.io/profile), there you will be able to copy your `API key` and authorize whichever IP address you'd like.

---
## /api/v2/lookup
This endpoint is used to perform various queries against our database to get the information you're looking for.


## Queries
Hackcheck currently offers six Queries.
- Email Address `email`
- Username      `username`
- Full Name     `name`
- Password      `password`
- IP Address    `ip`
- Phone Number  `phone`
- Domain Name   `domain`

Keep in mind that some plans cannot use all of these queries, for more details visit [plans](https://hackcheck.io/plans). 


## Response Handling
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

---
## Breakdown
`found` - INT that represents the number of results that were found for your query.

`results` - Array that contains all of the results found.

`elapsed` - String that represents the milliseconds it took our server to return results for your query.

`success` - Boolean that represents if the API request was successful or if it failed.

`message` - String that contains a message, this element is only returned if success is false.

As of right now the `results` array is limited to 20,000 unique results, however the `found` integer will still go beyond 20,000. This is to prevent abuse.

---
## Examples
#### Request Example
`GET https://api.hackcheck.io/api/v2/lookup?key=0000000000000000000000&email=example@gmail.com`

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
    "elapsed": "5ms",
    "success": true
}
```

---
### Rate Limits
**Warning:** If you request our API at a rate of 30 requests per second or more for a prolonged amount of time you will be temporarily blocked.

A rate limit is the allowed requests per second someone is allowed to send requests & receive a response to our API. The rate limit you receive depends on the plan you purchase.
If you want to have insight on your current rate limit you can use the following response headers.

```hc-allowed-rate``` - This number represents the requests per second you are allowed to send using the current API key.

```hc-current-rate``` - This number represents the numbers of requests you've send in the last second.
