When using `pgweb` you might find that there's no way to quickly
establish connection to a server even if you've connected to it 
many times before. Thats's correct, pgweb does not keep track of 
those connections. So bookmarks feature comes into play.
It basically allows you to keep connection settings to your most
frequent servers as a bookmarks with credentials stored in a file
on your local filesystem, encoded as TOML. Bookmark files are stored
in `~/.pgweb/bookmarks` directory.

Here's an example of a bookmark file (`~/.pgweb/bookmarks/local-server.toml`):

```TOML
host = "localhost"
port = 5432
user = "postgres"
database = "mydatabase"
sslmode = "disable"
```

Here's an example of a bookmark file with SSH options (`~/.pgweb/bookmarks/ssh-tunnel-to-db.toml`). Use this to create an SSH connection through a "Jump server" using an SSH credential file, to another database (such as AWS RDS):

```TOML
host = "rds-db-name.cluster-asdf.us-east-1.rds.amazonaws.com"
port = 5432
user = "rds-username"
password = "rds-password"
database = "rds-database-name"

[SSH]
host = "ec2-111-111-111-111.compute-1.amazonaws.com"
user = "ec2-user"
key = "/path/to/key-file"
key_password = "key-file-password"
``` 

To keep your config short, you can also just define a url:

```TOML
url = "postgres://user:password@host:port/database?sslmode=mode"
```

Keeping server bookmarks as files is very handy, you can sync those
as git repository or in Dropbox. TOML format is also very simple and
similar to INI format. Other formats, such as YAML or JSON, could also
be supported in future.