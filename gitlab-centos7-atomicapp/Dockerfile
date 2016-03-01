FROM projectatomic/atomicapp:0.4.3

MAINTAINER Red Hat, Inc. <container-tools@redhat.com>

LABEL io.projectatomic.nulecule.specversion="0.0.2" \
      io.projectatomic.nulecule.providers="kubernetes,docker"\
      Build="docker build --rm --tag test/gitlab-atomicapp ."

ADD /Nulecule /Dockerfile README.md gpl-3.0.txt /application-entity/
ADD /artifacts /application-entity/artifacts
