# MongoDB CentOS 7 Atomic App

### Description

A single container application built on the centos/mongodb-26-centos7 image.

### Deployment

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/mongodb-centos7-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/mongodb-centos7-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/mongodb-centos7-atomicapp --mode fetch --destination mongodb-centos7-atomicapp
cd mongodb-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/mongodb-centos7-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/mongodb-centos7-atomicapp --destination mongodb-centos7-atomicapp
cd mongodb-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

The default port is :27017

#### Using the Docker Provider

```sh
mongo --host localhost --port 27017 -u <MongoDB Username> -p <MongoDB Password>
```

#### Using the Kubernetes Provider

By default kubernetes will assign an available external IP.

```sh
docker run -it --rm mongo mongo --host <IP Address> --port <MongoDB Port> -u <MongoDB Username> -p <MongoDB Password>
> db.getName();
some-db
```
