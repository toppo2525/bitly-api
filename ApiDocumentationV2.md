See also the ApiDocumentation and JavascriptClientApiDocumentation

# Deprecation Notice #

**As of 2010-Mar-30 this v2 API has been deprecated in favor of V3 endpoints (see ApiDocumentation). This document will be updated with the phaseout schedule when that is available.  For the time being, existing API endpoints will remain active, but we encourage you to upgrade your client libraries and API calls to the newest version at your earliest convenience.  Additionally, upcoming endpoints that provide increased functionality will only be rolled out via the V3 interface.**

The document is in regards to API version **2.0.1**

**Sections**



---


## Authentication and Shared Parameters ##

All APIs require authentication credentials supplied as query arguments You can find your apiKey at http://bit.ly/account/your_api_key :

**NOTE:** do not use the login `bitlyapidemo`. That login is for example purposes only.

> login=**login**&apiKey=**apiKey**

All APIs require a version identifier to be present:

> version=**2.0.1**

All APIs support an optional return format specifier (**json** is the default response format. **xml** is also available):

> format=**json**

All APIs support an optional callback specifier for use with json return format:

> callback=**callback**

<a href='Hidden comment: 
Removed this since it felt confusing and redundant here.
APIs which take both shortUrl and hash as arguments must have one or the other present.
'></a>

---


## Rate Limiting ##

bit.ly currently limits API users to no more than five concurrent connections from a single IP address.  In general, if you intend to be an extremely high-volume user of the api, please contact us at support@bit.ly to discuss your options.


---


---


# REST API #

## /shorten ##
Given a long URL, /shorten encodes it as a shorter one and returns it.

**Additional Parameters**
  * **longUrl**
> > A long URL to shorten, eg: http://betaworks.com


> Note: Long URLs should be [URL-escaped](http://en.wikipedia.org/wiki/Percent-encoding).

**Examples**
  * `http://api.bit.ly/shorten?version=2.0.1&longUrl=http://cnn.com&login=bitlyapidemo&apiKey=R_0da49e0a9118ff35f52f629d2d71bf07`


---


## /expand ##
Given a bit.ly URL or hash, /expand decodes it back into a long source URL and returns it.

**Additional Parameters**

> Either **shortUrl** or **hash** must be given as a parameter.
    * **shortUrl**
> > > A bitly URL, eg: http://bit.ly/1RmnUT
    * **hash**
> > > A bit.ly hash, eg: 2bYgqR

**Examples**
  * `http://api.bit.ly/expand?version=2.0.1&shortUrl=http://bit.ly/31IqMl&login=bitlyapidemo&apiKey=R_0da49e0a9118ff35f52f629d2d71bf07`

---


## /info ##
Given a bit.ly URL or hash, return information about that page, such as the long source URL, associated usernames, and other information.

**Additional Parameters**


> Either **shortUrl** or **hash** must be given as a parameter.
    * **shortUrl**
> > > A single bitly URL, eg: http://bit.ly/1RmnUT
    * **hash**
> > > A bit.ly hash, eg: 2bYgqR
    * **keys**
> > > One or more keys to limit the attributes returned about each bitly document, eg: htmlTitle,thumbnail

**Examples**
  * `http://api.bit.ly/info?version=2.0.1&hash=3j4ir4&login=bitlyapidemo&apiKey=R_0da49e0a9118ff35f52f629d2d71bf07`

---


## /stats ##
Given a bit.ly URL or hash, return traffic and referrer data.

**Additional Parameters**


> Either **shortUrl** or **hash** must be given as a parameter.
    * **shortUrl**
> > > A single bitly URL, eg: http://bit.ly/1RmnUT
    * **hash**
> > > A single hash, eg: 1RmnUT

**Examples**
  * `http://api.bit.ly/stats?version=2.0.1&shortUrl=http://bit.ly/31IqMl&login=bitlyapidemo&apiKey=R_0da49e0a9118ff35f52f629d2d71bf07`


---


## /errors ##
Get a list of bit.ly API error codes.

**Examples**
  * `http://api.bit.ly/errors?version=2.0.1&login=bitlyapidemo&apiKey=R_0da49e0a9118ff35f52f629d2d71bf07`


---


---


# Discussion #

Please visit our Google Group for discussion of projects and technical issues.


> http://groups.google.com/group/bitly-api