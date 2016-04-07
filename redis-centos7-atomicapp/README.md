# Redis CentOS 7 Atomic App

### Description

This is a redis sample application, in which redis master and slave components are packaged as an Atomic App.

### Deployment

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/redis-centos7-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/redis-centos7-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/redis-centos7-atomicapp --mode fetch --destination redis-centos7-atomicapp
cd redis-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/redis-centos7-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/redis-centos7-atomicapp --destination redis-centos7-atomicapp
cd redis-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

The default port is :3306

#### Using the Docker Provider

```sh
redis-cli
```

#### Using the Kubernetes Provider

By default kubernetes will assign an available external IP.

```sh
$ kubectl get service redis-master
NAME           LABELS                   SELECTOR                 IP              PORT(S)
redis-master   name=redis,role=master   name=redis,role=master   <IP Address>    <port>/TCP
$ docker run --rm -it --entrypoint=redis-cli centos/redis -h <IP Address> -p <port>
<IP Address>:<port>> get key
(nil)
<IP Address>:<port>> set key value
OK
<IP Address>:<port>> get key
"value"
<IP Address>:<port>> del key
(integer) 1
<IP Address>:<port>> get key
(nil)
<IP Address>:<port>> exit
```
