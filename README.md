Docker Tinyproxy
================

[![Stars](https://img.shields.io/docker/stars/diwu1989/tinyproxy-docker.svg)](https://hub.docker.com/r/diwu1989/tinyproxy-docker/)
[![Pulls](https://img.shields.io/docker/pulls/diwu1989/tinyproxy-docker.svg)](https://hub.docker.com/r/diwu1989/tinyproxy-docker/)
[![License](https://img.shields.io/github/license/diwu1989/tinyproxy-docker.svg)](https://github.com/diwu1989/tinyproxy-docker/blob/master/LICENSE)

> Docker implementation of [TinyProxy](https://github.com/tinyproxy/tinyproxy)

## Getting started

For testing purpose, you may want to change the **tinyproxy.conf** and switch the **LogLevel** value to **Info** and comment the Allow line.

```
# build docker image
docker build -t tinyproxy .

# run container in background
docker run -d --name tinyproxy -p 8888:8888 tinyproxy

# proxy request via the running container
http_proxy=127.0.0.1:8888 https_proxy=127.0.0.1:8888 curl https://www.google.com -v

# or
curl -x 127.0.0.1:8888 curl https://www.google.com -v

# or proxy all requests from linux based containers
docker run -t -i \
  -e "http_proxy=tinyproxy:8888" \
  -e "https_proxy=tinyproxy:8888" \
  --link tinyproxy \
  travix/toolbox \
  curl https://www.google.com
```

## Custom Tinyproxy configuration

```
docker run -t -i \
  -v $(pwd)/tinyxproxy.conf:/etc/tinyproxy.conf
  -p 8888:8888 \
  tinyproxy
```

## License

MIT © [Travix International](http://travix.com)
