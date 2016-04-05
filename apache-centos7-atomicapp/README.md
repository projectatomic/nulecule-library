# Apache CentOS 7 Atomic App

### Description

A centos/apache container similar to the "helloapache" example.

### Deployment

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/apache-centos7-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/apache-centos7-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/apache-centos7-atomicapp --mode fetch --destination helloapache
cd apache-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/apache-centos7-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/apache-centos7-atomicapp --destination helloapache
cd apache-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

#### Using the Docker Provider

The default port is :80.

```sh
curl localhost
<html-foobar>
```

#### Using the Kubernetes Provider

By default kubernetes will assign an available external IP.

```sh
kubectl describe pod apache-centos7-atomicapp
Name:           apache-centos7-atomicapp
Namespace:      default
Node:           127.0.0.1/127.0.0.1
Start Time:     Wed, 30 Mar 2016 15:05:50 -0400
Labels:         app=apache-centos7-atomicapp
Status:         Running
IP:             172.17.0.5

curl 172.17.0.5
<html-output>
```
