# Events API
## API for sending the events from a publisher or an advertiser side
#### HTTP endpoint

`GET http://ads.hyperadx.com/v2/events`

#### (GET) request parameters 

### Query Parameters

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
ip | false | Sender ip | Device IP
event_name | Yes | No | Event name: Purchase, Login, etc
user_agent | No | Sender user-agent | Device user-agent
lat | No | No | Sender lattitude
lng | No | No | Sender longitude
sdk_version | No | No | Version of SDK used by sender
token | Yes | No | Token for authentication
ios_idfa | Yes, for iOS| No | iOS advertising ID
gaid | Yes, for android | No | Android advertising ID
user_key | No | No | Custom user identifier
created_at | No | No | Event date ("%Y-%m-%d")

