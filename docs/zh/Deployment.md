# 部署方式

## `Docker`部署

### 部署方式

mrapi 的项目，建议采用 Docker 部署，使用 TAPD 工作流打包 Docker 镜像并推送到 `腾讯云` 上，部署到对应集群里

#### `dockerFile`基础配置

```dockerFile
FROM node:13

# 同步时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

WORKDIR /usr/src/app

COPY ./package.json ./
COPY ./yarn.lock ./

RUN yarn install

COPY . .

ENV ENVIROMENT=production

RUN yarn gen
RUN yarn build

CMD yarn start:prod
# EXPOSE 3001

# CMD ["yarn", "start"]
```
