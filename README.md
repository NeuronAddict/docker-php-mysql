# Quick php+mysql docker-compose

Docker ready to use with : 

- php
- mysql
- xdebug


## Quickstart

You need docker and docker-compose.

```
$ git clone https://github.com/NeuronAddict/docker-php-mysql.git
$ cd docker-php-mysql
$ echo '<?php echo "coucou\n"; ?>' > src/index.php
$ docker-compose up
<your apache and mysql logs>
```
Now, in other console :

```
$ curl http://127.0.0.1:8181
coucou
```

Open the project with phpstorm and enable debugging.

### Configuration

#### php source files
Put your php files into src, src become your apache root.

#### mysql init

Put in folder docker-entrypoint-initdb.d your sql file. It will be executed at statup.
See https://hub.docker.com/_/mysql/ for more help.

#### mysql config
Put your cnf files into mysql/conf.d folder.
See https://dev.mysql.com/doc/refman/8.0/en/option-files.html for more help.


#### add php module
Modify the Dockerfile in php. See https://hub.docker.com/_/php/ for more help.

### debug in php storm or intellij idea

- run a docker-compose configuration with the docker-compose.yml on the root
- click on the 'run a listener to debug php' at right at the run button.
- add a breakpoint on your index.php file

### save the sql databse for later usage

You can save the current state of the database for later start :

```
sh -c 'docker exec -it dockerphpmysql_mysql_1 mysqldump -u mysql -pmysql db' > docker-entrypoint-initdb.d/dump.sql
```

(All files on docker-entrypoint-initdb.d are executeds by the database at startup)
