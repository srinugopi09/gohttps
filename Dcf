############################
# STEP 1 build executable binary
############################
FROM golang:alpine AS builder
# Install git.
# Git is required for fetching the dependencies.
RUN apk update && apk add --no-cache git build-base
# WORKDIR $GOPATH/src/mypackage/myapp/
# COPY . .
# COPY catalog.istioinaction.io.cert.pem   /go/bin
# COPY catalog.istioinaction.io.key.pem  /go/bin
# RUN mkdir /build
# ADD * /build/
#WORKDIR /build
#RUN CGO_ENABLED=0 GOOS=linux go build -a -o golang-memtest .
# RUN  go build -a -o golang-memtest .

WORKDIR /go/app
COPY  * .
RUN set -ex; CGO_ENABLED=0 GOOS=linux GOARCH=amd64; go build -a -o golang-memtest .

# Fetch dependencies.
# Using go get.

# RUN go get -d -v
# # Build the binary.
# RUN CGO_ENABLED=0 GOOS=linux go build -o /go/bin/hello
############################
# STEP 2 build a small image
############################
FROM scratch
# Copy our static executable.
#COPY --from=builder /go/bin/hello /go/bin/hello
COPY --from=builder /go/app/* .
#COPY  --from=builder /go/bin/cata* /go/bin/
# Run the hello binary.
ENTRYPOINT [ "/go/app/golang-memtest" ]
CMD [ "3", "300" ]

#ENTRYPOINT ["echo", "Hello World"]