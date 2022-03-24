# Java HTTP Server
## Understanding Image layers & caching


### Checkout the source code

Checkout the source code from [this](https://github.com/sridhar09/docker-java-http) repository

### Create a new docker image

Create a new docker image with this command 

```bash
docker build -t [your-dockerhub-id]/java-http-server .
```

You will see an output similar to this

```
[+] Building 33.0s (11/11) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                             0.0s
 => => transferring dockerfile: 389B                                                                                                                                                             0.0s
 => [internal] load .dockerignore                                                                                                                                                                0.0s
 => => transferring context: 2B                                                                                                                                                                  0.0s
 => [internal] load metadata for docker.io/library/openjdk:8-jdk-alpine                                                                                                                          7.4s
 => [auth] library/openjdk:pull token for registry-1.docker.io                                                                                                                                   0.0s
 => [internal] load build context                                                                                                                                                                0.0s
 => => transferring context: 1.61kB                                                                                                                                                              0.0s
 => [1/6] FROM docker.io/library/openjdk:8-jdk-alpine@sha256:94792824df2df33402f201713f932b58cb9de94a0cd524164a0f2283343547b3                                                                   23.4s
 => => resolve docker.io/library/openjdk:8-jdk-alpine@sha256:94792824df2df33402f201713f932b58cb9de94a0cd524164a0f2283343547b3                                                                    0.0s
 => => sha256:94792824df2df33402f201713f932b58cb9de94a0cd524164a0f2283343547b3 1.64kB / 1.64kB                                                                                                   0.0s
 => => sha256:44b3cea369c947527e266275cee85c71a81f20fc5076f6ebb5a13f19015dce71 947B / 947B                                                                                                       0.0s
 => => sha256:a3562aa0b991a80cfe8172847c8be6dbf6e46340b759c2b782f8b8be45342717 3.40kB / 3.40kB                                                                                                   0.0s
 => => sha256:e7c96db7181be991f19a9fb6975cdbbd73c65f4a2681348e63a141a2192a5f10 2.76MB / 2.76MB                                                                                                   1.0s
 => => sha256:f910a506b6cb1dbec766725d70356f695ae2bf2bea6224dbe8c7c6ad4f3664a2 238B / 238B                                                                                                       1.0s
 => => sha256:c2274a1a0e2786ee9101b08f76111f9ab8019e368dce1e325d3c284a0ca33397 70.73MB / 70.73MB                                                                                                21.7s
 => => extracting sha256:e7c96db7181be991f19a9fb6975cdbbd73c65f4a2681348e63a141a2192a5f10                                                                                                        0.2s
 => => extracting sha256:f910a506b6cb1dbec766725d70356f695ae2bf2bea6224dbe8c7c6ad4f3664a2                                                                                                        0.0s
 => => extracting sha256:c2274a1a0e2786ee9101b08f76111f9ab8019e368dce1e325d3c284a0ca33397                                                                                                        1.5s
 => [2/6] COPY ./classes/ /tmp/classes/                                                                                                                                                          0.2s
 => [3/6] COPY ./source/ /tmp/source/                                                                                                                                                            0.0s
 => [4/6] RUN javac -d /tmp/classes/ /tmp/source/HTTPServer.java &&  cd /tmp/classes/ &&  jar cvfm HTTPServer.jar manifest.txt *.class                                                           1.5s
 => [5/6] RUN cp /tmp/classes/HTTPServer.jar /HTTPServer.jar                                                                                                                                     0.4s
 => exporting to image                                                                                                                                                                           0.0s
 => => exporting layers                                                                                                                                                                          0.0s
 => => writing image sha256:fc099c295244ae3be20ff2abfcd6dbbbbcd1d60383cd10ddb4d2b0bcf7b460f5                                                                                                     0.0s
 => => naming to docker.io/msridhar009/java-http-server                                                                                                                                          0.0s

```

### Run the webserver

```bash
docker run -d -p 8000:8000 java-http-server
```

### Verify the webserver is running

Vist ``http://localhost:8000/test``

You will see an text similar to this

```
The webserver works!!
How awesome is that?
```

### Kill the container

```bash
docker kill [CONTAINER ID]
```

### See the docker history

```bash
docker history [your-dockerhub-id]/java-http-server
```

You will see an output similar to this

```
IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
fc099c295244   2 minutes ago   EXPOSE map[8000/tcp:{}]                         0B        buildkit.dockerfile.v0
<missing>      2 minutes ago   ENTRYPOINT ["java" "-Xmx256m" "-jar" "./HTTP…   0B        buildkit.dockerfile.v0
<missing>      2 minutes ago   RUN /bin/sh -c cp /tmp/classes/HTTPServer.ja…   2.37kB    buildkit.dockerfile.v0
<missing>      2 minutes ago   WORKDIR /                                       0B        buildkit.dockerfile.v0
<missing>      2 minutes ago   RUN /bin/sh -c javac -d /tmp/classes/ /tmp/s…   4.92kB    buildkit.dockerfile.v0
<missing>      2 minutes ago   COPY ./source/ /tmp/source/ # buildkit          1.39kB    buildkit.dockerfile.v0
<missing>      2 minutes ago   COPY ./classes/ /tmp/classes/ # buildkit        24B       buildkit.dockerfile.v0
<missing>      2 years ago     /bin/sh -c set -x  && apk add --no-cache   o…   99.3MB
<missing>      2 years ago     /bin/sh -c #(nop)  ENV JAVA_ALPINE_VERSION=8…   0B
<missing>      2 years ago     /bin/sh -c #(nop)  ENV JAVA_VERSION=8u212       0B
<missing>      2 years ago     /bin/sh -c #(nop)  ENV PATH=/usr/local/sbin:…   0B
<missing>      2 years ago     /bin/sh -c #(nop)  ENV JAVA_HOME=/usr/lib/jv…   0B
<missing>      2 years ago     /bin/sh -c {   echo '#!/bin/sh';   echo 'set…   87B
<missing>      2 years ago     /bin/sh -c #(nop)  ENV LANG=C.UTF-8             0B
<missing>      2 years ago     /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B
<missing>      2 years ago     /bin/sh -c #(nop) ADD file:a86aea1f3a7d68f6a…   5.53MB
```

Notice that there is a docker layer for each instruction in the dockerfile


### Change the dockerfile

Change Lines 7 & 8 as following

```dockerfile
WORKDIR /java
Run cp /tmp/classes/HTTPServer.jar /java/HTTPServer.jar
```

### Rerun the build

```
docker build -t msridhar009/java-http-server .
```

You will see an output simialr to this
```
[+] Building 7.7s (12/12) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                             0.0s
 => => transferring dockerfile: 398B                                                                                                                                                             0.0s
 => [internal] load .dockerignore                                                                                                                                                                0.0s
 => => transferring context: 2B                                                                                                                                                                  0.0s
 => [internal] load metadata for docker.io/library/openjdk:8-jdk-alpine                                                                                                                          7.3s
 => [auth] library/openjdk:pull token for registry-1.docker.io                                                                                                                                   0.0s
 => [1/6] FROM docker.io/library/openjdk:8-jdk-alpine@sha256:94792824df2df33402f201713f932b58cb9de94a0cd524164a0f2283343547b3                                                                    0.0s
 => [internal] load build context                                                                                                                                                                0.0s
 => => transferring context: 169B                                                                                                                                                                0.0s
 => CACHED [2/6] COPY ./classes/ /tmp/classes/                                                                                                                                                   0.0s
 => CACHED [3/6] COPY ./source/ /tmp/source/                                                                                                                                                     0.0s
 => CACHED [4/6] RUN javac -d /tmp/classes/ /tmp/source/HTTPServer.java &&  cd /tmp/classes/ &&  jar cvfm HTTPServer.jar manifest.txt *.class                                                    0.0s
 => [5/6] WORKDIR /java                                                                                                                                                                          0.0s
 => [6/6] RUN cp /tmp/classes/HTTPServer.jar /java/HTTPServer.jar                                                                                                                                0.3s
 => exporting to image                                                                                                                                                                           0.0s
 => => exporting layers                                                                                                                                                                          0.0s
 => => writing image sha256:985353e3046f2efa954f324ef848d9091c495e19e4cefc4634aa7fe8426ac57d                                                                                                     0.0s
 => => naming to docker.io/msridhar009/java-http-server
```

1. Notice that the build took very less time this time
2. Notice how some Layes (1,2,3,4) are Cached

###Check history again

You will se an output similar to 

```
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
985353e3046f   2 minutes ago    EXPOSE map[8000/tcp:{}]                         0B        buildkit.dockerfile.v0
<missing>      2 minutes ago    ENTRYPOINT ["java" "-Xmx256m" "-jar" "./HTTP…   0B        buildkit.dockerfile.v0
<missing>      2 minutes ago    RUN /bin/sh -c cp /tmp/classes/HTTPServer.ja…   2.37kB    buildkit.dockerfile.v0
<missing>      2 minutes ago    WORKDIR /java                                   0B        buildkit.dockerfile.v0
<missing>      12 minutes ago   RUN /bin/sh -c javac -d /tmp/classes/ /tmp/s…   4.92kB    buildkit.dockerfile.v0
<missing>      12 minutes ago   COPY ./source/ /tmp/source/ # buildkit          1.39kB    buildkit.dockerfile.v0
<missing>      12 minutes ago   COPY ./classes/ /tmp/classes/ # buildkit        24B       buildkit.dockerfile.v0
<missing>      2 years ago      /bin/sh -c set -x  && apk add --no-cache   o…   99.3MB
<missing>      2 years ago      /bin/sh -c #(nop)  ENV JAVA_ALPINE_VERSION=8…   0B
<missing>      2 years ago      /bin/sh -c #(nop)  ENV JAVA_VERSION=8u212       0B
<missing>      2 years ago      /bin/sh -c #(nop)  ENV PATH=/usr/local/sbin:…   0B
<missing>      2 years ago      /bin/sh -c #(nop)  ENV JAVA_HOME=/usr/lib/jv…   0B
<missing>      2 years ago      /bin/sh -c {   echo '#!/bin/sh';   echo 'set…   87B
<missing>      2 years ago      /bin/sh -c #(nop)  ENV LANG=C.UTF-8             0B
<missing>      2 years ago      /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B
<missing>      2 years ago      /bin/sh -c #(nop) ADD file:a86aea1f3a7d68f6a…   5.53MB
```

1. Notice the difference in CREATED timestamp
----

Takeaways & learnings from this exercise :

1. Docker Image layers & caching
2. Docker history command