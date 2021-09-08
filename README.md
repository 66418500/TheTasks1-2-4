# docker && ansible tasks
# 1.The Task 4. Docker and a bit of Dev
* The API directory contains a DockerFile, a simple Web service for the GO language Gin framework.
# Use it
```
cd api
docker build -t go-example .
docker run -it -d -p 8080:8080 $IMAGEID

#test
curl localhost:8080/ping
{"message":"pong"}
```

# 2.Task 2. Configuration management

