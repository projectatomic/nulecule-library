###Overview

This is an atomicapp based on Nulecule specification. This is a 2-tier
application based on [Flask](flask.pocoo.org) and [redis](redis.io). Every time
you access the web page, a message is displayed which indicates the number of
times the web page was accessed. And this counter is incremented upon each
access.

###Prerequisites

The redis container has a volume mounted from the host system. At the moment we
are mounting `/opt/redis` on `/redis` in the redis container. This is mainly
for the sake of persistence, in that, even if a redis container/pod is killed
and started afresh, the count is stored. For this to work, we need to apply
below SELinux context on `/opt/redis` on the host:

    $ sudo chcon -Rt svirt_sandbox_file_t /opt/redis

This app is based on [CentOS 7](https://hub.docker.com/_/centos/) image.

###Usage

####Option 1 - Interactive

Run the image with below command. It'll use `kubernetes` as the default
provider. It will prompt for the parameters in Nulecule file that do not have
default values.

    $ [sudo] atomic run dharmit/flask_redis

####Option 2 - Unattended

Create a new directory and in that, create a file called `answers.conf` with
below contents:

    [flask]
    flaskImage = dharmit/flask:latest
    NODE_PORT = 31000
    [redis]
    redisImage = dharmit/redis:latest
    redisPath = /opt/redis
    [general]
    namespace = default
    provider = kubernetes

Now, from the directory containting `answers.conf` file, run the application:

    $ [sudo] atomic run dharmit/flask_redis

####Option 3 - Install and Run

You can download the application, review the `Nulecule` file and edit
answerfile before running the application.

1. Download the app using `atomic install`:

        [sudo] atomic install dharmit/flask_redis

2. Rename `answers.conf.sample`:

        mv answers.conf.sample answers.conf

3. Edit `answers.conf`, review the files if desired and run:

       [sudo] atomic run dharmit/flask_redis

###Check the app

To check the app, open [http://localhost:31000](http://localhost:31000) in the
web browser. If you have chosen some other value for the environment variable
`NODE_PORT`, use that port instead of 31000.
