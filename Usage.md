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
  -v, --version             Print version
  -d, --debug               Enable debugging mode
      --log-level=          Logging level (default: info)
      --log-format=         Logging output format (default: text)
      --log-forwarded-user  Log user information available in X-Forwarded-User/Email headers
      --url=                Database connection string
      --host=               Server hostname or IP (default: localhost)
      --port=               Server port (default: 5432)
      --user=               Database user
      --pass=               Password for user
      --passfile=           Local passwords file location
      --db=                 Database name
      --ssl=                SSL mode
      --ssl-rootcert=       SSL certificate authority file
      --ssl-cert=           SSL client certificate file
      --ssl-key=            SSL client certificate key file
      --open-timeout=       Maximum wait for connection, in seconds (default: 30)
      --bind=               HTTP server host (default: localhost)
      --listen=             HTTP server listen port (default: 8081)
      --auth-user=          HTTP basic auth user
      --auth-pass=          HTTP basic auth password
  -s, --skip-open           Skip browser open on start
      --sessions            Enable multiple database sessions
      --prefix=             Add a url prefix
      --readonly            Run database connection in readonly mode
      --lock-session        Lock session to a single database connection
  -b, --bookmark=           Bookmark to use for connection. Bookmark files are stored under $HOME/.pgweb/bookmarks/*.toml
      --bookmarks-dir=      Overrides default directory for bookmark files to search
      --no-pretty-json      Disable JSON formatting feature for result export
      --no-ssh              Disable database connections via SSH
      --connect-backend=    Enable database authentication through a third party backend
      --connect-token=      Authentication token for the third-party connect backend
      --connect-headers=    List of headers to pass to the connect backend
      --no-idle-timeout     Disable connection idle timeout
      --idle-timeout=       Set connection idle timeout in minutes (default: 180)
      --query-timeout=      Set global query execution timeout in seconds (default: 300)
      --cors                Enable Cross-Origin Resource Sharing (CORS)
      --cors-origin=        Allowed CORS origins (default: *)
      --binary-codec=       Codec for binary data serialization, one of 'none', 'hex', 'base58', 'base64' (default: none)
      --metrics             Enable Prometheus metrics endpoint
      --metrics-path=       Path prefix for Prometheus metrics endpoint (default: /metrics)
      --metrics-addr=       Listen host and port for Prometheus metrics server

Help Options:
  -h, --help                Show this help message

Available environment variables:
  PGWEB_DATABASE_URL  Database connection string
  PGWEB_URL_PREFIX    HTTP server path prefix
  PGWEB_SESSIONS:     Enable multiple database sessions
  PGWEB_LOCK_SESSION  Lock session to a single database connection
  PGWEB_AUTH_USER     HTTP basic auth username
  PGWEB_AUTH_PASS     HTTP basic auth password
```