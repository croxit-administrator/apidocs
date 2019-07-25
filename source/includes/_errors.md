# Errors

<aside class="warning">
This error section is information about your failed request to our <code>croxit</code> server.
</aside>

The Kittn API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The croxit requested is hidden for specific user only.
404 | Not Found -- The specified croxit could not be found.
405 | Method Not Allowed -- You tried to access a croxit with an invalid method.
406 | Not Acceptable -- You requested a format that cannot accept by croxit.
410 | Gone -- The croxit requested has been removed from our servers.
418 | I'm a teapot.
429 | Too Many Requests -- You're requesting too many to croxit! slowdown!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
