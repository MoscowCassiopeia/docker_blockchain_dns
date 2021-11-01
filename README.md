# docker_blockchain_dns
dns based on blockchain `alfis`  and `emercoin`

Эти докерфайлы и `docker-compose.yml` позволят собрать связку из трех `Docker` контейнеров, которая обеспечит `dns resolve` зон `Emercoin` и `Alfis`.
Связка состоит из трех контейнеров. Первый это контейнер с `Emercoin`, воторой с `Alfis`,третий с `DnsMasq` он нужен для роутинга доменов.
При поступлении запроса к `DnsMasq` он согласно правилам форвардит его либо в контейнер `Emercoin` (только зоны `Emercoin`), либо в контейнер `Alfis`(зоны `Alfis`и клирнет).

Для работы нужно установить `Docker` и `Docker-Compose`. 

Установить всё это дело можно примерно вот таким способом:

```
mkdir ./your_work_dir && \
git clone https://github.com/MoscowCassiopeia/docker_blockchain_dns.git && \
cd ./docker_blockchain_dns && \
docker build -t dnsmasq:scratch ./dnsmasq && \
docker build -t emercoin:archlinux ./emercoin && \
docker build -t alfis:archlinux ./alfis && \
docker-compose up -d
```
После этого у вас на всех интерфейсах локальной машины будет открыт порт 53 через который можно резольвить зоны БЧ Emercoin, Alfis и обычные доменные имена интерета,
которые будут пересылаться через Alfis --> DoH --> Default Upstream Server

Если вы будете менять имена `images` при сборке образов то не забудьте поменять их и в файле `docker-compose.yml` 
