Example plist for OSX:

```plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>KeepAlive</key>
    <dict>
      <key>SuccessfulExit</key>
      <false/>
    </dict>
    <key>Label</key>
    <string>homebrew.mxcl.pgweb</string>
    <key>Program</key>
    <array>
      <string>/usr/local/bin/pgweb</string>
    </array>
    <key>ProgramArguments</key>
    <array>
      <string>/usr/local/bin/pgweb</string>
      <string>-s</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>WorkingDirectory</key>
    <string>/usr/local/var</string>
    <key>StandardErrorPath</key>
    <string>/usr/local/var/log/pgweb.log</string>
    <key>StandardOutPath</key>
    <string>/usr/local/var/log/pgweb.log</string>
  </dict>
</plist>
```

You can use tools like [lunchy](https://github.com/sosedoff/lunchy-go) to manage application
plists.