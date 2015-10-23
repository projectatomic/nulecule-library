This is an atomic application based on Nulecule specification. Docker is the
only supported provider at the moment but work for Kubernetes provider is under
active development. A workstation needs to have atomic command to be able to
run this app.

This is a 2-tier application based on [flask](flask.pocoo.org) and
[redis](redis.io). Every time you access the web page, a message is displayed
which indicates the number of times the web page was accessed. And this counter
is incremented upon each access.

This repo ships with an `answers.conf.sample` file which needs to be renamed as
`answers.conf`. This is because `atomic run` uses Kubernetes as default
provider and in absence of `answers.conf` file, `atomic run` will generate and
use the resulting `answers.conf`.

Thus, to run this atomic app, one needs to follow below steps:

~~~
$ mv answers.conf.sample answers.conf
$ atomic run dharmit/flask_redis
~~~

To check the app, open up port 5000 in the web browser or simply use below
`curl` command:

~~~
curl localhost:5000
~~~
