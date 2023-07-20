# docker
# docker

### 镜像源加速

> Alpine

~~~dockerfile
ARG APK_MIRROR=mirrors.aliyun.com
RUN sed -i "s/dl-cdn.alpinelinux.org/${APK_MIRROR}/g" /etc/apk/repositories
~~~

> CentOS/RedHat/AliOS

- 阿里镜像官方地址 http://mirrors.aliyun.com/

> Debian

~~~dockerfile
ARG APT_MIRROR=mirrors.aliyun.com
RUN sed -ie "s/deb http:\/\/\(.*\).debian.org/deb http:\/\/${APT_MIRROR}/g" /etc/apt/sources.list
~~~

> Ubuntu

~~~dockerfile
ARG APT_MIRROR=mirrors.aliyun.com
RUN sed -ie "s/deb http:\/\/\(.*\).ubuntu.com/deb http:\/\/${APT_MIRROR}/g" /etc/apt/sources.list
~~~

> Python Application

~~~dockerfile
ARG PIP_INDEX_URL=https://mirrors.aliyun.com/pypi/simple/
RUN pip config set global.index-url ${PIP_INDEX_URL} 
~~~

### 镜像体积优化

> Alpine - apk

- `apk add` with `--no-cache`

~~~dockerfile
RUN apk add --no-cache \
    bash \
    vim
~~~

> CentOS/RedHat/AliOS - yum

- `yum install` with `yum clean all`

~~~dockerfile
RUN yum install -y \
    curl \
    && yum clean --enablerepo=* all
~~~

> Debian/Ubuntu - apt

- `apt-get` install with `--no-install-recommends`
- `rm -rf /var/lib/apt/lists/* /var/lib/apt/lists/* /tmp/* /var/tmp/*`

~~~dockerfile
RUN apt-get update  \
	&& apt-get install -curl --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
~~~

> Python - pip

- `pip install` with `--no-cache-dir`

~~~dockerfile
RUN pip --no-cache-dir install pandas
~~~
