#Ad Serving API 

### HTTP endpoint

`GET http://ads.hyperadx.com/v2/ads/:placement_id`

### (GET) request parameters

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
ip | false | Requester's ip | Device IP
user_agent | false | Requester's user-agent | Device user-agent
content | false | title,icon,main | Required native content separated by comma: title,desc,icon,main
callback | false | No | Callback function for [JSONP](https://en.wikipedia.org/wiki/JSONP) request
ios_idfa | false| No | iOS advertising ID
gaid | false | No | Android advertising ID
limit | false | 1 | Count of advertisements
user_key | false | No | User's ID for frequency capping and profile (replacement for Google's GAID and iOS IFA when disabled ad tracking in iOS 10)

### Request examples (Android)

* 320x50 (you should create 320x50 placement in UI) `http://ads.hyperadx.com/v2/ads/:placement_id?gaid=e8876377-a4b6-4e4e-a151-876ab207a870&ip=24.158.146.111&user_agent=Mozilla%2F5.0+%28Linux%3B+Android+5.1%3B+HTCD
200LVW+Build%2FLMY47O%3B+wv%29+AppleWebKit%2F537.36+%28KHTML%2C+like+Gecko%
29+Version%2F4.0+Chrome%2F51.0.2704.81+Mobile+Safari%2F537.36`

* Native placement (you should create Native placement in UI) `http://ads.hyperadx.com/v2/ads/:placement_id?content=icon,main,title,desc&gaid=e8876377-a4b6-4e4e-a151-876ab207a870&ip=24.158.146.111&user_agent=Mozilla%2F5.0+%28Linux%3B+Android+5.1%3B+HTCD
200LVW+Build%2FLMY47O%3B+wv%29+AppleWebKit%2F537.36+%28KHTML%2C+like+Gecko%
29+Version%2F4.0+Chrome%2F51.0.2704.81+Mobile+Safari%2F537.36`

* Video placement (you should create Video placement in UI) `http://ads.hyperadx.com/v2/ads/:placement_id?gaid=e8876377-a4b6-4e4e-a151-876ab207a870&ip=24.158.146.111&user_agent=Mozilla%2F5.0+%28Linux%3B+Android+5.1%3B+HTCD
200LVW+Build%2FLMY47O%3B+wv%29+AppleWebKit%2F537.36+%28KHTML%2C+like+Gecko%
29+Version%2F4.0+Chrome%2F51.0.2704.81+Mobile+Safari%2F537.36`

### Response example

```json
{
  "status": "success",
  "user": {"key": ":id"},
  "settings": {"close_timer": 1, "viewability": 2, "redirect": "direct", "reward_label": "Coins", "reward_amount": 10},
  "ads": [
    {
      "title": "Ad title",
      "description": "Ad description",
      "rating": "3.44",
      "ratings_count": "9872",
      "click_url": "http://click.com",
      "cta":"Install Now!",
      "type": "native|html|video",
      "vast": "VAST",
      "markup": "HTML content",
      "creatives": {
        "icon": {
          "url": "http://cdn.com/icon",
          "width": 60,
          "height": 60
        },
        "image": {
          "url": "http://cdn.com/image",
          "width": 1200,
          "height": 627
        },
        "vast": "VAST XML",
      },
      "beacons": ["http://pixel.com"]
    }
  ]
}
```

#### JSON Response key parameters

* `status` – Always `OK` if the request was processed successfully 
* `ads` – [Ad objects collection](#ad)
* `user` – [User object](#user)
* `settings` – [Placement settings object](#settings)

#### User

* `user.key` – Unique user `GUID`, which is generated on each request or sent from the `user_key` GET variable.
When an ad is being requested, the user identifier, which is stored in app, is sent to `user_key`. For the first request nothing is sent, as the identifier does not exist yet. The Ad server generates a new `GUID` and sends it in the response, 
the SDK saves the identifier in the app. The next requests can use this identifier. 

#### Settings

* `settings.viewability` – duration (in seconds) of displaying the ad on the screen of the tracking pixels device. 

* `settings.close_timer` – time (in seconds) during which the closing buttons are not displayed for `Interstitial` ad type. The countdown timer is shown instead.

* 'setting.redirect' – is used in Android version to specify the way of moving to URL when the ad is clicked, either a native application of the system or a web-browser.

* `settings.s2s` - is used in rewarded video to specify S2S

* `settings.reward_amount` - is used in rewarded video to specify reward label for completed view (Coins, Gold etc)

* `settings.reward_amount` - is used in rewarded video to specify reward amount for completed view

#### Ad

* `ad.type` – Response type for an ad. This setting defines the Ad object structure. The available parameter values are the following: `native`, `html`, `video`. Value depends on your placement's type:

`native`

* `ad.title` – Ad header.
* `ad.description` – Ad description.
* `ad.cta` – Text on the CTA (Call to Action) button.
* `ad.rating` – Advertised app rating (if an app is promoted).
* `ad.ratings_count` – Number of application evluations (if an app is promoted).
* `ad.click_url` – Tracking link for redirection on clicking the ad (each redirection is added to statistics).
* `ad.beacons` – Array of the tracking links for recording the display. Each link provides link with a `gif` of `0х0` size. Every link should be requested when displaying (each redirection is added to statistics).
* `ad.creatives.icon` – Link to the icon (if requested).
* `ad.creatives.main` – Link to the banner picture (if requested). 
* `ad.creatives.vast` – `xml` in [VAST](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast-3-0/) format (if requested). 

`html`

* `ad.markup` – HTML string, which should be displayed. The tracking pixel will be attached as `img` tags inside markup.

`video`

* `ad.vast` – `xml` string in [VAST](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast-3-0/) format.
