# fluentd-boot

Spring boot logs redirected to Elastic Search via fluentd.

The necessary configuration for Elastic Search is in the docker-compose file. 

## Usage

### 1. Run fluentd + elastic search + kibana

```
docker-compose up -d
```

Then go to `http://${DOCKER_HOST}:5601` (ie, `http://localhost:5601` or your docker machine ip) to see the Kibana dashboard.

Run the application with your IDE. If neither `FLUENTD_HOST` nor `DOCKER_HOST` variable are set,
the logger will try to connect to fluentd on `localhost`.

You can customize the `FLUENTD_HOST` and `FLUENTD_PORT` environment variables to point to your docker-machine IP.

For instance, on my mac, I run the application with `FLUENTD_HOST=192.168.99.100`.

### 2. Run ./gradlew bootRun

This step will start the springboot application, it will produce random logs and put them to the elasticsearch.
We can view the logs in Kibana.

## Principle

Uses a logback appender to redirect logs to fluentd.

See `src/main/resources/logback.xml` for more information.
