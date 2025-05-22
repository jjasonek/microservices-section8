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
