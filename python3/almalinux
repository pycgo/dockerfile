# 默认python3
FROM almalinux:9.0

COPY requirements.txt /
RUN dnf install python-devel -y  && \
    dnf clean all && \
    pip3 install -r /requirements.txt
