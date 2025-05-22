# Udemy Course Microservices with Spring Boot, Docker, Kubernetes Section8
https://www.udemy.com/course/master-microservices-with-spring-docker-kubernetes/
## spring version: 3.4.5
## Java 21


## Documentation
After adding the library, the swagger page is accessible through address 
http://localhost:8080/swagger-ui/index.html,
http://localhost:8090/swagger-ui/index.html,
http://localhost:9000/swagger-ui/index.html.


## Note: 
### We start on section 6 V2
### And we delete the Spring Cloud Buss and RabbitMQ stuff.


## Eureka Server

### Generete the Eureka Server using https://start.spring.io/
add: 
- Eureka Server
- Config Client
- Spring Boot Actuator

### Start the config server and confirm the eureka properties:
http://localhost:8071/eurekaserver/default

### Start h=the eureka server and confirm the eureka properties:
...
2025-05-22T14:06:48.102+02:00  INFO 24212 --- [eurekaserver] [           main] o.s.c.c.c.ConfigServerConfigDataLoader   : Fetching config from server at : http://localhost:8071
...
2025-05-22T14:06:53.620+02:00  INFO 24212 --- [eurekaserver] [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 8070 (http) with context path '/'
2025-05-22T14:06:53.621+02:00  INFO 24212 --- [eurekaserver] [           main] .s.c.n.e.s.EurekaAutoServiceRegistration : Updating port to 8070
...

http://localhost:8070/ brings up the Eureka dashboard.



## Registering the service to the Eureka Server

### after starting:
...
2025-05-22T19:19:42.441+02:00  INFO 32340 --- [accounts] [  restartedMain] com.netflix.discovery.DiscoveryClient    : Getting all instance registry info from the eureka server
2025-05-22T19:19:43.673+02:00  INFO 32340 --- [accounts] [  restartedMain] com.netflix.discovery.DiscoveryClient    : The response status is 200
2025-05-22T19:19:43.675+02:00  INFO 32340 --- [accounts] [  restartedMain] com.netflix.discovery.DiscoveryClient    : Starting heartbeat executor: renew interval is: 30
2025-05-22T19:19:43.677+02:00  INFO 32340 --- [accounts] [  restartedMain] c.n.discovery.InstanceInfoReplicator     : InstanceInfoReplicator onDemand update allowed rate per min is 4
2025-05-22T19:19:43.679+02:00  INFO 32340 --- [accounts] [  restartedMain] com.netflix.discovery.DiscoveryClient    : Discovery Client initialized at timestamp 1747934383678 with initial instances count: 0
2025-05-22T19:19:43.688+02:00  INFO 32340 --- [accounts] [  restartedMain] o.s.c.n.e.s.EurekaServiceRegistry        : Registering application ACCOUNTS with eureka with status UP
2025-05-22T19:19:43.688+02:00  INFO 32340 --- [accounts] [  restartedMain] com.netflix.discovery.DiscoveryClient    : Saw local status change event StatusChangeEvent [timestamp=1747934383688, current=UP, previous=STARTING]
2025-05-22T19:19:43.690+02:00  INFO 32340 --- [accounts] [foReplicator-%d] com.netflix.discovery.DiscoveryClient    : DiscoveryClient_ACCOUNTS/localhost:accounts:8080: registering service...
2025-05-22T19:19:43.715+02:00  INFO 32340 --- [accounts] [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 8080 (http) with context path '/'
2025-05-22T19:19:43.716+02:00  INFO 32340 --- [accounts] [  restartedMain] .s.c.n.e.s.EurekaAutoServiceRegistration : Updating port to 8080
2025-05-22T19:19:44.179+02:00  INFO 32340 --- [accounts] [foReplicator-%d] com.netflix.discovery.DiscoveryClient    : DiscoveryClient_ACCOUNTS/localhost:accounts:8080 - registration status: 204
...


http://192.168.56.1:8080/actuator/info
{
    "app": {
        "name": "accounts",
        "description": "Eazy Bank Accounts Application",
        "version": "1.0.0"
    }
}
