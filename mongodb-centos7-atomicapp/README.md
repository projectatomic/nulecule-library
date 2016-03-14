This is an atomic application based on the nulecule specification. Kubernetes and native docker are currently the only supported providers. You'll need to run this from a workstation that has the atomic command and kubectl client that can connect to a kubernetes master.

It's a single container application based on the ``centos/mongodb-26-centos7`` image.

### Option 1: Unattended

Run the image. It will automatically use kubernetes as the orchestration provider.

    $ [sudo] atomic run projectatomic/mongodb-centos7-atomicapp
