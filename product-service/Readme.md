# Product Service

The Product Service provides a set of endpoints for managing products.

## API Endpoints

### Retrieve All Products

**Endpoint**: `/product/`

**Method**: `GET`

**Response**:

Returns a list of all available products in the system.

### Retrieve Product by ID

**Endpoint**: `/product/{id}`

**Method**: `GET`

**Path Variable**:

- `id`: The ID of the product.

**Response**:

Returns a product with the given ID if found.

### Create Product

**Endpoint**: `/product/`

**Method**: `POST`

**Headers**:

- `x-username`: The username performing the operation.

**Request Body**:

Product details in JSON format.

**Response**:

- If the username is `admin`, the product is saved and a success message is returned.
- Otherwise, a 403 Forbidden status code is returned.

### Update Product

**Endpoint**: `/product/{id}`

**Method**: `PUT`

**Path Variable**:

- `id`: The ID of the product.

**Headers**:

- `x-username`: The username performing the operation.

**Request Body**:

Updated product details in JSON format.

**Response**:

- If the username is `admin` and the version of the product matches, the product is updated and a success message is returned.
- If the version does not match, a 409 Conflict status with an "Optimistic locking conflict" message is returned.
- If the username is not `admin`, a 403 Forbidden status code is returned.

## Implementation Details

- The service uses Spring's `@RestController` for creating the API endpoints.
- Jackson's `ObjectMapper` is used to handle JSON serialization and deserialization.
- `ProductService` manages the business logic related to products.
- Product updates utilize optimistic locking to ensure data integrity. This means when two or more requests try to modify the same product version, only one will succeed, and others will receive a conflict error.

## Dependencies

- Spring Web for creating the API endpoints.
- Jackson for handling JSON serialization and deserialization.
