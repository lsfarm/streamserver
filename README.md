# streamserver
https://ipv6.rs/tutorial/macOS/Icecast_2/
```
icecast -c /usr/local/etc/icecast.xml
```
https://www.apachefriends.org/download.html
/Applications/XAMPP/xamppfiles/htdocs/dashboard
```
/Applications/XAMPP/xamppfiles/xampp startapache
```
## ApacheWebserver Autolaunch
```
sudo nano /Library/LaunchDaemons/com.apache.xampp.startapache.plist
```
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
 "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>com.apache.xampp.startapache</string>

    <key>ProgramArguments</key>
    <array>
      <string>/Applications/XAMPP/xamppfiles/xampp</string>
      <string>startapache</string>
    </array>

    <key>RunAtLoad</key>
    <true/>

    <key>StandardOutPath</key>
    <string>/tmp/xampp-apache-start.log</string>
    <key>StandardErrorPath</key>
    <string>/tmp/xampp-apache-start.err</string>
  </dict>
</plist>
```
```
sudo chown root:wheel /Library/LaunchDaemons/com.apache.xampp.startapache.plist
```
```
sudo chmod 644 /Library/LaunchDaemons/com.apache.xampp.startapache.plist
```
```
sudo launchctl load /Library/LaunchDaemons/com.apache.xampp.startapache.plist
```
## Broadcast Autolaunch
```
sudo nano /usr/local/bin/start-broadcast.sh
```
```
#!/bin/bash

# Start Icecast
/usr/local/bin/icecast -c /usr/local/etc/icecast.xml &

# Give Icecast a few seconds to initialize
sleep 5

# Start butt
/usr/local/bin/butt -c tsconfig -s
```
Adjust paths if needed using which icecast and which butt.
```
sudo chmod +x /usr/local/bin/start-broadcast.sh
```
```
sudo nano /Library/LaunchDaemons/com.example.buttstarter.plist
```
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.buttstarter</string>

    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/start-broadcast.sh</string>
    </array>

    <key>RunAtLoad</key>
    <true/>

    <key>NetworkState</key>
    <true/>

    <key>StandardOutPath</key>
    <string>/var/log/broadcast.log</string>
    <key>StandardErrorPath</key>
    <string>/var/log/broadcast.err</string>
</dict>
</plist>
```
```
sudo chown root:wheel /Library/LaunchDaemons/com.example.buttstarter.plist
```
```
sudo chmod 644 /Library/LaunchDaemons/com.example.buttstarter.plist
```
```
sudo launchctl load /Library/LaunchDaemons/com.example.buttstarter.plist
```
### run script:
```
sudo /usr/local/bin/start-broadcast.sh

```
### debugging:
```
sudo cat /var/log/broadcast.log
sudo cat /var/log/broadcast.err
```
```
ps aux | grep icecast
ps aux | grep butt
cat /var/log/broadcast.log
```
