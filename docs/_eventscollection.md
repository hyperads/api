# Events API
## API for sending the events from publisher/advertiser 
#### HTTP endpoint

`GET http://ad.dispply.com/v2/events`

#### (GET) request parameters 

### Query Parameters

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
ip | false | Requester's ip | Device IP
user_agent | false | Requester's user-agent | Device user-agent
sdk_version | Yes | No | Version of used SDK
ag_key | Yes | No | Token for identifying audience group
ios_idfa | Yes, for iOS| No | iOS advertising ID
gaid | Yes, for android | No | Android advertising ID
user_key | false | No | Custom user identifier
event_name | false | No | Name of event: Purchase, Login etc
sale | false | No | Amount of purchase in USD. Ex. 0.5
created_at | false | No | Date of event

