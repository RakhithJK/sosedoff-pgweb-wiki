# Usage

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

### SSH Gateway

If your postgres server is running behind firewall, you can connect to it using
ssh gateways. First, you'll need to run a ssh command:

```
ssh -Ng -L 5433:localhost:5432 user@remotehost.com
```

Then you can start pgweb with the following command:

```
pgweb --url postgres://user:password@localhost:5433/database
``` 

### CLI options

```
Usage:
  pgweb [OPTIONS]

Application Options:
  -v, --version    Print version
  -d, --debug      Enable debugging mode (false)
  -s, --skip-open  Skip browser open on start
      --url=       Database connection string
      --host=      Server hostname or IP (localhost)
      --port=      Server port (5432)
      --user=      Database user (postgres)
      --pass=      Password for user
      --db=        Database name (postgres)
      --ssl=       SSL option (disable)
      --bind=      HTTP server host (localhost)
      --listen=    HTTP server listen port (8080)
      --auth-user= HTTP basic auth user
      --auth-pass= HTTP basic auth password
```
