FROM golang:1.24-alpine AS builder

RUN apk add --no-cache git ca-certificates && update-ca-certificates

WORKDIR /src

COPY . .

RUN go mod tidy

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -mod=mod -o /app/guestbook-api .

FROM alpine:3.20

RUN adduser -D -u 10001 app
WORKDIR /
COPY --from=builder /app/guestbook-api /guestbook-api

USER 10001
EXPOSE 8080
ENTRYPOINT ["/guestbook-api"]
