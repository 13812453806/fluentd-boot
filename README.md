# fluentd-boot

通过fluentd将SpringBoot应用的日志发送到Elastic Search。

Elastic Search 的配置在 docker-compose 文件中。 

## 用法

### 1. 启动 fluentd + elastic search + kibana

```
docker-compose up -d
```

在浏览器中打开`http://localhost:5601`可以看到Kibana dashboard的页面。

### 2. 执行 ./gradlew bootRun

这步会启动SpringBoot的应用，该应用会随机的产生日志信息，并将日志发送到Elastic Search。
可以在Kibana中查看日志内容。

通过在环境变量中配置`FLUENTD_HOST` 和 `FLUENTD_PORT`，可以指定docker容器的地址和端口，如果没有指定，日志会默认发送到localhost，在此种情况下，SpringBoot应用和docker容器应该是运行在同一台机器上。

## 原理

应用通过一个logback appender将日志发送到fluentd。

logback的配置在 `src/main/resources/logback.xml` 中。
