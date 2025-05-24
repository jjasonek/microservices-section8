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


### shut down accounts (port 8080):
POS Thttp://localhost:8080/actuator/shutdown
{
"message": "Shutting down, bye..."
}

2025-05-23T13:15:58.268+02:00  INFO 3532 --- [accounts] [      Thread-10] o.s.c.n.e.s.EurekaServiceRegistry        : Unregistering application ACCOUNTS with eureka with status DOWN
2025-05-23T13:15:58.269+02:00  INFO 3532 --- [accounts] [      Thread-10] com.netflix.discovery.DiscoveryClient    : Saw local status change event StatusChangeEvent [timestamp=1747998958269, current=DOWN, previous=UP]
2025-05-23T13:15:58.270+02:00  INFO 3532 --- [accounts] [foReplicator-%d] com.netflix.discovery.DiscoveryClient    : DiscoveryClient_ACCOUNTS/localhost:accounts:8080: registering service...
2025-05-23T13:15:58.330+02:00  INFO 3532 --- [accounts] [      Thread-10] o.s.b.w.e.tomcat.GracefulShutdown        : Commencing graceful shutdown. Waiting for active requests to complete
2025-05-23T13:15:58.369+02:00  INFO 3532 --- [accounts] [tomcat-shutdown] o.s.b.w.e.tomcat.GracefulShutdown        : Graceful shutdown complete
2025-05-23T13:15:58.371+02:00  INFO 3532 --- [accounts] [foReplicator-%d] com.netflix.discovery.DiscoveryClient    : DiscoveryClient_ACCOUNTS/localhost:accounts:8080 - registration status: 204
2025-05-23T13:15:58.426+02:00  INFO 3532 --- [accounts] [      Thread-10] j.LocalContainerEntityManagerFactoryBean : Closing JPA EntityManagerFactory for persistence unit 'default'
2025-05-23T13:15:58.523+02:00  WARN 3532 --- [accounts] [      Thread-10] o.s.b.f.support.DisposableBeanAdapter    : Invocation of destroy method failed on bean with name 'inMemoryDatabaseShutdownExecutor': org.h2.jdbc.JdbcSQLNonTransientConnectionException: Databáze byla již ukončena (pro deaktivaci automatického ukončení při zastavení virtuálního stroje přidejte parametr ";DB_CLOSE_ON_EXIT=FALSE" do URL databáze)
Database is already closed (to disable automatic closing at VM shutdown, add ";DB_CLOSE_ON_EXIT=FALSE" to the db URL) [90121-232]
2025-05-23T13:15:58.526+02:00  INFO 3532 --- [accounts] [      Thread-10] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Shutdown initiated...
2025-05-23T13:15:58.535+02:00  INFO 3532 --- [accounts] [      Thread-10] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Shutdown completed.
2025-05-23T13:15:58.540+02:00  INFO 3532 --- [accounts] [      Thread-10] com.netflix.discovery.DiscoveryClient    : Shutting down DiscoveryClient ...
2025-05-23T13:16:01.551+02:00  INFO 3532 --- [accounts] [      Thread-10] com.netflix.discovery.DiscoveryClient    : Unregistering ...
2025-05-23T13:16:01.571+02:00  INFO 3532 --- [accounts] [      Thread-10] com.netflix.discovery.DiscoveryClient    : DiscoveryClient_ACCOUNTS/localhost:accounts:8080 - deregister  status: 200
2025-05-23T13:16:01.572+02:00  INFO 3532 --- [accounts] [      Thread-10] com.netflix.discovery.DiscoveryClient    : Completed shut down of DiscoveryClient
Disconnected from the target VM, address: '127.0.0.1:63025', transport: 'socket'


### After some testing it looks like 
management:
    endpoint:
        shutdown:
            enabled: true
**is needed**, whereas
endpoints:
    shutdown:
        enabled: true
**is not needed**.


## Linking services together using the OpenFeign Client

### Request:
GET http://localhost:8080/api/fetchCustomerDetails?mobileNumber=4354437687
### Response:
{
    "name": "Madan Reddy",
    "email": "tutor@eazybytes",
    "mobileNumber": "4354437687",
    "accountsDto": {
        "accountNumber": 1024671414,
        "accountType": "Savings",
        "branchAddress": "123 Main Street, New York"
    },
    "loansDto": {
        "mobileNumber": "4354437687",
        "loanNumber": "100468436788",
        "loanType": "Home Loan",
        "totalLoan": 100000,
        "amountPaid": 0,
        "outstandingAmount": 100000
    },
    "cardsDto": {
        "mobileNumber": "4354437687",
        "cardNumber": "100500947447",
        "cardType": "Credit Card",
        "totalLimit": 100000,
        "amountUsed": 0,
        "availableAmount": 100000
    }
}


## Generating docker images

docker logout
docker login -u jjasonek

cd accounts
mvn compile jib:dockerBuild
cd ..\cards
mvn compile jib:dockerBuild
cd ..\configserver\
mvn compile jib:dockerBuild
cd ..\eurekaserver\
mvn compile jib:dockerBuild
cd ..\loans\
mvn compile jib:dockerBuild

### Delete old images
docker rmi f70a201defbf cc115ee4240a 8db789bb4aa8 2089b8cc8fd2

### push images
docker image push docker.io/jjasonek/accounts:s8
docker image push docker.io/jjasonek/configserver:s8
docker image push docker.io/jjasonek/eurekaserver:s8
docker image push docker.io/jjasonek/loans:s8
docker image push docker.io/jjasonek/cards:s8

### run the images
docker compose up -d
