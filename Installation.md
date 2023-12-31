### Supported Platforms

- OSX 64 bit
- Linux 32/64 bit
- Windows 32/64 bit
- ARM 64 bit

### Github Releases

Pgweb binaries and source code for each version is distributed via [Github Releases][1]

### Docker

Download an [official][3] Pgweb image:

```
docker pull sosedoff/pgweb
```

Or use Github Container Registry:

```
docker pull ghcr.io/sosedoff/pgweb:latest
```

### Mac

Install latest Pgweb version with [Homebrew][2]:

```
brew update
brew install pgweb
```

### Linux

Download and install Pgweb manually:

```
curl -s https://api.github.com/repos/sosedoff/pgweb/releases/latest \
  | grep linux_amd64.zip \
  | grep download \
  | cut -d '"' -f 4 \
  | wget -qi - \
  && unzip pgweb_linux_amd64.zip \
  && rm pgweb_linux_amd64.zip \
  && mv pgweb_linux_amd64 /usr/local/bin/pgweb
```

[1]: https://github.com/sosedoff/pgweb/releases
[2]: http://brew.sh 
[3]: https://hub.docker.com/r/sosedoff/pgweb/tags