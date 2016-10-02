Go 1.7 is required. You can install Go with `homebrew`:

```
brew install go
```

To compile source code run the following command:

```
make setup
make dev
```

This will produce `pgweb` binary in the current directory.

There's also a task to compile binaries for other operating systems:

```
make release
```

Under the hood it uses [gox](https://github.com/mitchellh/gox). Compiled binaries
will be stored into `./bin` directory.