# Stage 1

FROM golang:alpine as builder
RUN mkdir -p /build
ENV BUILDPATH /go/src/github.com/ghsbhatia/msgbox
RUN mkdir -p $BUILDPATH
WORKDIR $BUILDPATH
ADD . $BUILDPATH
RUN go build -o /build/useradminsvc cmd/useradmin/useradminservice.go

# Stage 2

FROM alpine
RUN adduser -S -D -H -h /app appuser
USER appuser
COPY --from=builder /build/useradminsvc /app/
WORKDIR /app
ENV MYSQLDB_URL root@tcp(127.0.0.1:3306)/msgbox
EXPOSE 6060
CMD ["./useradminsvc"]
