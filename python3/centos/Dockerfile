FROM centos

COPY requirements.txt /
RUN yum install python38 which -y  && \
    yum install wkhtmltox-0.12.6-1.centos8.x86_64.rpm -y && \
    yum clean all && \
    pip3 install -r /requirements.txt
    
COPY getHttpsDeadline.py /
COPY Songti.ttc /usr/share/fonts
CMD python3 /getHttpsDeadline.py
