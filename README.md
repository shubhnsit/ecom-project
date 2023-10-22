# ecommerce-app

# service-registry-app
Acts as a Eureka Service Registry, a vital component in a microservice architecture.
Enables services to register and discover other services.
Provides a visual dashboard to oversee the status of registered services.

![eureka-server](https://github.com/SachinMittal101/ecommerce-app/blob/main/images/eureka-server.png)

# sci-service
SCI stands for Service Connector Interface which is a cloud api-gateway which will parse every request going to order and product service.
This service acts as a Eureka client and is registered on the Service Registry App (Eureka Server).

Focuses on securing routes and validating incoming requests.
Utilizes JWT for token authentication.
Filters requests to check for the presence of a valid authorization token and routes them accordingly.

# auth-service
auth-service will be used to register user in database. It also allows creation of JWT token based on registered users
only.It also exposes one endpoint which will be used to validate token.
This service acts as a Eureka client and is registered on the Service Registry App (Eureka Server).

Manages user authentication and registration.
Offers endpoints for user registration, token generation, and token validation.
Utilizes Spring Security's AuthenticationManager to verify user credentials.

Service Endpoints:
`localhost:8080/auth/register`
`localhost:8080/auth/token`
`localhost:8080/auth/validate`

# order-service
The Order Service is responsible for managing order operations. This service acts as a Eureka client and is registered on the Service Registry App (Eureka Server).
It also interacts with Product service and Payment service via Eureka to fetch product and payemnt details respectively. An EmailTemplate stub is also exposed in this service for sending email to the consumer once order is created.

Service Endpoints:
Create order endpoint: `localhost:8080/order/`
Get order endpoint: `localhost:8080/order/`

# product-service
The Product Service is responsible for managing order operations.This service acts as a Eureka client and is registered on the Service Registry App (Eureka Server).

A central service for handling product-related operations.
Manages operations like adding, updating, retrieving. 

Service Endpoints:
Create Product Endpoint: `localhost:8080/product/`
Get Products: `localhost:8080/product/`

# payment-service
The Payment Service is responsible for processing payment of an order .This service acts as a Eureka client and is registered on the Service Registry App (Eureka Server).

Facilitates the processing of payments.
Accepts payment details and processes the payment.
Includes robust logging for tracking payment processing.

Service Endpoints:
Create Product Endpoint: `localhost:8080/payment/process`
