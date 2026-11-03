In an HTML file with HTMX, here's what happen step by step

```html
<button
    hx-get="/login"
    hx-target="#result"
    hx-include="#q"
    hx-swap="innerHTML">
    laugine
</button>

<p id="result"></p>
```

The attribute : 
- `hx-get="/login"` : sends an HTTP GET request to `/login`
- `hx-target="#result"` : Tells HTMX where to put the response
- `hx-swap="innerHTML"` : insert the response inside the target element

1. We click the button that request the go app
2. The go handler executes a go response like so :
   ```go
   fmt.Fprintf(w, "Login failed")
   ```
   This writes Login Failed into the HTTP response body.
3. HTMX receives the response
   It sends back the `Login Failed` plain text
4. HTMX looks at the `hx-target` which is `#result`. And replace dynamically the result in the html
   so 
   ```html
   <p id="result"></p>
   ```
   becomes
   ```html
<p id="result">Login failed</p>
   ```
And this happens because we've set
`hx-swap="innerHTML"`
So it becomes dynamically updated without reloading the page