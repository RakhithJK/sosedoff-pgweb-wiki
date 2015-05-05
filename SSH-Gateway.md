If your PostgreSQL server is running behind firewall you can establish
connection via SSH gateway. Your operating system should have `ssh`
binary available.

Start gateway with command:

```
ssh -Ng -L 5000:localhost:5432 user@mysite.com
```

From SSH man page:

- `-N` - Do not execute a remote command. This is useful for just forwarding ports
- `-g` - Allows remote hosts to connect to local forwarded ports.
- `-L` - Specifies that the given port on the local (client) host is to be forwarded to the given host and port on the remote side. Format: `[bind_address:]port:host:hostport`

Once ssh connection and port forwarding is established, you can start pgweb:

```
pgweb --url postgres://user:password@localhost:5000/database
``` 