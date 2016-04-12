# Guestbook Go Atomic App

### Description

This is the [guestbook-go](https://github.com/GoogleCloudPlatform/kubernetes/tree/master/examples/guestbook-go) sample application from the kubernetes project, packaged as an atomic application based on the nulecule specification. 

### Deployment

__Kubernetes requirements:__ [skydns](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns) must be installed in order to utilize DNS lookup.

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/guestbook-go-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/guestbook-go-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/guestbook-go-atomicapp --mode fetch --destination guestbook-go-atomicapp
cd guestbook-go-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/guestbook-go-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/guestbook-go-atomicapp --destination guestbook-go-atomicapp
cd guestbook-go-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

The default port is :31288

#### Using the Kubernetes Provider

By default kubernetes will assign an available external IP.


```
$ kubectl describe service guestbook | grep NodePort

NodePort:   <unnamed> 31288/TCP
```

```
$ kubectl get nodes
NAME          LABELS                               STATUS
kube-node-1   kubernetes.io/hostname=kube-node-1   Ready
```

```
$ kubectl describe nodes kube-node-1 | grep Addresses
Addresses:  192.168.121.174
```

```
curl 192.168.121.174:31288
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta content="text/html; charset=utf-8" http-equiv="Content-Type">
    <meta charset="utf-8">
    <meta content="width=device-width" name="viewport">
    <link href="/style.css" rel="stylesheet">
    <title>Guestbook</title>
  </head>
...
``` 
