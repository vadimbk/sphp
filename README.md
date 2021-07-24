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
Other control options (start/stop):
```
brew services stop httpd
brew services start httpd
```

## php install replacement
You  need to install php-fpm version to replace too slow standard php 7.3 installatio wnich called by Apple "deprecated"
At first, add repository
```
brew tap shivammathur/php
```
Firther, add php for various versions:
```
brew install shivammathur/php/php@5.6
brew install shivammathur/php/php@7.0
brew install shivammathur/php/php@7.1
brew install shivammathur/php/php@7.2
brew install shivammathur/php/php@7.3
brew install shivammathur/php/php@7.4
brew install shivammathur/php/php@8.0
```
You need to know that 5.6-7.2 versions are deprecated and may cause some errors, but they are need to lauch old sites.


Also need add modules to httpd.conf   

## For Intel Macs 
* 
