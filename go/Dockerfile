FROM golang:1.23 AS builder

WORKDIR /usr/src/app

COPY go.mod ./
RUN go mod download && go mod verify

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build  -v -ldflags="-s -w" -trimpath -o /usr/local/bin/app ./... 

FROM scratch

WORKDIR /app

COPY --from=builder /usr/local/bin/app .

EXPOSE 8080

CMD ["./app"]
