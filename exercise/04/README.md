# Java HTTP Server
## Understanding Image layers & caching


### Checkout the source code

Checkout the source code from [this](https://github.com/sridhar09/docker-java-http) repository

### Create a new docker image from multi stage file

Create a new docker image with this command 

```bash
docker build -t [your-dockerhub-id]/java-http-server -f Dockerfile.multi .
```

### Check the size of the image

```
docker images
```

See how the size of the image is significantly lower

---

Takeaways & learnings from this exercise :

1. Docker Multi stage build
2. Size reduction