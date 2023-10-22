# Order Management Service

This service provides endpoints for managing orders for users.

## API Endpoints

### Retrieve Orders by User

**Endpoint**: `/order/`

**Method**: `GET`

**Headers**:

- `x-username`: The username for which the orders need to be retrieved.

**Response**:

Returns a list of orders associated with the provided username.

### Retrieve Order by ID

**Endpoint**: `/order/{id}`

**Method**: `GET`

**Path Variable**:

- `id`: The ID of the order.

**Headers**:

- `x-username`: The username for which the order needs to be retrieved.

**Response**:

Returns an order with the given ID if found.

### Create Order

**Endpoint**: `/order/`

**Method**: `POST`

**Headers**:

- `x-username`: The username for whom the order needs to be created.

**Request Body**:

Order details in JSON format.

**Response**:

Returns a 201 status code if the order is created successfully, otherwise, it will return a 404 status code.

## Implementation Details

- The service uses Spring's `@RestController` for creating the API endpoints.
- All the requests and responses are handled in JSON format using Jackson's `ObjectMapper`.
- The service uses an `OrderService` to handle business logic related to orders.
- All responses are converted to string format using the `ObjectMapper` to maintain consistency.

## Dependencies

- Spring Web for creating the API endpoints.
- Jackson for handling JSON serialization and deserialization.
