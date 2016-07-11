# Nulecule Library

This library contains a set of working examples of composite container applications. The applications are specified using the [Nulecule Specification](https://github.com/projectatomic/nulecule). This specification allows for reusable components and defines a full multi-container application. You may use the applications for reference or, in some cases, deployment.

These examples are all intended to be used with [atomicapp](https://github.com/projectatomic/atomicapp). There is a thorough [getting started guide](https://github.com/projectatomic/atomicapp/blob/master/docs/start_guide.md) available.

### Index

- [apache-centos7-atomicapp](apache-centos7-atomicapp/):
    - A centos/apache container similar to the "helloapache" example
- [etherpad-centos7-atomicapp](etherpad-centos7-atomicapp/):
    - This is a multi-container application that uses both Etherpad and MariaDB
- [flask-redis-centos7-atomicapp](flask-redis-centos7-atomicapp/):
    - A 2-tier application based on Flask and Redis
- [gitlab-centos7-atomicapp](gitlab-centos7-atomicapp/):
    - A 3-tier application based on Redis, PostgreSQL and Gitlab 
- [gocounter-scratch-atomicapp](gocounter-scratch-atomicapp/):
    - A stand-alone Go application that displays a counter for each web visit
- [helloapache](helloapache/):
    - A helloworld example using the centos/apache container
- [mariadb-centos7-atomicapp](mariadb-centos7-atomicapp/):
    - A single container application built on the centos/mariadb image
- [mariadb-fedora-atomicapp](mariadb-fedora-atomicapp/):
    - A single container application built on the fedora/mariadb image
- [mongodb-centos7-atomicapp](mongodb-centos7-atomicapp/):
    - A single container application built on the centos/mongodb-26-centos7 image
- [postgresql-centos7-atomicapp](postgresql-centos7-atomicapp/):
    - It's a single container application based on the centos/postgresql image
- [redis-centos7-atomicapp](redis-centos7-atomicapp/):
    - A Redis sample application, in which Redis master and slave components are packaged as an Atomic App
- [skydns-atomicapp](skydns-atomicapp/):
    - Deploys SkyDNS on the respective Kubernetes cluster
- [wordpress-centos7-atomicapp](wordpress-centos7-atomicapp/):
    - This is a Wordpress AtomicApp based on the Nulecule specification. 
    - It will reuse the MariaDB AtomicApp to provide Kubernetes, OpenShift3 and Docker based Wordpress to you


### Library format

__Files:__

Please only include the `/artifact` directory and the Nulecule, Dockerfile and README.md files in your application.

__For example [projectatomic/helloapache](https://github.com/projectatomic/nulecule-library/tree/master/helloapache), only includes the following files:__

```sh
.
├── artifacts
│   ├── docker
│   │   └── hello-apache-pod_run
│   ├── kubernetes
│   │   └── hello-apache-pod.json
├── Dockerfile
├── Nulecule
└── README.md
```

__The README.md file should contain the following three sections:__

  1. Description: What the application does
  2. Deployment: How to deploy the application using the `atomic` or `atomicapp` CLIs
  3. Interaction: How to access/use the application after deployment

### Generating the `index.yaml` for `atomicapp index list` commands

In order to generate a Docker-compatible image for an Atomic App library index. Use the following steps:

```
atomicapp index generate .
docker build -t $USER/index .
```

### Contributing

Feel free to open a PR if you wish to contribute to the nulecule-library! We accept all kind of applications.


### Communication channels

* IRC: #nulecule (On Freenode)
* Mailing List: [container-tools@redhat.com](https://www.redhat.com/mailman/listinfo/container-tools)
