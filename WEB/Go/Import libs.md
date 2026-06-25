in the terminal run `go get github/repo` in the current repo to download the dependencies

then `go mod tidy` to finish the job.

Then you can import it in you're go file :
```go
package main

import (
	"fmt"
	tea "charm.land/bubbletea/v2"
)

func main (){
	tea.BackgroundColorMsg(stuff);
}
```