# ERPNext-installation-Guide-Mac
## The complete guide to install ERPNext in your Mac system

### Pre-requisites 

      Python 3.6+
      Homebrew 3.6+
      Node.js 14
      Redis 5                                       (caching and real time updates)
      MariaDB                                       (to run database driven apps)
      yarn 1.12+                                    (js dependency manager)
      pip 20+                                       (py dependency manager)


### STEP 1 Install brew
Homebrew is an app for macOS that allows you to install a huge variety of UNIX software on your Mac 
with one simple command (on the command line).

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    
here you can see the full installation guide.    

    https://treehouse.github.io/installation-guides/mac/homebrew


### STEP 2 Install git
Git is the most commonly used version control system. Git tracks the changes you make to files, 
so you have a record of what has been done, and you can revert to specific versions should you ever need to. 
Git also makes collaboration easier, allowing changes by multiple people to all be merged into one source.
    
    brew install git


### STEP 3 Install setuptools and pip (Python's Package Manager).
Setuptools is a collection of enhancements to the Python distutils that allow developers 
to more easily build and distribute Python packages, especially ones that have 
dependencies on other packages. Packages built and distributed using setuptools 
look to the user like ordinary Python packages based on the distutils.

pip is a package manager for Python.  It's a tool that allows you to install and manage 
additional libraries and dependencies that are not distributed as part of the standard library.

    sudo pip3 install setuptools

### STEP 4 Install virtualenv
virtualenv is a tool for creating isolated Python environments containing their own copy of
python , pip , and their own place to keep libraries installed from PyPI.
It's designed to allow you to work on multiple projects with different dependencies 
at the same time on the same machine.
    
    sudo pip3 install virtualenv
    

### STEP 5 Install MariaDB
MariaDB is developed as open source software and as a relational database it provides an SQL interface 
for accessing data.

open this link

    https://mariadb.com/resources/blog/installing-mariadb-10-1-16-on-mac-os-x-with-homebrew/
 
Install Mariadb

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
    brew install mariadb
    mysql_install_db
    mariadb-secure-installation
    mariadb -u root -p
    
     
IMPORTANT :During this installation you'll be prompted to set the MySQL root password.
If you are not prompted for the same You can initialize the MySQL server setup by executing 
the following command
    
    sudo mysql_secure_installation
    
### STEP 6  MySQL database development files

    brew install mysql-client

### STEP 7 Edit the mariadb configuration ( unicode character encoding )

    sudo nano /opt/homebrew/mariadb/my.cnf

add this to the my.cnf file

    [mysqld]
    character-set-client-handshake = FALSE
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci

    [mysql]
    default-character-set = utf8mb4

Now press (Ctrl-X) to exit

    brew services start mariadb

NOTE: After setting the mariadb configuration if you still face this type of issue.

    Creation of your site - site1.local failed because MariaDB is not properly
    configured to use the Barracuda storage engine.
    Please add the settings below to MariaDB's my.cnf, restart MariaDB then
    run `bench new-site site1.local` again.
    
then you have to go in mariadb shell and run these commands

      SET collation_server = 'utf8mb4_unicode_ci';
      brew services restart mariadb

### STEP 8 install Redis
Redis is an open source (BSD licensed), in-memory data structure store, used as a database, 
cache, and message broker.
    
    brew install redis

### STEP 9 install Node.js 14.X package
Node.js is an open source, cross-platform runtime environment for developing server-side and 
networking applications. Node.js applications are written in JavaScript, and can be run within the Node.js
runtime on OS X, Microsoft Windows, and Linux.

    brew install node
    
This will be install latest version of Node.

If you want to change the node version you can use NVM.

    https://tecadmin.net/install-nvm-macos-with-homebrew/

### STEP 10  install Yarn
Yarn is a JavaScript package manager that aims to be speedy, deterministic, and secure. 
See how easy it is to drop yarn in where you were using npm before, and get faster, more reliable installs.
Yarn is a package manager for JavaScript.
    
    sudo npm install -g yarn

### STEP 11 install wkhtmltopdf
Wkhtmltopdf is an open source simple and much effective command-line shell utility that enables 
user to convert any given HTML (Web Page) to PDF document or an image (jpg, png, etc)

    brew install wkhtmltopdf
    
    
### STEP 12 install frappe-bench

    sudo -H pip3 install frappe-bench

IMPORTANT: you may wish to log out and log back into your terminal 
before next step and You must login.
    
    bench --version
    
### STEP 13 initilise the frappe bench & install frappe latest version 

    bench init frappe-bench --frappe-branch version-13
    
    cd frappe-bench/
    bench start
    
### STEP 14 create a site in frappe bench 
    
    bench new-site site1.local

### STEP 15 install ERPNext latest version in bench & site

    bench get-app erpnext --branch version-13
    ###OR
    bench get-app https://github.com/frappe/erpnext --branch version-13

    bench --site site1.local install-app erpnext

    bench --site site1.local add-to-hosts
    
    bench start
    
Your server will run on this host

    http://site1.local:8000/
