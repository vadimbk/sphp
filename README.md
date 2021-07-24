# sphp
Switching php version for M1/Itel MACs

# Usage: 
$ sphp **phpversion**, e.g.:
```
sphp 7.4
```
# Before switching 

## Install HomeBrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

## Change standard Apache to Homebrew one
```
sudo apachectl stop
sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist 2>/dev/null
````
and install 
```
brew install httpd
```
test installation: open http://localhost:8080 in browser
to restart Apache:
```
breq services restart apache
```
## Install php
You need add modules to httpd.conf   

## For Intel Macs 
* 
