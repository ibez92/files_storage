FROM golang:1.19-bullseye AS builder

WORKDIR /app

COPY go.mod ./

RUN go mod download

COPY ./ ./

RUN mkdir /build \
  && CGO_ENABLED=0 go build -ldflags="-s -w" -o /build ./cmd/app/

FROM debian:bullseye

COPY --from=builder /build/app /usr/local/bin/

CMD ["app"]
