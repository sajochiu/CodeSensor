
# Prerequisites
 - CentOS 7 x86_64
 - Apache Web Server

  ```sh
  sudo yum install httpd
  sudo systemctl start httpd
  sudo systemctl enable httpd
  ```
 - MariaDB Server

  ```sh
  sudo yum install mariadb-server mariadb
  sudo systemctl start mariadb
  sudo systemctl enable mariadb
  sudo /usr/bin/mysql_secure_installation
  ```
 - PHP

  ```sh
   sudo yum install php php-mysql php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-snmp php-soap curl curl-devel 
  systemctl restart httpd.service 
  ```
 - Node.js

  ```sh
  sudo yum install epel-release
  sudo yum install nodejs
  sudo yum install npm
  ```
 - Tools and Liraries
 
  ```sh
  sudo yum groupinstall 'Development Tools'
  sudo yum install libuuid-devel
  sudo yum install valgrind
  ```

# Directory Layout



# Installation 

1. Create database
 - Create database *code_sensor_2015*
 - Add user 'codesensor' (pwd: *nctucodesensor* ) to database *code_sensor_2015*
 - Initialze tables for *code_sensor_2015*
  ```sh
    sudo mysql -u codesensor -p code_sensor_2015 < tools/db_schema.sql
  ```
 - Edit tools/DBLoader_nodejs/student_roster.txt to add user accounts for CodeSensor
    - Each row contains an ID, NAME pair for each account
 - Load user accounts to DB
  ```sh
    cd tools/DBLoader_nodejs
    npm -y install
    node dbloader.js
  ```
    - The default password is 'algo'+ID
    - Password hash can be manually generated by the tool *tools/DBLoader_nodejs/gen_password_hash.js*
  
2. SELinux module
 - Install SELinux development library
  ```sh
    sudo yum selinux-policy-devel
  ```
 - Compile and install SELinux module
  ```sh
    cd 'selinux policy'/
    ln -sf /usr/share/selinux/devel/Makefile
    make 
    sudo semodule -i codesensor.pp
  ```
 - For testing, you may first disable SELinux by 
  ```sh
    sudo setenforce 0 
  ```

3. Install CodeSensor
 ```sh
  (Change to project root)
  sudo ./install
  sudo ./install_webpage
 ```

4. Open web browser and connect to *http://localhost/2015_hw1_sort_text/*
5. Try login with ID:*0000000*   PWD:*algo0000000*
6. 

install
config.php
CreateScore.php

yum install selinux-policy
yum install selinux-policy-devel

1. selinux policy

```sh
  make
  semodule -i homework.pp
```

2. HomeworkInspector/src  

  make
  cp HomeworkInspector /usr/bin/HomeworkInspector/

  ln -s build_script /usr/bin/HomeworkInspector/build_script
  ln -s init_script /usr/bin/HomeworkInspector/init_script
  ln -s skeleton_code /usr/bin/HomeworkInspector/skeleton_code

  chmod u+s /usr/bin/HomeworkInspector/HomeworkInspector
  chown root /usr/bin/HomeworkInspector/HomeworkInspector
  chcon -t homework_inspector_exec_t /usr/bin/HomeworkInspector/HomeworkInspector

  chcon -t homework_exec_t /usr/bin/valgrind.safe

3. HomeworkInspector_php

  cp * /var/www/html


4. mkdir /var/homeworks

5. mkdir /var/homeworks/queue
