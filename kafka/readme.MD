构建镜像 kafka:2.13-2.7.0，执行以下命令
```
docker build -t kafka:2.13-2.7.0 .
```

在虚拟机上创建配置文件目录和logs目录
```
mkdir -p /appdata/server/kafka-cluster/config
mkdir -p /appdata/server/kafka-cluster/kafka-logs
```

运行kafka-docker
```shell script
docker run -d --name=kafka-cluster-1 \
 -p 9092:9092 \
 -v /appdata/server/kafka-cluster/kafka-logs:/tmp/kafka-logs \
 -v /appdata/server/kafka-cluster/config/server.properties:/opt/kafka/config/server.properties \
 kafka:2.13-2.7.0
```