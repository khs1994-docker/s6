# s6

## 示例

**Alpine**

```docker
FROM --platform=$TARGETPLATFORM alpine

RUN --mount=type=bind,from=khs1994/s6:2.0.0.1,source=/,target=/tmp/s6 \
    set -x \
    && tar -zxvf /tmp/s6/s6-overlay.tar.gz -C / \
    && ln -s /init /s6-init

ENTRYPOINT ["/s6-init"]
```

**Ubuntu**

```docker
FROM --platform=$TARGETPLATFORM ubuntu

RUN --mount=type=bind,from=khs1994/s6:2.0.0.1,source=/,target=/tmp/s6 \
    set -x \
    && tar -zxvf /tmp/s6/s6-overlay.tar.gz -C / --exclude='./bin' \
    && tar -zxvf /tmp/s6/s6-overlay.tar.gz -C /usr ./bin \
    && ln -s /init /s6-init

ENTRYPOINT ["/s6-init"]
```
