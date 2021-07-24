## 1 docker 创建redis服务 

####  使用官方 REDIS 镜像
```shell script
docker run --name redis -p 6379:6379 -d redis:6
```

***

#### 使用自定义配置启动 REDIS 镜像

- 使用 Dockerfile 构建自定义镜像
将redis配置文件 redis.conf 放在同一目录
```shell script
FROM redis
COPY redis.conf /usr/local/etc/redis/redis.conf
CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]
```

- 使用 `docker run` 命令启动
```shell script
docker run -v /myredis/conf/redis.conf:/usr/local/etc/redis/redis.conf --name redis -p 6379:6379 -d redis:6
```

