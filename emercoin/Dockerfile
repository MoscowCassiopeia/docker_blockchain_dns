FROM archlinux:latest
LABEL name="Emercoin 0.7.10" version=1
WORKDIR /app
RUN mkdir ./bin && \
    mkdir /srv/emercoin_data && \
    curl -L  https://github.com/emercoin/emercoin/releases/download/v0.7.10emc/emercoin-0.7.10-x86_64-linux-gnu.tar.gz -o emercoin-0.7.10-x86_64-linux-gnu.tar.gz && \
    tar -xvf ./emercoin-0.7.10-x86_64-linux-gnu.tar.gz && \
    mv ./emercoin-0.7.10/bin/{emercoind,emercoin-cli,emercoin-tx} ./bin/ && \
    echo -e 'listen=1\nserver=1\ndaemon=0\nrpcallowip=0.0.0.0/0\nrpcport=6662\nmaxconnections=80\ngen=0\nreservebalance=0\nrpcuser=emcrpc\nrpcpassword=emcpass\nemcdns=1\nemcdnsallowed=$enum|.coin|.emc|.lib|.bazar\nemcdnsport=5335' > ./emercoin.conf && \
    rm -rf ./emercoin-0.7.10 && \
    rm -rf ./emercoin-0.7.10-x86_64-linux-gnu.tar.gz

EXPOSE 6662
EXPOSE 6661
EXPOSE 5335/udp
CMD ["/app/bin/emercoind", "-datadir=/srv/emercoin_data", "-conf=/app/emercoin.conf"]
 
