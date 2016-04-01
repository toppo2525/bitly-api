# bitly API Best Practices #
**Please follow these guidelines when using the bitly API**



## Using the Latest Version of the API ##
The current and most stable version of the bitly API is 3.0. For up-to-date information about the bitly API, please read the complete [API Documentation](ApiDocumentation.md) and join our Google Group at http://groups.google.com/group/bitly-api

## Rate Limiting ##
bitly currently institutes per-hour, per-minute, and per-IP rate limits for each API method, and limits API users to a maximum of five concurrent connections from a single IP address. Our default limits are more than sufficient for nearly all use cases. **Please read through this documentation in its entirety to avoid common causes of rate limiting issues.**

## Caching ##
Since **bitly links never change or expire**, we ask that you cache data locally wherever possible.

## Avoiding API Calls on Page Loads ##
Most rate limiting issues are caused by extraneous API calls. We ask that you avoid making calls to the bitly API on page loads, and instead make these calls based on explicit user actions (such as clicking a “share” button).

## Authenticating End-Users With OAuth 2 ##
If you are shortening URLs on behalf of end-users, we ask that you use our OAuth 2 implementation to authenticate end-users before shortening.  URLs shortened in this manner will be added to the specified end-user’s history, allowing the end-user to manage and track his/her shortened URLs. You can begin registering an OAuth application from within your bitly account settings.

## HTTP Response Status Codes ##
Please note that all valid responses in json and xml format will carry an HTTP Response Status Code of 200. This means that **invalid, malformed or rate-limited json and xml requests may still return an HTTP response status code of 200**. In json and xml responses, the status\_code and status\_txt values indicate whether a request is well formed and valid. For txt format calls, the HTTP Response Status Codes 403, 500 and 503 are used denote rate limiting, a problem with the request format, or an unknown error.

## Checking for Errors ##
An invalid or rate limited request to the bitly API will not return a short URL.  Please check all API responses for errors, and fallback to a long link.  Invalid or rate limited API calls made via Javascript will often return “`http://bit.ly/undefined`” -- if you are seeing such links, please check the status\_code and status\_txt values for errors.

## Batch Processing ##
The bitly API does not support shortening more than one long URL with a single API call. However, up to 15 URLs can be handled in one API call using the “/v3/lookup,” “/v3/expand” and “/v3/clicks” endpoints.

## High-Volume Shorten Requests ##
If you need to shorten a large number of URLs at once, we recommend that you leave ample time to spread these requests out over many hours. Our API rate limits reset hourly, and rate limited batch requests can be resumed at the top of the hour.

## URL Encoding ##
All long URLs sent to the bitly API must be URL encoded, even if these links already contain escaped characters.  For more information about URL encoding, see http://www.w3schools.com/tags/ref_urlencode.asp.

For example, the link `http://betaworks.com/page?parameter=value#anchor` should be fully escaped to `http%3A%2F%2Fbetaworks.com%2Fpage%3Fparameter%3Dvalue%23anchor`.  The link `http://betaworks.com/page%3Fparameter%3Dvalue%23anchor` should be fully escaped to `http%3A%2F%2Fbetaworks.com%2Fpage%253Fparameter%253Dvalue%2523anchor`.

A valid API call to shorten the link `http://betaworks.com/page?parameter=value#anchor` would be: `http://api.bitly.com/v3/shorten?login=bitlyapidemo&apiKey=R_0da49e0a9118ff35f52f629d2d71bf07&longUrl=http%3A%2F%2Fbetaworks.com%2Fpage%3Fparameter%3Dvalue%23anchor&format=json`

Most languages include a function for URL encoding, including urlib.quote() in Python, encodeURIComponent() in javascript, and urlencode() in PHP.