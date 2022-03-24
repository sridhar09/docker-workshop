# Dockerfile
## Creating an image that runs a SimpleHTTPServer
A Dockerfile can be used to define a docker image. In this section, we are going to create a docker image that runs a SimpleHTTPServer on python

To get started, let's follow the steps below

### Create a new Dockerfile

1. Create a new file named `Dockerfile` in an empty directory
2. Populate the following content in Dockerfile

```dockerfile
FROM python:3.8.13-slim-bullseye 
COPY index.html /
EXPOSE 7000
CMD python -m http.server 7000
```

### Create a new html file

1. Create a new file named `index.html` in the same directory
2. Populate any valid html in the file. A sample html is shown below
```html
<h4> Hello, Docker Noob </h4>
<p> You are awesome, well done </p>
```

### Build the docker image

From the same directory, run the following command

```bash
docker build -t simple-http-server .
```

You will see an output similar to this

```
[+] Building 76.1s (7/7) FINISHED                                                                                                                            
 => [internal] load build definition from Dockerfile                                                                                                    0.0s
 => => transferring dockerfile: 121B                                                                                                                    0.0s
 => [internal] load .dockerignore                                                                                                                       0.0s
 => => transferring context: 2B                                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/python:latest                                                                                        5.3s
 => [internal] load build context                                                                                                                       0.1s
 => => transferring context: 102B                                                                                                                       0.0s
 => [1/2] FROM docker.io/library/python:latest@sha256:c79b09764b2a8d920bcf3c5fe79b79370f445c855f3822069096c8995f9cee0c                                 70.4s
 => => resolve docker.io/library/python:latest@sha256:c79b09764b2a8d920bcf3c5fe79b79370f445c855f3822069096c8995f9cee0c                                  0.0s
 => => sha256:a0bf850a0df065fb202ebf8a3527699dc18322469c34733a6cb7f412a7aaefa6 10.87MB / 10.87MB                                                       11.2s
 => => sha256:c79b09764b2a8d920bcf3c5fe79b79370f445c855f3822069096c8995f9cee0c 2.14kB / 2.14kB                                                          0.0s
 => => sha256:460573a11357df4f338df5b5afe8ac1fddb6338391a318296fe9b13bd919319b 2.22kB / 2.22kB                                                          0.0s
 => => sha256:03ef5b5a30a4d05e512083b14ff1d820c96efb594a98abd24a4e199affe797c8 8.56kB / 8.56kB                                                          0.0s
 => => sha256:5492f66d270062ddb73f28649d80eef162f2c9376d53973a3557158390af4f30 54.92MB / 54.92MB                                                       15.1s
 => => sha256:540ff8c0841d610e4cc2ad3b9ed4c6edcad4f5be2add8765f416515fbc2be2a8 5.15MB / 5.15MB                                                          6.3s
 => => sha256:d751dc38ae511bbc21c148bffa7e863057cbc7b4a8ff5155f2eca7e8d03740c6 54.58MB / 54.58MB                                                       34.7s
 => => sha256:9720a112e8860134f8c112605b4ff865d333e824edc4300ee976303d693f372f 196.54MB / 196.54MB                                                     60.1s
 => => sha256:f97b81fbdbd96e6a54b663bc855d1e0a60b48960d84cafefe617a7da8382acdc 6.29MB / 6.29MB                                                         17.7s
 => => extracting sha256:5492f66d270062ddb73f28649d80eef162f2c9376d53973a3557158390af4f30                                                               2.5s
 => => extracting sha256:540ff8c0841d610e4cc2ad3b9ed4c6edcad4f5be2add8765f416515fbc2be2a8                                                               0.2s
 => => sha256:4c4dc701b2d601454d6bb94c31c2ea5877cd6e346cd26278da5cb56f714f833f 19.73MB / 19.73MB                                                       26.5s
 => => extracting sha256:a0bf850a0df065fb202ebf8a3527699dc18322469c34733a6cb7f412a7aaefa6                                                               0.3s
 => => sha256:e8a2d0a0ed405231e2ea295edc50c239adcc11e026ae913c225972590f828d69 235B / 235B                                                             27.9s
 => => sha256:6c6773b870d9e76903a755c838f70de9f097c3b5b3931d5eedd6d2fe508fb674 2.87MB / 2.87MB                                                         29.9s
 => => extracting sha256:d751dc38ae511bbc21c148bffa7e863057cbc7b4a8ff5155f2eca7e8d03740c6                                                               2.8s
 => => extracting sha256:9720a112e8860134f8c112605b4ff865d333e824edc4300ee976303d693f372f                                                               7.9s
 => => extracting sha256:f97b81fbdbd96e6a54b663bc855d1e0a60b48960d84cafefe617a7da8382acdc                                                               0.3s
 => => extracting sha256:4c4dc701b2d601454d6bb94c31c2ea5877cd6e346cd26278da5cb56f714f833f                                                               0.9s
 => => extracting sha256:e8a2d0a0ed405231e2ea295edc50c239adcc11e026ae913c225972590f828d69                                                               0.0s
 => => extracting sha256:6c6773b870d9e76903a755c838f70de9f097c3b5b3931d5eedd6d2fe508fb674                                                               0.3s
 => [2/2] COPY index.html /                                                                                                                             0.3s
 => exporting to image                                                                                                                                  0.0s
 => => exporting layers                                                                                                                                 0.0s
 => => writing image sha256:c405c74a7d9fa4b7cf9bc3fad2f5d2e11a8c2ea9e702c2d041db39b7e3f076bb                                                            0.0s
 => => naming to docker.io/library/simple-http-server  
```

### Verify that the container image has been pulled
You can use the docker images command to see a list of all images on your system.

```bash
docker images
```


### Run the container
Great! Let's now run a Docker container based on this image. To do that we are going to use the almighty docker run command.

```bash
docker run -d -p 80:80 docker/getting-started
```

### Verify that the container is running
You can use the docker ps command to see a list of running containers on the system

```bash
docker ps
```

### Catch your http server in action

1. Open any web browser
2. Open incognito mode or private mode
3. Open the URL ``localhost`` or `127.0.0.1`
4. Congratulations!! The index.html that you had created is rendered
5. Close the incognito/private browser window.


### Stop the container

To stop the docker container, you can use the docker kill command

```bash
docker kill [CONTAINER ID]
```

----

Takeaways & learnings from this exercise :

1. Introduction to Dockerfile, the file where you can define a custom image
2. docker build command
3. Creating your own lightweight http server
