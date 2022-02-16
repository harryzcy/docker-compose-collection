FROM golang:1.17-alpine as builder

WORKDIR /go/src/github.com/hacdias
RUN apk --update add ca-certificates git

RUN git clone https://github.com/hacdias/webdav.git
WORKDIR /go/src/github.com/hacdias/webdav
RUN go mod download
RUN CGO_ENABLED=0 go build -o webdav

FROM scratch
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt

EXPOSE 80
COPY --from=builder /go/src/github.com/hacdias/webdav/webdav /webdav

ENTRYPOINT [ "/webdav" ]
