In order to handle cmd, IRC clients will need a specific format .
For IRC 2812 the format look like so

```
[2.3.1](https://www.rfc-editor.org/rfc/rfc2812#section-2.3.1) Message format in Augmented BNF

   The protocol messages must be extracted from the contiguous stream of
   octets.  The current solution is to designate two characters, CR and
   LF, as message separators.  Empty messages are silently ignored,
   which permits use of the sequence CR-LF between messages without
   extra problems.

   The extracted message is parsed into the components <prefix>,
   <command> and list of parameters (<params>).

    The Augmented BNF representation for this is:

    message    =  [ ":" prefix SPACE ] command [ params ] crlf
    prefix     =  servername / ( nickname [ [ "!" user ] "@" host ] )
    command    =  1*letter / 3digit
    params     =  *14( SPACE middle ) [ SPACE ":" trailing ]
               =/ 14( SPACE middle ) [ SPACE [ ":" ] trailing ]

    nospcrlfcl =  %x01-09 / %x0B-0C / %x0E-1F / %x21-39 / %x3B-FF
                    ; any octet except NUL, CR, LF, " " and ":"
    middle     =  nospcrlfcl *( ":" / nospcrlfcl )
    trailing   =  *( ":" / " " / nospcrlfcl )

    SPACE      =  %x20        ; space character
    crlf       =  %x0D %x0A   ; "carriage return" "linefeed"
```
see [IRC_2812](https://www.rfc-editor.org/rfc/rfc2812#section-2.3.1)

- The prefix will be the name of the \r\ emitter(ircserver/nickname)
- command can contain, depends on the message : 
	- the literal cmd/msg
	- a 3 digit code that refer to the cmd see [cmd_response](https://www.rfc-editor.org/rfc/rfc2812#section-5) this is code is usually given by the command section you want to use.
	  Example : Join message will use (RPL_TOPIC). see [join_message](https://www.rfc-editor.org/rfc/rfc2812#section-2.3.1)
