# dockerExample
* The API directory contains a DockerFile, a simple Web service for the GO language Gin framework.
# Use it
```
cd api
docker build -t go-example .
docker run -it -d -p 8080:8080 $IMAGEID
```
