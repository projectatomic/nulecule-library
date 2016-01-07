This is an atomic application based on the nulecule specification. You can run it on
Docker, Kubernetes, or Openshift.

This is a multi container application based on the etherpad and mariadb

### Step 1: Get answers file

Grab the answers file from the application:

```
$ [sudo] atomic run projectatomic/etherpad-centos7-atomicapp --mode=genanswers
```

Will populate answers.conf in the current directory. Edit the answers
file and update values (replace "None" with values).

### Step 2: Run it

To run the application in Docker and have it extracted to your local
directory:

```
$ [sudo] atomic run projectatomic/etherpad-centos7-atomicapp --provider=docker --destination ./
```

*NOTE*: Provide `--provider=kubernetes` or `--provider=openshift` to run
on those platforms.

### Step 2: Stop it

To stop the application:

```
$ [sudo] atomic stop projectatomic/etherpad-centos7-atomicapp ./
```
