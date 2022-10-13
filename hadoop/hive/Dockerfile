CMD ["bash"]
RUN set -eux; apt-get update; apt-get install -y --no-install-recommends ca-certificates p11-kit ; rm -rf /var/lib/apt/lists/*
ENV JAVA_HOME=/usr/local/openjdk-8
RUN { echo '#/bin/sh'; echo 'echo "$JAVA_HOME"'; } > /usr/local/bin/docker-java-home  \
	&& chmod +x /usr/local/bin/docker-java-home  \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ] # backwards compatibility
ENV PATH=/usr/local/openjdk-8/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LANG=C.UTF-8
ENV JAVA_VERSION=8u332
RUN set -eux; arch="$(dpkg --print-architecture)"; case "$arch" in 'amd64') downloadUrl='https://github.com/AdoptOpenJDK/openjdk8-upstream-binaries/releases/download/jdk8u332-b09/OpenJDK8U-jdk_x64_linux_8u332b09.tar.gz'; ;; 'arm64') downloadUrl='https://github.com/AdoptOpenJDK/openjdk8-upstream-binaries/releases/download/jdk8u332-b09/OpenJDK8U-jdk_aarch64_linux_8u332b09.tar.gz'; ;; *) echo >&2 "error: unsupported architecture: '$arch'"; exit 1 ;; esac; savedAptMark="$(apt-mark showmanual)"; apt-get update; apt-get install -y --no-install-recommends dirmngr gnupg wget ; rm -rf /var/lib/apt/lists/*; wget --progress=dot:giga -O openjdk.tgz "$downloadUrl"; wget --progress=dot:giga -O openjdk.tgz.asc "$downloadUrl.sign"; export GNUPGHOME="$(mktemp -d)"; gpg --batch --keyserver keyserver.ubuntu.com --recv-keys EAC843EBD3EFDB98CC772FADA5CD6035332FA671; gpg --batch --keyserver keyserver.ubuntu.com --keyserver-options no-self-sigs-only --recv-keys CA5F11C6CE22644D42C6AC4492EF8D39DC13168F; gpg --batch --list-sigs --keyid-format 0xLONG CA5F11C6CE22644D42C6AC4492EF8D39DC13168F | tee /dev/stderr | grep '0xA5CD6035332FA671' | grep 'Andrew Haley'; gpg --batch --verify openjdk.tgz.asc openjdk.tgz; gpgconf --kill all; rm -rf "$GNUPGHOME"; mkdir -p "$JAVA_HOME"; tar --extract --file openjdk.tgz --directory "$JAVA_HOME" --strip-components 1 --no-same-owner ; rm openjdk.tgz*; apt-mark auto '.*' > /dev/null; [ -z "$savedAptMark" ] || apt-mark manual $savedAptMark > /dev/null; apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; { echo '#!/usr/bin/env bash'; echo 'set -Eeuo pipefail'; echo 'trust extract --overwrite --format=java-cacerts --filter=ca-anchors --purpose=server-auth "$JAVA_HOME/jre/lib/security/cacerts"'; } > /etc/ca-certificates/update.d/docker-openjdk; chmod +x /etc/ca-certificates/update.d/docker-openjdk; /etc/ca-certificates/update.d/docker-openjdk; find "$JAVA_HOME/lib" -name '*.so' -exec dirname '{}' ';' | sort -u > /etc/ld.so.conf.d/docker-openjdk.conf; ldconfig; javac -version; java -version
ENV HADOOP_HOME=/opt/hadoop HIVE_HOME=/opt/hive
RUN echo 'deb http://mirrors.aliyun.com/debian/ bullseye main non-free contrib' > /etc/apt/sources.list  \
	&& echo 'deb http://mirrors.aliyun.com/debian-security/ bullseye-security main' >> /etc/apt/sources.list  \
	&& echo 'deb http://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib' >> /etc/apt/sources.list  \
	&& echo 'deb http://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib' >> /etc/apt/sources.list  \
	&& apt update  \
	&& apt install net-tools procps -y  \
	&& rm -rf /var/lib/apt/lists/*
#第一个hive 第二个hadoop
ADD file:e7722dfa6a2e3ffa95f10acd285968ac705ef21939ea540da04425904f4051f0 in /opt
ADD file:5d32b2933ebdfbe4dd6e81da22567f971413f17c97c5f02542fe699555956c25 in /opt
ADD mysql-connector-java-5.1.49.jar in /opt/hive/lib
ADD hudi-common-0.8.0-NAZA-1.jar in /opt/hive/lib
ADD hudi-hadoop-mr-0.8.0-NAZA-1.jar in /opt/hive/lib
ADD hudi-hadoop-mr-bundle-0.8.0-NAZA-1.jar in /opt/hive/lib


WORKDIR /opt/hive
