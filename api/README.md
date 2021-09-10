```
docker build -t go-example .
docker run -it -d -p 8080:8080 go-example

#test
curl localhost:8080/ping
{"message":"pong"}
```
