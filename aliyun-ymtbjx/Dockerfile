FROM python:3

COPY file/* /root/

RUN sh /root/requirements.sh \
    && mkdir -p /usr/local/aliyun/ \
    && mv /root/yuming.py /usr/local/aliyun/ \
    && touch /usr/local/aliyun/yuming.log \
    #&& sed -i s@/deb.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list \
    && apt-get update \
    && apt-get -y install cron \
    && apt-get -y install vim \
    && service cron start \
    && echo '*/10 * * * * sh /root/cron.sh' | crontab
    
CMD [ "sh", "/root/start.sh" ]
