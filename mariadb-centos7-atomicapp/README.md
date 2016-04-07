# MariaDB CentOS 7 Atomic App

### Description

A single container application built on the centos/mariadb image.

### Deployment

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/mariadb-centos7-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/mariadb-centos7-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/mariadb-centos7-atomicapp --mode fetch --destination mariadb-centos7-atomicapp
cd mariadb-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/mariadb-centos7-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/mariadb-centos7-atomicapp --destination mariadb-centos7-atomicapp
cd mariadb-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

The default port is :3306

#### Using the Docker Provider

```sh
docker run -it centos/mariadb mysql -h localhost -u <username> -p <database name>
```

#### Using the Kubernetes Provider

By default kubernetes will assign an available external IP.

```sh
kubectl get service mariadb
NAME      LABELS    SELECTOR       IP               PORT(S)
mariadb   name=db   name=mariadb   10.254.167.159   3306/TCP

docker run -it centos/mariadb mysql -h <IP address> -u <username> -p <database name>
Enter password: <password>
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 3
Server version: 10.0.17-MariaDB MariaDB Server

Copyright (c) 2000, 2015, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [dbname]> show databases;
+--------------------+
| Database           |
+--------------------+
| dbname             |
| information_schema |
| mysql              |
| performance_schema |
| test               |
+--------------------+
5 rows in set (0.00 sec)
```

