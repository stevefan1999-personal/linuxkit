FROM linuxkit/alpine:daed76b8f1d28cdeeee215a95b9671c682a405dc AS build

RUN apk add --no-cache go musl-dev
ENV GOPATH=/go PATH=$PATH:/go/bin

COPY cmd/ /go/src/
RUN go-compile.sh /go/src/memlogd
RUN go-compile.sh /go/src/logread
RUN go-compile.sh /go/src/logwrite

FROM scratch
ENTRYPOINT []
CMD []
WORKDIR /
COPY --from=build /go/bin/memlogd usr/bin/memlogd
COPY --from=build /go/bin/logread usr/bin/logread
COPY --from=build /go/bin/logwrite usr/bin/logwrite
# We'll start from init.d
COPY etc/ /etc/