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
# Python docker起動
docker run --rm --name python -it python:3.9.6 /bin/bash
# Python docker起動（ボリューム共有）
docker run --rm -v "$(PWD)":/opt/app/src -w /opt/app/src --name python -it python:3.10.2-bullseye /bin/bash --login

# Go docker起動（ボリューム共有）
docker run --rm -v "$(PWD)":/go/src -w /go/src --name go -it golang:1.17.6-bullseye /bin/bash

# JupyterNotebook起動
docker run --rm -v "$(PWD)":/home/jovyan/work -w /home/jovyan/work -p 8888:8888 --name jupyter jupyter/scipy-notebook

# Node docker起動
docker run --rm -v "$(PWD)":/opt/app/src -w /opt/app/src --name node -it node:16.13.2-bullseye /bin/bash --login
```

## LOG

```bash
# 直前に起動したコンテナのログを表示する（日本語対応）
docker logs $(docker ps -ql) -f

# docker-composeログを表示する（日本語非対応）
docker-compose logs -f
```
