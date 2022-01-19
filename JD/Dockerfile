FROM node:lts-alpine3.12


ARG KEY="-----BEGIN RSA PRIVATE KEY-----\nMIIEpAIBAAKCAQEAx/UD0ksxo0oDfvsjHt2aApsMZljyjs3yFEMB+mLGBZS2pK7v\nWSTWxIIrgbNSfkIZIqqjsWM/22QP5DdZg7ftSsqnPzmYPcu3GMd4gmOaB/V2cu1T\nlI40Y8fQV4r2nyscpsTmq63x1xlwROlcL1wAiShjJQ7DqtMGvEnRES0AEJWIPuur\n6uUWuFHFTy6sslrs8FT6DZrj8bTidbmd5eOpiFTOGaOHdnp4ghzvp7rcLvUYLaGq\nP8Tj655sSqJsrfvu2Fch6++1xvFNIV1bUC3ThB9/Wn4rWpONJZdR1bW8wAy0XQ3v\nqp2MHNENsXzVYkEkAxD5ukGXiYNSV/EqPyx5owIDAQABAoIBAQCGD3R/cqCWDNJp\nOTEjyYkvRAq9N9dv/Q3XndFesQh4x2ro4MxiJPvFBkzrCXI+akx13JghHxy6F807\nwgxG7nKumU4mapPyonlgqKPYL7Uerui6RvmpeOoRF+9MMkQFFR+BhDPvWJDzGQAX\ng6mlqvZE/wnx14NCLXevl4IPFO+dLaOZ3SB3D2oVU5Mh6IOny7c3+JbsDiN3zPUa\nN7tnUQI77Z29Cq+vBceiNSeAV96qF3ai9f9hU5a8J7ZSp6NqUxNKHRt8Lff8z9iv\n5RamkWogrfSgFrtE6MZX3WXMR37WXKt1LhSEM3UvPiN1ViHeE/3yZGf72Y+o8x6R\n0zGskkvhAoGBAPXx49GJKQmnAStlZ0pIrPORxAue/QQselSkAHp6std7m/Ge7XxJ\nP3WQojcFkuMNnzhO7b/09TunoHQFdBNXBeVI147V6yVRUJYdryJ6LzDGM1CyYpfD\nA9LgjDuUks/FbU+IPfct9TB4kAcURFY5AsX3YdZEe/N7EHAwtcouUa3RAoGBANAh\nzqed0kz6NbvRt+yQMd/sEFQ4CrGk7+cWkTaUvEBXVYUHeJcCM21+dWdOvsksrC+v\n7QctS6bAlAQ5PMk6NiJfnCkX0MSTn1HL2UxWodwxrx2ObGnuOJC4CyQuW0/CGt7u\n3r9wvju7ogXsgzwa/84KpR746v7v8Zn9UbdPQokzAoGAckxE/OcKbFLxpzJMC2i0\n/8kZW/E6Uss82sMQ+dq17JCki2i5o44C8OcTjBCKD/0PpsJ/mTsFEQE4/1JdfHNv\n6PuuOdJOopwkoG8RKiuwbLFfvbv5N+BIkaMLaNEGXYq530FI0uvHzAvrm26ex5dd\nI5VxIXvYQvJJVGo+wcQ+71ECgYARKxi+3tfgHaudCJmhW+uhSvm12MGZEb/wUf48\ngFxe+lVFme4qlrXjTFEm6mn2ckbp0Bs/Qk9BPBV5m7cV6kVY5IYfJaXE8WBtAOG1\n2FeVsEt/pqXuvwXPej8BBwnlNF+/D/kz1Xr7tmiREIdqx9deCabBPUs1KFnHmAvL\nkTAt3QKBgQDI+GX5zm0Srj25/IipW1Kaic1nm3jqcVYdBI/B3eSP5ibhBF9V4u/p\n/QzzZ53yLORFpL1teg8oLwAuPYbHXRkwOeOTgQ69YJRDTttXbTxWSfe5p86bb8Nl\nQc1DhL5yV4U+Dh3a1dqQlIueMruJ0r+osmOAubvzvQsyj01WGMkplg==\n-----END RSA PRIVATE KEY-----"

# FROM # 基础镜像 比如node
# MAINTAINER # 镜像是谁写的 姓名+邮箱(MAINTAINER已经被废弃)
# LABEL # 给镜像添加一些元数据
# ARG # 构建参数,与 ENV 作用一至.不过作用域不一样。ARG设置的环境变量仅对Dockerfile内有效,也就是说只有docker build的过程中有效，构建好的镜像内不存在此环境变量
# RUN # 镜像构建时需要运行的命令
# ADD # 添加，比如添加一个tomcat压缩包
# WORKDIR # 镜像的工作目录
# VOLUME # 挂载的目录
# EXPOSE # 指定暴露端口，跟-p一个道理
# RUN # 最终要运行的
# CMD # 指定这个容器启动的时候要运行的命令，只有最后一个会生效，而且可被替代
# ENTRYPOINT # 指定这个容器启动的时候要运行的命令，可以追加命令
# ONBUILD # 当构建一个被继承Dockerfile 这个时候运行ONBUILD指定，触发指令
# COPY # 将文件拷贝到镜像中
# ENV # 构建的时候设置环境变量

# ====================================================================
# Add proxy, using --build-arg "HTTP_PROXY=http://192.168.1.100:7890"

ENV HTTP_PROXY ${HTTP_PROXY}
ENV HTTPS_PROXY ${HTTP_PROXY}
ENV http_proxy ${HTTP_PROXY}
ENV https_proxy ${HTTP_PROXY}

# set -e ： -e这个参数的含义是,当命令发生错误的时候,停止脚本的执行
# set -x ： -x参数的作用是把将要运行的命令用一个+标记之后显示出来
# echo -e ：激活转义字符
# echo -n ：不换行输出
# apk : 软件包管理工具
# mkdir -p ：递归创建目录，即使上级目录不存在，会按目录层级自动创建目录
# git clone -b : 克隆指定的分支 git clone -b 分支名 仓库地址

# 设置环境变量，容器内部使用
ENV DEFAULT_LIST_FILE=crontab_list.sh \
    CUSTOM_LIST_MERGE_TYPE=append \
    COOKIES_LIST=/scripts/logs/cookies.list \
    REPO_URL=https://gitee.com/zkills/dd \
    REPO_BRANCH=master

RUN set -ex \
    && echo $http_proxy \
    && echo -e "https://mirrors.ustc.edu.cn/alpine/latest-stable/main\nhttps://mirrors.ustc.edu.cn/alpine/latest-stable/community" > /etc/apk/repositories \
    && apk update \
    && apk upgrade \
    && apk add --no-cache bash tzdata git moreutils curl jq openssh-client vim \
    && apk add --no-cache make gcc g++ python3-dev pkgconfig pixman-dev cairo-dev pango-dev libjpeg-turbo-dev giflib-dev \
    && rm -rf /var/cache/apk/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && mkdir -p /root/.ssh \
    && echo -e $KEY > /root/.ssh/id_rsa \
    && chmod 600 /root/.ssh/id_rsa \
    && ssh-keyscan gitee.com > /root/.ssh/known_hosts \
    && git clone -b $REPO_BRANCH $REPO_URL /scripts \
    && cd /scripts \
    && mkdir logs \
    && npm config set registry https://registry.npm.taobao.org \
    && npm install \
    && cp /scripts/docker/docker_entrypoint.sh /usr/local/bin \
    && chmod +x /usr/local/bin/docker_entrypoint.sh \
    && echo "alias ll='ls -l'" >> /root/.bashrc \
    && source /etc/profile

#Add pip install mirror:

RUN echo "[global] \
    index-url = https://mirrors.aliyun.com/pypi/simple \
    trusted-host = mirrors.aliyun.com \
    timeout = 120 \
    " > /etc/pip.conf
# ====================================================================
# RUN pip install --upgrade pip 
# ====================================================================
ENV HTTP_PROXY ""
ENV HTTPS_PROXY ""
ENV http_proxy ""
ENV https_proxy ""
# ====================================================================

WORKDIR /scripts

ENTRYPOINT ["docker_entrypoint.sh"]

# alpine版本内嵌的是BusyBox，使用alpine的crontab实际就是使用BusyBox的crond服务
CMD [ "crond" ]
