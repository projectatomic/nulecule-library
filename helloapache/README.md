# Hello Apache

### Description

A helloworld example using the centos/apache container.

### Deployment

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/helloapache
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/helloapache
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/helloapache --mode fetch --destination helloapache
cd helloapache
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/helloapache .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/helloapache --destination helloapache
cd helloapache
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
kubectl describe pod helloapache
Name:           helloapache
Namespace:      default
Node:           127.0.0.1/127.0.0.1
Start Time:     Wed, 30 Mar 2016 15:05:50 -0400
Labels:         app=helloapache
Status:         Running
IP:             172.17.0.5

curl 172.17.0.5
<html-output>
```
