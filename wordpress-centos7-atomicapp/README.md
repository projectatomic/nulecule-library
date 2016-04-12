# Wordpress CentOS 7 Atomic App

### Description

This is a Wordpress AtomicApp based on the Nulecule specification. It will reuse the MariaDB AtomicApp to provide Kubernetes, OpenShift3 and Docker based Wordpress to you.

### Deployment

__Kubernetes requirements:__ [skydns](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns) must be installed in order to utilize DNS lookup.

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/wordpress-centos7-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/wordpress-centos7-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/wordpress-centos7-atomicapp --mode fetch --destination wordpress-centos7-atomicapp
cd wordpress-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/wordpress-centos7-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/wordpress-centos7-atomicapp --destination wordpress-centos7-atomicapp
cd wordpress-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

The default port is :80

#### Using the Docker Provider

```sh
curl localhost:80
<html-foobar>
```

#### Using the Kubernetes Provider

By default kubernetes will assign an available external IP.

```sh
kubectl get pods
NAME                   READY     STATUS    RESTARTS   AGE
mariadb                1/1       Running   0          5h
wordpress              1/1       Running   0          5h

kubectl describe pod wordpress
Name:           wordpress
Namespace:      default
Node:           127.0.0.1/127.0.0.1
Start Time:     Thu, 07 Apr 2016 09:29:26 -0400
Labels:         name=wordpress-frontend
Status:         Running
IP:             172.17.0.5

curl 172.17.0.5:80
<html-output>
```
