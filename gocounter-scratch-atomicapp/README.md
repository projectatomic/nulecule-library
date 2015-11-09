###Overview

This is an atomicapp based on Nulecule specification. This is a standalone 
Golang application based on this [example](https://gist.github.com/technovangelist/b48e95d995bc420eeab0).
Every time you access the web page, a message is displayed which indicates the
number of times the web page was accessed in past one minute.

Motivation of this example is to showcase a quick example running using
atomicapp. The Docker image `dharmit/gocounter` is under 7 MB in size!

###Prerequisites

You need to install `atomicapp` from its [git
repo](https://github.com/projectatomic/atomicapp/) before being able to check
the app.

###Usage

####Option 1 - Interactive

Run the image with below command. It'll use `kubernetes` as the default
provider. It will prompt for the parameters in Nulecule file that do not have
default values.

    $ [sudo] atomicapp run dharmit/gocounterapp

####Option 2 - Unattended

Create a new directory and in that, create a file called `answers.conf` with
below contents:

    [gocounter]
    goImage = dharmit/gocounter:master
    NODE_PORT = 32000
    [general]
    namespace = default
    provider = docker


Now, from the directory containting `answers.conf` file, run the application:

    $ [sudo] atomicapp run -a answers.conf dharmit/gocounterapp

####Option 3 - Install and Run

You can download the application, review the `Nulecule` file and edit
answerfile before running the application.

1. Download the app using `atomicapp install`:

        [sudo] atomicapp install dharmit/gocounterapp

2. `cd` into the directory where the files were loaded by above command. Rename
   `answers.conf.sample`:

        mv answers.conf.sample answers.conf

3. Edit `answers.conf`, review the files if desired and run:

        [sudo] atomicapp run -a answers.conf dharmit/gocounterapp

###Check the app

To check the app, open [http://localhost:32000](http://localhost:32000) in the
web browser. If you have chosen some other value for the environment variable
`NODE_PORT`, use that port instead of 32000.
