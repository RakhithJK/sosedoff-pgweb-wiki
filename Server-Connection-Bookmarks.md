When using `pgweb` you might find that there's no way to quickly
establish connection to a server even if you've connected to it 
many times before. Thats's correct, pgweb does ton keep track of 
those connections. So bookmarks feature comes into play.
It basically allows you to keep connection settings to your most
frequent servers as a bookmarks with credentials stored in a file
on your local filesystem, encoded as TOML. Bookmark files are stored
in `~/.pgweb/bookmarks` directory.

Here's an example of a bookmark file (`~/.pgweb/bookmarks/server.toml`):

```TOML
host = "localhost"
port = "5432"
user = "postgres"
database = "mydatabase"
ssl_mode = "disable"
``` 

To keep things short, you can just define an url:

```TOML
url = "postgres://user:password@host:port/database?sslmode=mode"
```

Keeping server bookmarks as files is very handy, you can sync those
as git repository or in Dropbox. TOML format is also very simple and
similar to INI format. Other formats, such as YAML or JSON, could also
be supported in future.