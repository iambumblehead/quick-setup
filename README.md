Quick Setup Steps
=================

-------------------------------------------------------------------------------
### NODE.JS:

 1. **Get Node**
    ```bash
    $ wget http://nodejs.org/dist/latest/node-v0.12.0-linux-x86.tar.gz
    ```
 
 2. **Unpack Node**
    ```bash
    $ tar -xvf node-v*.tar.gz
    ```

 3. **Install Node**, _gcc, g++ must be installed_
    ```bash 
    $ cd node-v*
    $ ./configure # for remote server use ./configure --jobs=1 --prefix=$HOME
    $ make
    $ sudo make install
    ```
    
 4. **Make _node_ Available to Shell** _relogin to test_
    *./bashrc*
    ```bash
    export PATH=$PATH:/usr/local/bin/
    ```


-------------------------------------------------------------------------------
### GIT:

setup a git repository on the host server.

 1. **Install**
    ```bash
    $ wget http://kernel.org/pub/software/scm/git/git-1.7.5.tar.gz
    $ cd git*
    $ ./configure --prefix=$HOME/git/
    $ make
    $ make install
    $ $HOME/bin/git --version
    ```

 2. **Make available through ssh.** _relogin to test_
    *~/.bashrc*
    ```
    export PATH=$PATH:$HOME/git/bin/
    ```

 3. **Configure Remote**
    ```bash
    $ mkdir myproject.com && cd /myproject.com
    $ git init
    $ git add .
    $ git config --global user.email "myman@myhost.com"
    $ git config --global user.name "myman"
    $ git commit -m "initial import"
    $ git config --bool core.bare true
    ```

 4. **Configure Local**
    ```bash
    $ git clone myman@myhost.com:~/gitapps/remoterepo
    $ git commit -a -m "added the howto file"
    $ git push origin master
    ```

-------------------------------------------------------------------------------
### MONGODB:


 1. **Download**
    ```bash
    $ git clone git://github.com/mongodb/mongo.git
    ```
 
 2. **Run**
    ```bash
    $ ./mongod # or ./mongod --config ~/mongodb.conf
    ```

-------------------------------------------------------------------------------
### LIGHTTPD:

 1. **Install**
    ```bash
    $ sudo apt-get install lighttpd
    ```
 
 2. **Start**
    ```bash
    $ sudo /etc/init.d/lighttpd start
    ```
 
 3. **Test**
    ```bash
    http://198.199.50.50/index.lighttpd.html
    ```

 4. **Replace**
    ```bash
    /var/www/index.lighttpd.html
    ```

 5. **Add mod_proxy**
    */etc/lighttpd/lighttpd.conf*


-------------------------------------------------------------------------------
### NGINX:

 1. **Install NGINX**
    ```bash
    $ sudo apt-get install nginx
    ```

 2. **Start NGINX**
    ```bash
    $ sudo service nginx start
    ```

-------------------------------------------------------------------------------
### Generate a Fake CA

http://www.akadia.com/services/ssh_test_certificate.html
http://stackoverflow.com/questions/9519707/can-nodejs-generate-ssl-certificates

When prompted for Common Name I like to give 'local.$myhost.com'

```bash
$ openssl genrsa -out server-key.pem 1024
$ openssl req -new -key server-key.pem -out server-csr.pem
$ openssl x509 -req -in server-csr.pem -signkey server-key.pem -out server-cert.pem
```
