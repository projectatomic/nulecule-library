# Gitlab CentOS 7 Atomic App

### Description

This Atomic App is a 3 tier application based on redis, postgresql and gitlab. This is also an example of Nulecule having multiple tier artifacts rather using graphs.

### Deployment

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/gitlab-centos7-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/gitlab-centos7-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/gitlab-centos7-atomicapp --mode fetch --destination gitlab-centos7-atomicapp
cd gitlab-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/gitlab-centos7-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/gitlab-centos7-atomicapp --destination gitlab-centos7-atomicapp
cd gitlab-centos7-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

The default port for Gitlab web app is :30000

For first time login, the credentials are:
```
  - username: root
  - password: 5iveL!fe
```

#### Using the Docker Provider

```sh
curl localhost:30000
<html-foobar>
```

#### Using the Kubernetes Provider

By default kubernetes will assign an available external IP to the Gitlab instance.

The node port specified (:30000) will be assigned to a Gitlab instance and thus curl'ing the localhost will work.

```sh
curl localhost:30000
<html-output>
```
