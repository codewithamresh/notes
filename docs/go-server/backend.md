# Backend

## Load Env Variables in Java


```java

@Value("${DB_PASSWORD}")

```

```java

@Autowired
private Environment env;
String DB_URL = env.getProperty("DB_URL","default value");

```

## Load Env Variables in Go

`DB_URL := os.Getenv("DB_URL","default value")`

`DB_URL= mysql://localhost:3306/myDB`

```go
func init(){
    _ = godotenv.Load()
}
```

`data, _ := os.ReadFile("/etc/secrets/secret_key")`



## Go Server setup and Json Response

```go
package main

import (
	"encoding/json"
	"net/http"
)

type MessageResponse struct {
	Message string `json:"message"`
}


func main(){
	http.HandleFunc("/",func(w http.ResponseWriter, r *http.Request) {
		w.Header().Set("Content-Type","application/json")
		response  := MessageResponse{Message: "Hello World"}
		json.NewEncoder(w).Encode(response)
		http.ListenAndServe(":8080",nil)

	})
}

```

```go
func main(){
mux := http.NewServeMux()
}
```

- Router : Object that routes requests

- Handler : Object that handles requests

- In Go : ek router bhi handler hota hai because it satisfies the http.Handler interface.


### Chi Router

```go
router := chi.NewRouter()
http.ListenAndServe(":8080", router)
```

```go

r := gin.Default()
http.ListenAndServe(":8080",r)

```