A channel is just a named group of one or more client.
The channel is created implictly when the first client joins it, and the channel ceases to exist when the last client leaves.

A channel name is a string beggining with specifier prefix character :
- **'#'** for [[Regular channel]]
- **'&'** for local channel- **`#`** – the normal, global channel  
- **+** – modeless channel  
    Example: `#linux`, `#chat`
- **!** – timestamped / safe channel  
    Introduced to avoid channel takeovers during netsplits. Not universally supported anymore.
**Channel Names**
Channel names are strings beginning with '#', '&', '+', '!'
They are up to 50 characters long.
They SHALL NOT contains any space, ctrl + G, comma (' , ') .
Channel name are case insensitive.
