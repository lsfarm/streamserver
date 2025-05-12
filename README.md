# streamserver
https://ipv6.rs/tutorial/macOS/Icecast_2/
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
