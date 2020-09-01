# s6

## 示例

**alpine/debian**

```docker
FROM --platform=$TARGETPLATFORM alpine

RUN --mount=type=bind,from=khs1994/s6:2.0.0.1,source=/,target=/tmp/s6 \
    set -x \
    && tar -zxvf /tmp/s6/s6-overlay.tar.gz -C / \
    && ln -s /init /s6-init

ENTRYPOINT ["/s6-init"]
```

对于 `/bin` 是一个软链接的系统，则按照如下方法使用。

```bash
$ ls -la /
lrwxrwxrwx   1 root root    7 Jul 29 01:29 bin -> usr/bin
```

**ubuntu/centos/fedora**

```docker
FROM --platform=$TARGETPLATFORM ubuntu

RUN --mount=type=bind,from=khs1994/s6:2.0.0.1,source=/,target=/tmp/s6 \
    set -x \
    && tar -zxvf /tmp/s6/s6-overlay.tar.gz -C / --exclude='./bin' \
    && tar -zxvf /tmp/s6/s6-overlay.tar.gz -C /usr ./bin \
    && ln -s /init /s6-init

ENTRYPOINT ["/s6-init"]
```
