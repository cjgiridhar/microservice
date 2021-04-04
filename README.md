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
