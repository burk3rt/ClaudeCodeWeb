# ClaudeCodeWeb
This is a tryout of claude code web

## User Service API Mock Server

This project includes a mock server implementation for the User Service API using [Prism](https://stoplight.io/open-source/prism) by Stoplight.

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Installation

Install dependencies:

```bash
npm install
```

### Running the Mock Server

The mock server uses the `OpenAPI.yaml` specification to generate responses based on the examples defined in the OpenAPI file.

#### Basic Usage

Start the mock server on the default port (4010):

```bash
npm run mock
```

The server will be available at `http://localhost:4010`

#### Custom Port

Start the mock server on port 3000:

```bash
npm run mock:port
```

#### Dynamic Mode

Generate dynamic responses (beyond just examples):

```bash
npm run mock:dynamic
```

In dynamic mode, Prism will generate realistic mock data based on your schema definitions, not just returning the static examples.

#### Validation Mode

Enable request validation (validates incoming requests against the OpenAPI spec):

```bash
npm run mock:validate
```

### API Endpoints

Once the mock server is running, you can test the following endpoints:

- **POST** `/api/user` - Create a new user
- **GET** `/api/user/{user_uuid}` - Get user profile
- **PATCH** `/api/user/{user_uuid}` - Update user details
- **DELETE** `/api/user/{user_uuid}` - Delete user
- **GET** `/api/user/{user_uuid}/permissions/{course_uuid}` - Get user permissions for a course
- **GET** `/api/user/{user_uuid}/activity` - Get user activity log

### Example Requests

Create a user:
```bash
curl -X POST http://localhost:4010/api/user \
  -H "Content-Type: application/json" \
  -H "X-Api-Version: 0.1" \
  -d '{
    "username": "jdoe",
    "first_name": "John",
    "last_name": "Doe",
    "email": "john@example.com",
    "role": "student"
  }'
```

Get a user profile:
```bash
curl -X GET http://localhost:4010/api/user/550e8400-e29b-41d4-a716-446655440000 \
  -H "X-Api-Version: 0.1"
```

### Notes

- The mock server is **stateless** - created/updated data is not persisted between requests
- Responses are generated from the examples in `OpenAPI.yaml`
- Use dynamic mode (`npm run mock:dynamic`) for varied responses based on schema definitions
- All responses include the `X-User-Pseudo-ID` header as defined in the OpenAPI spec

### Documentation

For more information about Prism, visit the [official documentation](https://docs.stoplight.io/docs/prism/).
