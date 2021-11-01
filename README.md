# docker_blockchain_dns
dns based on blockchain alfis  and emercoin
Эти докерфайлы и docker-compose.yml позволят собрать связку из трех Docker контейнеров, которая обеспечит dns resolve через Emercoin и Alfis.
Для работы нужно установить Docker и Docker-Compose. 
Установить всё это дело можно примерно вот таким способом:
```
mkdir ./your_work_dir && \
docker build -t dnsmasq:scratch ./dnsmasq && \
docker build -t emercoin:archlinux ./emercoin && \
docker build -t alfis:archlinux ./alfis && \
docker-compose up -d
```
