# Events API
## API for sending the events from a publisher or an advertiser side
#### HTTP endpoint

`GET http://ad.dispply.com/v2/events`

#### (GET) request parameters 

### Query Parameters

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
ip | false | Sender ip | Device IP
user_agent | false | Sender user-agent | Device user-agent
sdk_version | Yes | No | Version of SDK used by sender
ag_key | Yes | No | Token for identifying the audience group
ios_idfa | Yes, for iOS| No | iOS advertising ID
gaid | Yes, for android | No | Android advertising ID
user_key | false | No | Custom user identifier
event_name | false | No | Event name: Purchase, Login, etc
sale | false | No | Purchase amount in USD. Ex. 0.5
created_at | false | No | Event date

