---
title: Docker 使用笔记
date: 2020/12/24 21:35:23
tags: Config
categories: Config
---

> `could not find an available, non-overlapping IPv4 address pool among the defaults to assign to the network`

- 使用 `docker network ls` 查看network数量
- `docker network prune` 关闭未使用的网络


```yml
FROM node:10-alpine

RUN npm config set registry https://registry.npm.taobao.org
ADD ./package.json /apps/
WORKDIR /apps
RUN npm install

COPY ./ /apps
RUN npm run release

FROM nginx:alpine
COPY --from=0 /apps/dist/ /usr/share/nginx/html/
```

```sh
# 删除所有 <none> image 
docker rmi `docker images | grep  "<none>" | awk '{print $3}'`
```


```sh
# 删除所有 <none> image 
docker rmi `docker images | grep  "months ago" | awk '{print $3}'`

docker stop `docker ps | grep  "weeks ago" | awk '{print $1}'`   

# 删除半年前的image
docker image prune -a --force --filter "until=4320h" 

# 这个命令会删除所有关闭的容器以及dangling镜像。
docker system prune

# 磁盘占用情况
docker system df
```