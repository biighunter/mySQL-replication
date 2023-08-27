# Introduction

This is a sample work to learn about docker, containers, running MySQL in docker and setting up MySQL
replication using docker containers.

# Directory structure explained
Here is the directory structure and its explanation

    MySQLReplDocker
        |
        +--- conf/
        |       +--- master1.cnf
        |       +--- master2.cnf
        |       +--- slave1.cnf
        |       +--- slave2.cnf
        +--- data/
        |       +--- master1/
        |       +--- master2/
        |       +--- slave1/
        |       +--- slave2/
        +--- docker/
        |       +--- master-2-slave.yml
        |       +--- master-2-master.yml
        |       +--- slave-2-master-2-master-2-slave.yml
        +--- scripts/
        |       +--- common-functions.sh
        |       +--- master-2-slave.sh
        |       +--- master-2-master.sh
        |       +--- slave-2-master-2-master-2-slave.sh
        +--- start
        +--- stop
        +--- check_params.sh


* The folder "___conf___" contains the MySQL configuration for master and slave nodes.
* The folder "___data___" contains folders to hold data for master and slave nodes.
* The folder "___docker___" contains the docker container configuation files
* The folder "___scripts___" contains bash script which does the real job of setup of replication between the nodes

# How to get MySQL containers up and running
To run a MySQL master-slave container replication execute the command
```sh
bash start master-slave
```
To run a MySQL master-master container replication execute the command
```sh
bash start master-master
```
To run a MySQL slave-master-master-slave replication execute the command
```sh
bash start slave-master-master-slave
```

# Seeing replication in action
In order to see if the replication is actually working, you need to enable our nerd mode. Lets kick in. Execute the following command to see the docker containers which are currently running
```sh
bash info master-slave
```
This will list down the containers, where you can clearly identify the MySQL master(s) and slave(s) nodes. In order to connect to any of the container, you can execute
```sh
docker container exec -it <name-of-container> mysql -u root -p <mysql-password>
```
> The name of the container is the first column from the output of info command. Once you are inside the prompt you can execute either of the following commands
>
> SHOW MASTER STATUS
>
> SHOW SLAVE STATUS\G
>
> NOTE: Find the passwords in .env file

You can repeat the command for all the MySQL containers and then play around and see the replication action coming live.

In case you are not comfortable using command line for interacting with MySQL, this repo also has support for phpMyAdmin.
You can access phpMyAdmin over the port 8080

> Access http://localhost:8080 in your favorite browser
>
> For hostname, username, and password refer to the .env file
