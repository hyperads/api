# Events API
## API for sending the events from a publisher or an advertiser side
#### HTTP endpoint

`GET http://ads.hyperadx.com/v2/events`

#### (GET) request parameters 

### Query Parameters

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
ip | false | Sender ip | Device IP
event | Yes | No | Pre-defined event code: 206(Purchase), 102(Login), etc
user_agent | No | Sender user-agent | Device user-agent
lat | No | No | Sender lattitude
lng | No | No | Sender longitude
sdk_version | No | No | Version of SDK used by sender
token | Yes | No | Token for authentication
ios_idfa | Yes, for iOS| No | iOS advertising ID
gaid | Yes, for android | No | Android advertising ID
user_key | No | No | Custom user identifier
created_at | No | No | Event date ("%Y-%m-%d")


### Event codes:

Authenticate events
- 101 Registration
- 102 Login
- 103 Open

eCommerce events

- 201 Add to Wishlist
- 202 Add to Cart
- 203 Added Payment Info
- 204 Reservation
- 205 Checkout Initiated
- 206 Purchase

Content events

- 301 Search
- 302 Content View

Gaming events

- 401 Tutorial Completed
- 402 Level Achieved
- 403 Achievement Unlocked
- 404 Spent Credit

Social events

- 501 Invite
- 502 Rated
- 504 Share
