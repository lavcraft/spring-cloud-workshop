# Spring cloud workshop

## Samples

 * five microservices that are called each other
 * eureka server (or you may use consul with small changes) (http://{you_docker_machine_host}:8761/)
 * gateway server with hystrix dashboard (see http://{you_docker_machine_host}:9000/hystrix/) and service routing
 * ops server with open zipking tracing through sleuth (http://{you_docker_machine_host}:9411/)
 * turbine server for colleting hystrix data from all services through rabbit-mq

## Build, run, rebuild

build app:   `./gradlew build`

build image: `./gradlew dockerBuild`

run all:     `./run up -d`

rebuild:     `./rebuild-{sub-project-name}`

rebuild script redeploy app automatically

example:

    ./gradlew build && ./run up -d && ./rebuild-rent-service

## Step0

* do nothing. Just launch `./rebuild-all` `./run up`

## Step1

* add @EnableDiscoveryClient to rent-service
* add eureka client configuration to it
* fix docker-compose.yml with env, links and dependsOn properties

* then launch again and test /rent method

## Step2

* add gateway

## Step 3

* add @EnableHystrix annotation to rent-service
* add dependency with hystrix-starter
* add `feign.hystrix.enabled` to application.yml

* then rebuild and check hystrix-dashboard at [gateway-server](http://localhost:9000/hystrix)

## Step 4

* add `hystrix-stream` starter and `stream-rabbit` to `rent-service`
* add rabbitmq endpoint (spring properties) to rent-service in `docker-compose.yml`

## Step 5

* add `sleuth` starter, `zipkin` starter and `sleuth-zipkin` start to `rent-service`
* add zipkin base url to rent-service in `docker-compose.yml`