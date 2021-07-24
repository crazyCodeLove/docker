## 创建 NACOS 3实例集群
- 服务器1，IP="10.0.0.30"
```shell script
docker run -d \
-e MODE=cluster \
-e NACOS_APPLICATION_PORT=19001 \
-e NACOS_SERVER_IP="10.0.0.30" \
-e NACOS_SERVERS=10.0.0.30:19001,10.0.0.31:19001,10.0.0.32:19001 \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=10.0.0.30 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=root \
-e MYSQL_SERVICE_DB_NAME=nacos \
-e MYSQL_SERVICE_DB_PARAM="characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useSSL=false&serverTimezone=GMT%2B8" \
-p 19001:19001 \
--name nacos1 \
nacos/nacos-server:1.4.2
```

- 服务器2，IP="10.0.0.31"
```shell script
docker run -d \
-e MODE=cluster \
-e NACOS_APPLICATION_PORT=19001 \
-e NACOS_SERVER_IP="10.0.0.31" \
-e NACOS_SERVERS=10.0.0.30:19001,10.0.0.31:19001,10.0.0.32:19001 \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=10.0.0.30 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=root \
-e MYSQL_SERVICE_DB_NAME=nacos \
-e MYSQL_SERVICE_DB_PARAM="characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useSSL=false&serverTimezone=GMT%2B8" \
-p 19001:19001 \
--name nacos2 \
nacos/nacos-server:1.4.2
```

- 服务器3，IP="10.0.0.32"
```shell script
docker run -d \
-e MODE=cluster \
-e NACOS_APPLICATION_PORT=19001 \
-e NACOS_SERVER_IP="10.0.0.32" \
-e NACOS_SERVERS=10.0.0.30:19001,10.0.0.31:19001,10.0.0.32:19001 \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=10.0.0.30 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=root \
-e MYSQL_SERVICE_DB_NAME=nacos \
-e MYSQL_SERVICE_DB_PARAM="characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useSSL=false&serverTimezone=GMT%2B8" \
-p 19001:19001 \
--name nacos3 \
nacos/nacos-server:1.4.2
```