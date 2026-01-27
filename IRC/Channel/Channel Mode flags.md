- **+t protected topic mode**
	this mode controls whether the channel privileges are required to set the topic.
- **+i Invite only mode**
	If the channel is in invite mode, the user must have received an invite for this channel.
	If not the user receive this message : 
		```<client> <channel> :Cannot join channel (+i)
- **+k key mode(password)**
	this mode letter sets a password that must be supplied in order to join this channel.
	The password have to be written after the channel param like so :```<channel>{,<channel>} [<key>{,<key>}]
	
- **+o operator privilege**
	give chan operator privileges to a user on the channel
	``MODE #Finnish +o Kilroy
	This will add the operator privilege to kilroy on the Finnish channel
- **+l protected topic mode**
	sets the limit for the number of users on the channel
	``MODE #eu-opers +l 10
	This will set the number of users on channel to 10
