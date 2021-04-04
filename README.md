# Microservice
Sample spring boot microservice implementation with Netflix OSS

# Services 
- Customer service: Lists all the customers
- Order service: Lists all the orders placed by customers
- Discovery Service: Order and Customer service register with discovery service
- Gateway Service: Provides a single interface to outside world

# Netflix OSS
- Eureka: Discovery Service uses the Eureka Server and other services connect with Eureka client.
- Zuul: Gateway service uses Zuul as router and server side load balancing. Zuul uses the service registry provided by our Discovery Service to locate each target service.
- Feign: Used to provide Interservice communication by implementing functions like (de)serialization, fault detection and load distribution. In this example, we make a call to order service from customer service with Feign.
- Ribbon: Provides client side load balancing and integrates with Eureka for service discovery and Hystrix to provide resilience. Ribbon is available as part of Feign.
- Hystrix: Resilience between inter service communication is provided by Hystrix.

# Starting services
- Browse to the service folder, say _customer-service_
- Run command _./gradlew bootRun_

# Eureka Dashboard
<img width="1272" alt="Eureka Dashboard" src="https://user-images.githubusercontent.com/807096/113499695-a8a31f00-9535-11eb-9cb3-d7ad64d2c825.png">

# Sequence of Action
- Upon receiving a GET request to the path /customers/{id}/orders, our Gateway service proxies it to the Customer Service.
- The Customer Service uses a Feign client to send a request to the Order Service to handle the request.
- The Feign client looks up the physical addresses of available Order Service instances in its local registry.
- It uses Ribbon to decide which instance of should receive the request.
- Upon receiving the request, the chosen Order Service instance does its work and sends back a response.
- The Customer Service receives the response and sends its own response back to the Gateway (and back to the client).
