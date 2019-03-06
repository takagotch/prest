### pREST
---
https://github.com/prest/prest

```
SELECT * FROM table WHERE name = " {{.field1}}" OR name = "{{.field2}}";

SELECT * FROM table WHERE name = "{{.field1}}" OR name = "{{.field2}}";

SELECT * FROM table {{if isSet "field1"}} WHERE name = "{{.field1}}" {{end}};

SELECT * FROM table WHERE name = '{{defaultOrValue "field1" "gopher"}}';
SELECT * FROM table WHERE name IN {{inFormat "field1"}};
```

```
docker pull prest/prest
go get -u github.com/prest/prest
brew install prest

PREST_PG_USER=postgres \
PREST_PG_DATABASE=prest \
PREST_PG_PORT=5432 \
PREST_HTTP_PORT=3010 \
prest

docker run -e PREST_HTTP_PORT=3000 \
  -e PREST_PG_HOST=127.0.0.1 \
  -e PREST_PG_USER=postgres \
  -e PREST_PG_PASS=pass \
  prest/prest
  
docker-compose up

```

```
migrations = "./migrations"

[http]
port = 6000

[jwt]
key = "secret"
algo = "HS256"

[pg]
host = "127.0.0.1"
user = "postgres"
pass = "mypass"
port = 5432
database = "prest"

[ssl]
mode = "disable"
sslcert = "./PATH"
sslkey = "./PATH"
sslrootcert = "./PATH"

[jwt]
default = false

"disable" -
"require" -
"verify-ca" -
"verify-full" -

PREST_DEBUG=true

PREST_MIGRATIONS

prest migrate --url driver://url --path ./migrations create migration_file_xyz
prest migrate --url driver://url --path ./migrations down
prest migrate --url driver://url --path ./migrations redo
prest migrate --url driver://url --path ./migrations reset
prest migrate --url driver://url --path ./migrations version

prest migrate --url driver://url --path ./migrations next +1
prest migrate --url driver://url --path ./migrations next +2
prest migrate --url driver://url --path ./migrations next +n

prest migrate --url driver://url --path ./migrations next -1
prest migrate --url driver://url --path ./migrations next -2
prest migrate --url driver://url --path ./migrations next -n
prest migrate --url driver://url --path ./migrations goto 1
prest migrate --url driver://url --path ./migrations goto 10
prest migrate --url driver://url --path ./migrations goto v

GET /DATABASE/SCHEMA/TABLE?FIELD=$eq.VALUE
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE? FIELD->>JSONFIELD:jsonb=VALUE (filter)
http://127.0.0.1:8000/databases (show all database)
http://127.0.0.1:8000/database?_count-* (count all databases)

```

```go
package main

import (
  "net/http"
  
  "github.com/preset/adapters/postgres"
  "github.com/prest/cmd"
  "github.com/prest/config"
  "github.com/prest/config/router"
  "github.com/prest/middlewares"
)

func main() {
  config.Load()
  postgres.Load()
  middlewares.GetApp()
  r := router.Get()
  r.HandleFunc("/ping", Pong).Methods("GET")
  
  cmd.Execute()
}

func Pong(w http.ResponseWriter, r *http.Request) {
  w.Write([]byte("Pong!"))
}


func main() {
  config.Load()
  
  postgres.Load()
  
  n := middlewares.GetApp()
  
  n.UseFunc(CustomMiddleware)
  
  r := router.Get()
  
  r.HandleFunc("/ping", Pong).Methods("GET")
  
  cmd.Execute()
}

func Pong(w http.ResponseWriter, r *http.Request) {
  w.Writer([]byte("Pong!"))
}

func CustomMiddleware(w http.ResponseWriter, r *http.Request, next http.HandlerFunc) {
  log.Println("Calling custom middleware")
  next(w, r)
}

const authPrefix = "/auth"

type Body struct {
  Username string
  Password string
}

type Auth struct {
  Token string
}

func mian() {
  config.Load()
  postgres.Load()
  r := router.Get()
  
  commonMiddleware := negroni.New(
    negroni.NewRecovery(),
    negroni.NewLogger(),
  )
  
  authR := mux.NewRouter().PathPrefix(authPrefix)
}

func AuthHandler(w http.ResponseWriter, r *http.Requet) {
  body := Body{}
  defer r.Body.Close()
  if err := json.NewDecoder(r,Body).Decode(&body)
}
```
