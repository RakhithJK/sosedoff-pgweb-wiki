Start server:

```
pgweb
```

You can also provide connection flags:

```
pgweb --host localhost --user myuser --db mydb
```

Connection URL scheme is also supported:

```
pgweb --url postgres://user:password@host:port/database?sslmode=[mode]
```

It works great with [Heroku Postgres](https://postgres.heroku.com) if you need 
to troubleshoot production database or simply run a few queries.

### CLI options

```
Usage:
  pgweb [OPTIONS]

Application Options:
  -v, --version       Print version
  -d, --debug         Enable debugging mode (false)
      --url=          Database connection string
      --host=         Server hostname or IP
      --port=         Server port (5432)
      --user=         Database user
      --pass=         Password for user
      --db=           Database name
      --ssl=          SSL option
      --bind=         HTTP server host (localhost)
      --listen=       HTTP server listen port (8081)
      --auth-user=    HTTP basic auth user
      --auth-pass=    HTTP basic auth password
  -s, --skip-open     Skip browser open on start
      --sessions      Enable multiple database sessions (false)
      --prefix=       Add a url prefix
      --readonly      Run database connection in readonly mode
      --lock-session  Lock session to a single database connection (false)
  -b, --bookmark=     Bookmark to use for connection. Bookmark files are stored under $HOME/.pgweb/bookmarks/*.toml

Help Options:
  -h, --help          Show this help message
```
