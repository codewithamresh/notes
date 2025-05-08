# Connection Pooling

max-pool-size - Max no. of connection allowed at once
min-idle  - idle me bhi eetne open rahenge
connection-timeout - wait time if no connection available
max-lifetime - connection ko kitni der baad recycle karna
idle timeout - Idle connection ko kitne der baad close karna

> Always use connection pooling

- database se connection banana heavy hota hai (time + CPU)
- Every request k liye new connection banaenge to server pe jada load padega. isliye hum ek connection pool banate hai
- jab Request aaye to pool se ek connection leke kaam kar lo phir wapis pool me daal do.

Real Life Example : har customer ke liye new waiter nahi hire kr sakte
isliye customer aaye waiter assign kar do aur kaam hone k baad wapis pool m chala jata.

Connection Pool - A pool(collection) of pre-created, reusable database connections.

> Kaam khatam hone k baad connection close nahi hota wapis pool me chala jaata h reuse k liye


```go

package db
import(
    "database/sql",
    "log",
    _"github.com/lib/pq"
    "time"
)

var DB *sql.DB

func InitDB(url string){
    var err error
    DB, err = sql.Open("postgres",url)
    if err != nil {
        log.Fatal("DB connection error:",err)
    }

DB.SetMaxOpenConns(30)
DB.SetMaxOpenConns(10)
DB.SetConnMaxIdleTime(5 * time.Minute)
DB.SetConnMaxLifeTime(30 * time.Minute)

if err = DB.Ping(); err != nil {
    log.Fatal("Ping error: ", err)
  }
}

func main(){
    db.InitDB(os.Getenv("DATABASE_URL"))
}

```

### In Spring Boot

```yml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/mydb
    username: myuser
    password: mypass
    driver-class-name: org.postgresql.Driver
    hikari:
      minimum-idle: 5
      maximum-pool-size: 20
      idle-timeout: 30000         # 30 seconds
      max-lifetime: 1800000       # 30 minutes
      connection-timeout: 30000   # 30 seconds
      pool-name: MyHikariPool
      auto-commit: true


```
