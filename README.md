# docker_blockchain_dns
dns based on blockchain `alfis`  and `emercoin`



Конфигурационные файлы для сборки образов Docker (докерфайлы/Dockerfile) и конфигурационный файл для запуска и управления контейнерами `docker-compose.yml` позволят собрать связку из трех `Docker` контейнеров,
которая обеспечит разрешение имён в DNS зонах блокчейнов `Emercoin` и `Alfis`. Эти децентрализованные DNS системы используются в том числе
в [Оверлейной сети Yggdrasil](https://ru.wikipedia.org/wiki/Yggdrasil)

Связка состоит из трех контейнеров. Первый это контейнер с `Emercoin`, воторой с `Alfis`,третий с `DnsMasq` он нужен для роутинга доменов.
При поступлении запроса к `DnsMasq` он согласно правилам форвардит его либо в контейнер `Emercoin` (только зоны `Emercoin`), либо в контейнер `Alfis`(зоны `Alfis`и клирнет).
При сборке образов не используется бинарных сборок с моего репозитория. Бинарники скачиваются с репозиториев разработчиков этих БЧ, это можно посмотреть в Dockerfile
соответствующего образа. `DnsMasq` собирается из исходных кодов во время сборки образа.
Для работы нужно установить `Docker` и `Docker-Compose`. 

Собрать контейнеры и запустить их можно следующими командами:

```
mkdir ./your_work_dir && \
cd ./your_work_dir && \
git clone https://github.com/MoscowCassiopeia/docker_blockchain_dns.git && \
cd ./docker_blockchain_dns && \
docker build -t dnsmasq:scratch ./dnsmasq && \
docker build -t emercoin:archlinux ./emercoin && \
docker build -t alfis:archlinux ./alfis && \
docker-compose up -d
```
После запуска контейнеров сразу начнет закачиваться блокчейн Emercoin и Alfis. Это может занять около часа, может и больше. 
После этого у вас на всех интерфейсах локальной машины будет открыт порт 53 через который можно резольвить зоны БЧ Emercoin, Alfis и обычные доменные имена интерета,
которые будут пересылаться через Alfis --> DoH --> Default Upstream Server

Проверить работоспособность можно командой `dig AAAA @127.0.0.1 howto.ygg` для Alfis и `dig @127.0.0.1 rutor.lib` для Emercoin. 

Если вы будете менять имена `images` при сборке образов то не забудьте поменять их и в файле `docker-compose.yml`
