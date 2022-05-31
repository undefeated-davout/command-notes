# Docker

## LOGIN

```bash
# コンテナにログイン
docker exec -it node-docker.app /bin/bash --login

# コンテナにログインし、指定のディレクトリで開く
docker exec -it -w /share/fuootus node-docker.app /bin/bash --login
```

## REMOVE

```bash
# 未使用オブジェクト削除
docker system prune
# 未使用オブジェクト削除（ボリューム含む）
docker system prune --volumes -f
# 稼働中のコンテナを停止
docker ps -q | xargs docker stop
# 停止したコンテナを削除
docker ps -aq | xargs docker rm -f
# 停止したコンテナとそのイメージを削除
docker ps -aq | xargs docker rm -f && docker images -aq | xargs docker rmi -f
# 停止したコンテナとそのイメージ、キャッシュを削除
docker ps -aq | xargs docker rm -f && docker images -aq | xargs docker rmi -f && docker system prune --volumes -f
# 停止したコンテナとそのイメージ、キャッシュ、ボリューム共有設定を削除
docker ps -aq | xargs docker rm -f && docker images -aq | xargs docker rmi -f && docker system prune --volumes -f && docker volume ls -q | xargs docker volume rm
```

## RUN

```bash
# Ubuntu
docker run --rm -it ubuntu:20.04 bash

# Python
docker run --rm -it python:3.9.6 bash
# Python（ボリューム共有）
docker run --rm -v "$(pwd)":/opt/app/src -w /opt/app/src -it python:3.10.2-bullseye bash --login

# Go（ボリューム共有）
docker run --rm -v "$(pwd)":/go/src -w /go/src -it golang:1.17.6-bullseye bash

# JupyterNotebook
docker run --rm -v "$(pwd)":/home/jovyan/work -w /home/jovyan/work -p 8888:8888 jupyter/scipy-notebook

# Node
docker run --rm -v "$(pwd)":/opt/app/src -w /opt/app/src -it node:16.13.2-bullseye bash --login
```

## LOG

```bash
# 直前に起動したコンテナのログを表示する（日本語対応）
docker logs $(docker ps -ql) -f

# docker-composeログを表示する（日本語非対応）
docker-compose logs -f
```
