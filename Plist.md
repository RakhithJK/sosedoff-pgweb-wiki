Example homebrew plist:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>KeepAlive</key>
  <true/>
  <key>Label</key>
  <string>homebrew.mxcl.pgweb</string>
  <key>ProgramArguments</key>
  <array>
    <string>/usr/local/Caskroom/pgweb/0.9.9/pgweb_darwin_amd64</string>
  </array>
  <key>RunAtLoad</key>
  <true/>
  <key>StandardErrorPath</key>
  <string>/usr/local/var/log/pgweb.error.log</string>
  <key>StandardOutPath</key>
  <string>/usr/local/var/log/pgweb.log</string>
</dict>
</plist>
```

Make sure to replace path to the pgweb binary if you installed it manually.