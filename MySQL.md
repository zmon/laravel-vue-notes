# Notes when having problems installing MySQL with Brew

### Background: Fresh mysql/mariadb installed by homebrew.

### Problem: The password for root is not empty and unknown.

### The fix:
```
   mysql -u `whoami` -p
```   
The password is empty (press enter)
```
   ALTER USER 'root'@'localhost' IDENTIFIED BY 'NEW-ROOT-PASSWORD';
   FLUSH PRIVILEGES;
```

### The reason:

Homebrew will create a user with root privileges named by the current MacOS username.
it has no password
Since it has all privileges, just reset the root password with that user.
The initial password for root was randomly generated.



## Install

brew update
# brew doctor
brew install mysql@8.0

```
We've installed your MySQL database without a root password. To secure it run:

    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:

    mysql -u root

mysql@8.0 is keg-only, which means it was not symlinked into /usr/local,
because this is an alternate version of another formula.

If you need to have mysql@8.0 first in your PATH, run:

  echo 'export PATH="/usr/local/opt/mysql@8.0/bin:$PATH"' >> ~/.zshrc

For compilers to find mysql@8.0 you may need to set:

  export LDFLAGS="-L/usr/local/opt/mysql@8.0/lib"
  export CPPFLAGS="-I/usr/local/opt/mysql@8.0/include"

For pkg-config to find mysql@8.0 you may need to set:

  export PKG_CONFIG_PATH="/usr/local/opt/mysql@8.0/lib/pkgconfig"

To restart mysql@8.0 after an upgrade:

  brew services restart mysql@8.0

Or, if you don't want/need a background service you can just run:

  /usr/local/opt/mysql@8.0/bin/mysqld_safe --datadir\=/usr/local/var/mysql
```

### Remove MySQL
https://gist.github.com/vitorbritto/0555879fe4414d18569d
```
pkill mysqld;
brew remove mysql
brew cleanup
# brew doctor
sudo rm /usr/local/mysql
sudo rm -rf /usr/local/var/mysql
sudo rm -rf /usr/local/mysql*


rm -rf /usr/local/var/mysql;
rm /usr/local/etc/my.cnf;

sudo rm ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
sudo rm -rf /Library/StartupItems/MySQLCOM
sudo rm -rf /Library/PreferencePanes/My*
launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
rm -rf ~/Library/PreferencePanes/My*
sudo rm -rf /Library/Receipts/mysql*
sudo rm -rf /Library/Receipts/MySQL*
sudo rm -rf /private/var/db/receipts/*mysql*
```


### Other

brew services stop mysql@8.4


https://stackoverflow.com/questions/50691977/how-to-reset-the-root-password-in-mysql-8-0-11

https://stackoverflow.com/questions/9695362/macosx-homebrew-mysql-root-password

mysql_secure_installation

sudo mysqld_safe --skip-grant-tables --skip-networking

mysqladmin -u root password NEWPASS



