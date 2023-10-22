# SciService Authentication and Routing Documentation

## Overview
The provided classes pertain to a Spring Cloud Gateway service that uses JWT (JSON Web Token) for authentication and secures certain routes while allowing some to be openly accessible.

## Components

### 1. AuthenticationFilter
This filter is responsible for authenticating the requests based on JWT.

#### Key Responsibilities:
- Check if the route needs to be secured by using the `RouteValidator`.
- Validate if the Authorization header is present in the request.
- Validate the JWT using the `JwtUtil`.
- If the JWT is valid, extract the username from the token and set it as `X-Username` header in the request.
- Allow valid requests to proceed and block invalid requests.

#### Dependencies:
- `RouteValidator`: Determines if a route requires authentication.
- `JwtUtil`: Utility to validate and extract information from the JWT.

### 2. RouteValidator
This component is responsible for determining whether a given route requires authentication.

#### Key Responsibilities:
- Define a list of openly accessible API endpoints.
- Check if the current request's route is present in the list of open endpoints.

#### Openly Accessible API Endpoints:
- `/auth/register`
- `/auth/token`
- `/eureka`

## Payload Definitions

### HttpHeaders.AUTHORIZATION
The request header that is expected to contain the JWT for authentication. The expected format of this header is: `Bearer {token}`.

### X-Username
This is a custom header set by the `AuthenticationFilter` after validating the JWT. It contains the username extracted from the token.

## Notes:
1. **Error Handling**: In case of missing or invalid JWTs, a runtime exception is thrown. It might be useful to handle these exceptions in a more user-friendly manner, potentially sending a specific HTTP status code and a descriptive error message.
2. **Logging**: System prints are used for logging purposes in the `AuthenticationFilter`. Transitioning to a logging framework like SLF4J/Logback can provide more flexibility and better logging management.

## Recommendations for Improvement:
1. Incorporate a proper logging framework.
2. Handle exceptions in a more graceful manner by providing meaningful HTTP responses.
3. Consider externalizing the list of open API endpoints, making it more configurable.