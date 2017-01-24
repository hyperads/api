# VAST player API
### API for obtaining VAST XML for applying in DFP or MoPub

#### HTTP endpoint

`GET http://ads.hyperadx.com/v2/vast/:placement_id`

#### (GET) request parameters 


### Query Parameters

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
ip | false | Sender ip | Device IP
user_agent | false | Sender user-agent | Device user-agent
gaid | false | No | Google identifier for Advertiser
ios_idfa | false | No | iOS identifier for Advertiser
euid | For Mopub | No | Mopub identifier

MoPub sample – http://ads.hyperadx.com/v2/vast/wp8Jb87v?v=3.0&ip=%%IPADDRESS%%&user_agent=%%USERAGENT%%&eudid=%eudid!
