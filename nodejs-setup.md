### Install Node 6.x
```
  $ curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
```

### Install Node 7.x
```
  $ curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
```

### Upgrade Node JS
```
  $ sudo npm cache clean -f
  $ sudo npm install -g n
  $ sudo n stable

  $ sudo ln -sf /usr/local/n/versions/node/<VERSION>/bin/node /usr/bin/node
  
  // for latest only
  $ sudo n latest

  // upgrade (or downgrade) to specific version
  $ sudo n <version>
  
  // To undo:
  $ sudo apt-get install --reinstall nodejs-legacy     # fix /usr/bin/node
  $ sudo n rm 6.0.0     # replace number with version of Node that was installed
  $ sudo npm uninstall -g n
```

### Install NPM
```
  $ sudo apt-get install npm
```

### Install pm2 for boot automatic script
```
  $ sudo npm install -g pm2
```
