The Data Source Name is the structure used to describe how to connect to Data Base.
It has many attributes but must of the time are :
- The name of the data source
- the location of the data source
- the name of a database driver which can access the data source
- a user ID for data acess (if required)
- a user password for data acess (if required)

There's several format but we usually kept 2 :

#### URL format 
` postgres://username:password@localhost:5432/mydatabase?sslmode=disable`

#### Key-value format
`host=localhost port=5432 user=postgres password=secret dbname=myapp sslmode=disable`
