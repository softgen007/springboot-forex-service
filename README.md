# Forex Service
Forex Service: A microservices demo application using Spring Boot.

## Overview
This application consists of mainly two microservices - 1. currency-conversion-service 2. currency-exchange-service. currency-exchange-service provides exchange rate. currency-conversion-service calls currency-exchange-service to get the exchange rate and then returns the total value of input amount in converted currency to client application. 

### Microservices features demoed in the application
This project demonstrates the following basics of microservices:
- How to implement microservices using Spring Cloud.
- How to establish communication between microservices.
- How to enable load balancing in microservices.
- How to implement Eureka Naming Server.
- How to add distributed tracing with Spring Cloud Sleuth and Zipkin.

### Expectations
- You should have basic understanding of Spring Boot.
- You should have basic understanding of Eclipse, Maven & Tomcat.
- You should have basic understanding of Git.

## How to Run
- Download the zip or clone the Git repository.
- Unzip the zip file (if you downloaded one)
- Open Eclipse 
   - File -> Import -> Existing Maven Project -> Navigate to the folder where you unzipped the zip
   - Select all projects
- Download Zipkin server. Visit https://zipkin.io/pages/quickstart.html for more details.
- Command to run Zipkin: java -jar zipkin-server-2.5.2-exec.jar
- Start the services from eclipse in following order:
   - netflix-eureka-naming-server
   - currency-exchange-service
   - currency-conversion-service
   - netflix-zuul-api-gateway-server
 - Start second instance of currency-exchange-service
   - Go to Eclipse Run Configurations
   - Create a copy currency-exchange-service run configuration
   - Change the port of second instance by providing this VM Argument: -Dserver.port=8001
   - Click Apply and Run
   
## How to Test
- Launch Eureka Naming server in browser: http://localhost:8761. You can see all services running there.
- Launch H2 Database console to verify current excahnge rate records
   - Launch H2 Database Console in browser: http://localhost:8000/h2-console
   - Enter following details:
      - Saved Settings: Generic H2 (Embedded)
      - Setting Name: Generic H2 (Embedded)
      - Driver Class: org.h2.Driver
      - JDBC URL: jdbc:h2:mem:testdb
      - Username: sa
      - Password: (keep it blank)
- Launch Zipkin Server: http://localhost:9411/zipkin
- Hit currency-conversion-service via API gateway. E.g. http://localhost:8765/currency-conversion-service/currency-converter-feign/from/USD/to/INR/quantity/10
   - In output verify totalCalculatedAmount and port values.
   - Every time you refresh/hit currency-conversion-service you may see different port number which implies that responses are 
   coming from different instances of currency-exchange-service
- Go to Zipkin server, you can see the requsets flow traces in zipkin server. Make sure to select service name, select sorting option and click Find Traces button.
 
