Headers carry Metadata about the request.
They are sent invisibly alongside it.
It is the browser or the app that sets them automatically. 

This include data about the host, client's user agent, language preferences...

This is used by the server to identify the browser and OS version of the client.

```
Host: api.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Content-Type: application/json
Connection: keep-alive
