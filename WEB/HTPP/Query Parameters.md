These are parameters appended to the URL.
It can use special command to add action on the query.
``` 
GET /api/products/search?q=coffee+beans&sort=price-low
```

The "**?**" delimit the Query Parameter

in this case q=coffee+beans is the value.
The browser it telling to search for "coffee beans"  because the "**+**" sign is used to represent space in URL.

The "**&**" separates this from the previous parameter.
Sort is the command and "**price-low**" is the value. That tells the server to sort the search result by price from lowest to highest.
