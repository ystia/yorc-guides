# Install Alien4Cloud

Alien4Cloud is the Orchestrator UI companion.
It provides a catalog of components and application templates and can rely on Yorc to deploy these application templates.
Yorc provides a plugin so that Alien4Cloud can interact with the orchestrator.

First you need to install Alien4Cloud. Yorc 3.0.1 requires Alien4Cloud 2.0.0.
You can either install manually Alien4Cloud dependencies python, curl, java 8 as described
in [ALien4Cloud 2.0.0 Getting Started guide](https://alien4cloud.github.io/#/documentation/2.0.0/getting_started/new_getting_started.html),
or use the docker image alien4cloud/alien4cloud:2.0.0 avaliable on [Docker Hub](https://hub.docker.com/r/alien4cloud/alien4cloud/).

The open source distribution of Alien4Cloud 2.0.0 can be downloaded at :
https://fastconnect.org/maven/service/local/repositories/opensource/content/alien4cloud/alien4cloud-dist/2.0.0/alien4cloud-dist-2.0.0-dist.tar.gz
There is also a premium edition (see https://alien4cloud.github.io/common/download.html) 
with interesting additional features, like the ability to see applications deployment
logs from the underlying orchestrator.

To install and run the Alien4Cloud Open Source edition through a docker container, run this command :
```bash
$ docker run -d --name a4c -p 8088:8088 alien4cloud/alien4cloud:2.0.0
```

Or if you are using a HTTP proxy that needs to be known by Alien4Cloud, for example 
if you need to import archives in Alien4cloud from an external web site,
you can define this proxy in Alien4Cloud using the environment variable `JAVA_EXT_OPTIONS`.

So the docker command to run would be :
```bash
$ docker run -d --name a4c \
             -p 8088:8088 \
             -e JAVA_EXT_OPTIONS="-Dhttp.proxyHost=10.1.2.3 -Dhttp.proxyPort=8080 -Dhttp.nonProxyHosts=\"127.0.0.1|10.11.12.13|10.20.*\"" \
             alien4cloud/alien4cloud:2.0.0
```
Logs can be seen running this command:
```bash
$ docker logs -f a4c
```
Once this log appear:
```
INFO  Bootstrap:57 - Started Bootstrap in 46.171 seconds (JVM running for 47.79)
```
Alien4Cloud is ready, you can login on Alien4Cloud at `http://<your host IP address>:8088`
and login using the defaut admin user/password: admin/admin.

You can now [Configure Alien4Cloud to use Yorc](configure_a4c_yorc.md).