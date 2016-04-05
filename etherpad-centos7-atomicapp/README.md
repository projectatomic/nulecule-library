# Etherpad CentOS 7 Atomic App

### Description

This is a multi-container application that uses both Etherpad and MariaDB.

### Deployment

__Kubernetes requirements:__ [skydns](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns) must be installed in order to utilize DNS lookup.

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/etherpad-centos7-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/etherpad-centos7-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/etherpad-centos7-atomicapp --mode fetch --destination etherpad-centos7-atomicapp
cd etherpad-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/etherpad-centos7-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/etherpad-centos7-atomicapp --destination etherpad-centos7-atomicapp
cd etherpad-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

The default port is :9001

#### Using the Docker Provider

```sh
curl localhost:9001
<html-foobar>
```

#### Using the Kubernetes Provider

By default kubernetes will assign an available external IP.

```sh
kubectl get pods
NAME                   READY     STATUS    RESTARTS   AGE
etherpad-6p7av         1/1       Running   0          5s
mariadb                1/1       Running   0          6s

kubectl describe pod etherpad-6p7av
Name:           etherpad-centos7-atomicapp
Namespace:      default
Node:           127.0.0.1/127.0.0.1
Start Time:     Wed, 30 Mar 2016 15:05:50 -0400
Labels:         app=etherpad-centos7-atomicapp
Status:         Running
IP:             172.17.0.5

curl 172.17.0.5:9001
<html-output>
```

