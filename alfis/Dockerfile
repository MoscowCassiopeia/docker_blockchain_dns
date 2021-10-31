FROM archlinux:latest
LABEL name="Alfis 0.6.9"
WORKDIR /app
RUN mkdir ./alfis_data && \
    curl -SsL https://github.com/Revertron/Alfis/releases/download/v0.6.9/alfis-linux-amd64-v0.6.9-nogui --output ./alfis-linux-amd64-v0.6.9-nogui && \
    chmod ug+x ./alfis-linux-amd64-v0.6.9-nogui && \
    ./alfis-linux-amd64-v0.6.9-nogui -g > ./alfis.conf && \
    sed -i 's/listen = "127.0.0.1:53"/listen = "0.0.0.0:53"/g' ./alfis.conf
#COPY ./ .
#RUN mkdir /srv/emercoind && cp emercoin.conf /srv/emercoind
#RUN mkdir /srv/emercoin_data
EXPOSE 4244
EXPOSE 53
EXPOSE 53/udp
CMD ["/app/alfis-linux-amd64-v0.6.9-nogui", "-n", "-c", "/app/alfis.conf", "-w", "/app/alfis_data"]
 
