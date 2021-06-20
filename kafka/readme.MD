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
 -p 9999:9999 \
 -v /appdata/server/kafka-cluster/kafka-logs:/tmp/kafka-logs \
 -v /appdata/server/kafka-cluster/config/server.properties:/opt/kafka/config/server.properties \
 -e JMX_PORT=9999 \
 -e KAFKA_HEAP_OPTS="-Xmx1G -Xms1G" \
 kafka:2.13-2.7.0
```

-  -e JMX_PORT=9999 jvm监控端口
-  -e KAFKA_HEAP_OPTS="-Xmx512M -Xms256M" 控制启动内存


对于kafka集群监控开源软件有： kafka manager 现在改名为 CMAK, kafdrop
- 运行 CMAK
```shell script
docker run -d --rm --name=kafka-manager -p9000:9000 -eZK_HOSTS=10.0.0.30:2181  kafkamanager/kafka-manager:3.0.0.4
```
- --rm选项，在容器退出时就能够自动清理容器内部的文件系统。


- 运行 kafdrop
```shell script
docker run -d --rm  --name=kafdrop -p 9001:9000 \
  -e KAFKA_BROKERCONNECT=10.0.0.30:9092,10.0.0.31:9092,10.0.0.32:9092 \
  -e JVM_OPTS="-Xms128M -Xmx128M" \
  -e SERVER_SERVLET_CONTEXTPATH="/" \
  obsidiandynamics/kafdrop
```