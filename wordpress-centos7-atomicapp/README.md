# Wordpress AtomicApp

This is a Wordpress AtomicApp based on the Nulecule specification.
It will reuse the MariaDB AtomicApp to provide Kubernetes, OpenShift3 and Docker based Wordpress to you.

This example depends on [kube-dns](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns)
 being configured on your cluster, when using Kubernetes.

Currently supported providers:
- Kubernetes
- OpenShift3
- Native Docker

You'll need to run this from a workstation that has the atomic command.
If you wish to use the Kubernetes provider, you will also need a `kubectl`
client that can connect to a Kubernetes master.

This is multicontainer AtomicApp, it will reuse the MariaDB Atomic App to
provide database for wordpress image, when using Kubernetes or Docker provider.

## Option 1: Interactive

Run the image. It will automatically use Kubernetes as the default orchestration provider.
```
atomic run projectatomic/wordpress-centos7-atomicapp
```

NOTE: For Wordpress image and for MariaDB image you have to use same db_pass, db_user, db_name.
Otherwise Wordpress will not be able connect to database.

## Option 2: Install and Run

Download the application files:
```
atomic run projectatomic/wordpress-centos7-atomicapp
```

Create answers.conf
```
cp answers.conf.sample answers.conf
```

Review and edit parameters in answers.conf if desired
```
$EDITOR  answers.conf
```
NOTE: For Wordpress image and for MariaDB image you have to use same db_pass, db_user, db_name.
Otherwise Wordpress will not be able connect to database.

Run application
```
atomic run projectatomic/wordpress-centos7-atomicapp
```

## Test

Get clusterIP of wordpress service.
```
# kubectl get service wordpress
NAME        LABELS                    SELECTOR                  IP(S)           PORT(S)
wordpress   name=wordpress-frontend   name=wordpress-frontend   10.254.112.20   80/TCP

```

Now you should be able to connect to that IP address and see if wordpress is
running.

```
# curl -I http://10.254.112.20/
HTTP/1.1 302 Found
Date: Wed, 04 Nov 2015 14:41:46 GMT
Server: Apache/2.4.10 (Debian) PHP/5.6.15
X-Powered-By: PHP/5.6.15
Expires: Wed, 11 Jan 1984 05:00:00 GMT
Cache-Control: no-cache, must-revalidate, max-age=0
Pragma: no-cache
Location: http://10.254.112.20/wp-admin/install.php
Content-Type: text/html; charset=UTF-8
```

# Changelog

## 2.0.0
- Modified to use [DNS in Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns)
- Added support for Docker provider
