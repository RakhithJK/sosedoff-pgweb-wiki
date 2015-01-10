Ongoing pgweb development is currently done on OSX Yosemite operating system.
If you're using Linux, there's a big chance that everything will *just* work
with no additional steps required to build software.

Most of the tasks are managed through `Makefile`:

```
Task                 : Description
-----------------    : -------------------
make setup           : Install all necessary dependencies
make dev             : Generate development build
make test            : Run tests
make build           : Generate production build for current OS
make release         : Generate binaries for all supported OSes
make clean           : Remove all build files and reset assets
make assets          : Generate production assets file
make dev-assets      : Generate development assets file
make docker          : Build docker image
```

To see usage, just run `make` with no arguments.