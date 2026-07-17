The body contains data sent to the server, usually with method request (GET, POST ...).
Its often JSON or raw text.
The format of the data in the body is specified in the Content-type [[Headers]] in the request.
The server needs it to correctly understand and process the data.

A classic JSON Content-type body :
```JSON
{  
	"name": "FrankyVincent",  
	"email" : "FrankyV@personeldemerde.com"  
}
```
