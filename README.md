# sphp
Switching php version for M1/Itel MACs

# Usage: 
$ sphp **phpversion**, e.g.:
```
sphp 7.4
```
# Before switching 
## Install XCode components (required)
```
xcode-select --install
```

## Install HomeBrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

## Change standard Apache to Homebrew one
```
sudo apachectl stop
sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist 2>/dev/null
````
and install HomeBrew Apache version
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
and install all php versions:
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

ini files are located at:
### Fof intel Macs:
```
/usr/local/etc/php/5.6/php.ini
/usr/local/etc/php/7.0/php.ini
/usr/local/etc/php/7.1/php.ini
/usr/local/etc/php/7.2/php.ini
/usr/local/etc/php/7.3/php.ini
/usr/local/etc/php/7.4/php.ini
/usr/local/etc/php/8.0/php.ini
```
### For Silicon M1 Macs:
```
/opt/Homebrew/etc/php/5.6/php.ini
/opt/Homebrew/etc/php/7.0/php.ini
/opt/Homebrew/etc/php/7.1/php.ini
//opt/Homebrew/etc/php/7.2/php.ini
/opt/Homebrew/etc/php/7.3/php.ini
/opt/Homebrew/etc/php/7.4/php.ini
/opt/Homebrew/etc/php/8.0/php.ini
```
# Apache PHP Setup
You need add modules to httpd.conf after LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so

## For Intel Macs 
(php7.4 as a standard)
```
#LoadModule php5_module /usr/local/opt/php@5.6/lib/httpd/modules/libphp5.so
#LoadModule php7_module /usr/local/opt/php@7.0/lib/httpd/modules/libphp7.so
#LoadModule php7_module /usr/local/opt/php@7.1/lib/httpd/modules/libphp7.so
#LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so
#LoadModule php7_module /usr/local/opt/php@7.3/lib/httpd/modules/libphp7.so
LoadModule php7_module /usr/local/opt/php@7.4/lib/httpd/modules/libphp7.so
#LoadModule php_module /usr/local/opt/php@8.0/lib/httpd/modules/libphp.so
```

## For Silicon M1 Macs
```
#LoadModule php5_module /opt/homebrew/opt/php@5.6/lib/httpd/modules/libphp5.so
#LoadModule php7_module /opt/homebrew/opt/php@7.0/lib/httpd/modules/libphp7.so
#LoadModule php7_module /opt/homebrew/opt/php@7.1/lib/httpd/modules/libphp7.so
#LoadModule php7_module /opt/homebrew/opt/php@7.2/lib/httpd/modules/libphp7.so
#LoadModule php7_module /opt/homebrew/opt/php@7.3/lib/httpd/modules/libphp7.so
LoadModule php7_module /opt/homebrew/opt/php@7.4/lib/httpd/modules/libphp7.so
#LoadModule php_module /opt/homebrew/opt/php/lib/httpd/modules/libphp.so
```

Search for the block
```
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
```
and replace it with 
```
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>

<FilesMatch \.php$>
    SetHandler application/x-httpd-php
</FilesMatch>
```

# Downloading and activating the script
## For Silicon M1 Macs
```
curl -L https://raw.githubusercontent.com/vadimbk/sphp/main/sphp > /opt/homebrew/bin/sphp
chmod +x /opt/homebrew/bin/sphp
```
## For Intel Macs
```
curl -L https://raw.githubusercontent.com/vadimbk/sphp/main/sphp >  /usr/local/bin/sphp
chmod +x /usr/local/bin/sphp
```

# Testing
Add info.php to Apache root directory
## For Silicon M1 Macs
```
printf "<?php\nphpinfo();\n?>" > /opt/homebrew/var/www/info.php
```
## For Intes Macs
```
printf "<?php\nphpinfo();\n?>" > /usr/loca/var/www/info.php
```

And run the test:
```
http://localhost:8080/info.php 
```
You should see an phpinfo() page

N'joy :)
