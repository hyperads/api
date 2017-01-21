#Ad Serving API 

### HTTP endpoint

`GET http://ad.dispply.com/v2/ads/:placement_id`

### (GET) request parameters 

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
ip | false | Requester's ip | Device IP
user_agent | false | Requester's user-agent | Device user-agent
platform | false | No | Device platform (ios/android)
device_type | false | phone | Device type (phone/tablet) if the user-agent absent
type | false | native | Type of advertisement: native/interstitial/html/banner/video/native_video/rewarded_video. Multiple values separated by "\|"
format | false | No | Creative's format (ex. 120x80)
content | false | title,icon,main | Required native content separated by comma: title,desc,icon,main
callback | false | No | Callback function for [JSONP](https://en.wikipedia.org/wiki/JSONP) request
ios_idfa | false| No | iOS advertising ID
gaid | false | No | Android advertising ID
limit | false | 1 | Count of advertisements
user_key | false | No | User's ID for frequency capping and profile (replacement for Google's GAID and iOS IFA when disabled ad tracking in iOS 10)

### Response parameters

```json
{
  "status": "success",
  "user": {"key": ":id"},
  "settings": {"close_timer": 1, "viewability": 2, "redirect":"direct"},
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

#### Ad

* `ad.type` – Response type for an ad. This setting defines the Ad object structure. The available parameter values are the following: `native`, `html`, `video`.

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
* `ad.creatives.vast` – `xml` in format [VAST](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast-3-0/) (if requested). 

`html`

* `ad.markup` – HTML string, which should be displayed. The tracking pixel shoud be attached as `img` tags.

`video`

* `ad.vast` – `xml` string in format [VAST](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast-3-0/).
