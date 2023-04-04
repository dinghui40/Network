FROM alpine:latest

ARG version=0.48.0

COPY ./start /usr/local/bin/start

RUN wget https://github.com/fatedier/frp/releases/download/v${version}/frp_${version}_linux_amd64.tar.gz \
    && tar -zvxf frp_${version}_linux_amd64.tar.gz \
    && cp -r frp_${version}_linux_amd64 frp \
    && cd frp \
    && chmod +x /usr/local/bin/start \
    && mv /frp/frps /usr/local/bin/ \
    && rm -rf frpc* LICENSE \
    && rm -rf /frp_${version}_linux_amd64*

COPY ./frps.ini /frp/frps.ini

COPY 404.html /frp/404.html

WORKDIR /frp

#客户端连接端口
EXPOSE 7000

#frp Web端
EXPOSE 7500

CMD /usr/local/bin/start