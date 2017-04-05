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
bundle_id | Yes, for apps | No | Appstore or Google Play identifier for application
user_agent | No | Sender user-agent | Device user-agent
connection_type | No | Sender connection type | Device connection type
carrier | No | Sender carrier | Device carrier
lat | No | No | Sender lattitude
lng | No | No | Sender longitude
yob | No | No | Year of birth
age | No | No | Age
gender | No | No | male or female
keywords | No | No | Keywords
sdk_version | No | No | Version of SDK used by sender
token | Yes | No | Token for authentication
ios_idfa | Yes, for iOS| No | iOS advertising ID
gaid | Yes, for android | No | Android advertising ID
user_key | No | No | Custom user identifier
created_at | No | No | Event date ("%Y-%m-%d")


### Events with code and additional parameters

Authenticate events
- Login (Code: 102)
- Open (Code: 103)

- Registration (Code: 101)

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
success | No | No | Registration status

eCommerce events

- 201 Add to Wishlist
- 202 Add to Cart
- 203 Added Payment Info
- 204 Reservation
- 205 Checkout Initiated

- Purchase (Code: 206)

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
content_id | No | No | Content unique identifier
content_type | No | No | Content type
quantity | No | No | Quantity
price | No | No | Content price
revenue | No | No | Real revenue from purchase
currency | No | No | Currency


Content events

- Search (Code: 301)

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
keyword | No | No | Search keyword
content_type | No | No | Content type
success | No | No | Completion status

- Content View (Code: 302)

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
content_id | No | No | Content unique identifier
content_type | No | No | Content type

Gaming events

- Tutorial Completed (Code: 401)

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
success | No | No | Completion status

- Level Achieved (Code: 402)

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
level | No | No | Game level
score | No | No | Game score in current moment 
lives | No | No | Game lives in current moment 
attempts | No | No | Attempts to achive game level
failed_attempts | No | No | Failed attempts to achive game level


- 403 Achievement Unlocked
- 404 Spent Credit

Social events

- 501 Invite
- 502 Rated
- 504 Share
