FROM golang

WORKDIR /go/src/app
COPY myapp.go /go/src/app/

RUN go mod init gin
RUN go mod edit -require github.com/gin-gonic/gin@latest
RUN go get -u github.com/gin-gonic/gin
EXPOSE 8080

CMD ["go","run","myapp.go"]
