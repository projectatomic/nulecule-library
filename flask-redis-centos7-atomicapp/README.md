###Overview

This is an atomic application based on Nulecule specification. This is a 2-tier
application based on [flask](flask.pocoo.org) and [redis](redis.io). Every time
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

To run this app, workstation needs to have atomic command. Use below command to
start the app:

    $ atomic run dharmit/flask_redis

To check the app, open [http://localhost:5000](http://localhost:5000) in the
web browser.

###Known Issues/ToDo

Things like port 5000 and volume to be mounted on redis container are hardcoded
at the moment. This could be changed with minor tweaks.
