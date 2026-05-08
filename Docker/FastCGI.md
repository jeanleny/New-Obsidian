*Fast Common Gateway Interface (Interface de passerelle commune)*
Its the evolution of the CGI, its an interface used by the servers HTTP and it has been normalised by the RFC 3875 protocol.

Instead of sending the whole file content (like html, png...), the http server execute a program and return the generated content.
The CGI is the industrial standard that indicate how to send the http server request to the program and how to get the generated response.

Typical use :
A web user submits a web form on a web page that uses CGI.
This form's data is sent to the web server within an HTTP request with an URL containing the CGI script.
The web server launches the CGI script in a new computer process. The CGI script passes its result in the HTML form then the web Server that relays it back to the browser.
