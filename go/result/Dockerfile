FROM golang:1.21

WORKDIR /

COPY go.mod go.sum ./
RUN go mod download

COPY *.go ./
COPY static/ ./static/

RUN GOOS=linux go build -o /main

EXPOSE 8080

CMD ["/main"]
