FROM alpine:latest

ARG version=0.48.0

COPY ./start /usr/local/bin/start

RUN wget https://github.com/fatedier/frp/releases/download/v${version}/frp_${version}_linux_amd64.tar.gz \
    && tar -zvxf frp_${version}_linux_amd64.tar.gz \
    && cp -r frp_${version}_linux_amd64 frp \
    && cd frp \
    && chmod +x /usr/local/bin/start \
    && mv /frp/frpc /usr/local/bin/ \
    && rm -rf frps* LICENSE \
    && rm -rf /frp_${version}_linux_amd64*

COPY ./frpc.ini /frp/frpc.ini

WORKDIR /frp

CMD /usr/local/bin/start