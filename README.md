
# Next.js API with Authentication and Webhook

This project demonstrates a Next.js API implementation with user management, JWT authentication, and a webhook endpoint. It's designed as a starting point for building secure and scalable APIs using Next.js.

## Features

- User Management API
  - Create new users
  - Fetch all users
  - Fetch a single user by ID
- JWT Authentication
- Webhook endpoint with signature verification
- Simple JSON file-based data storage

## Prerequisites

- Node.js (v14 or later)
- npm or yarn

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. Install dependencies:

   ```bash
   npm install
   # or
   yarn install
   ```

3. Set up environment variables:

   Create a `.env.local` file in the root directory and add the following:

   ```
   JWT_SECRET=your-jwt-secret
   WEBHOOK_SECRET=your-webhook-secret
   ```

   Replace `your-jwt-secret` and `your-webhook-secret` with secure random strings.

4. Run the development server:

   ```bash
   npm run dev
   # or
   yarn dev
   ```

The server will start on `http://localhost:3000`.

## API Endpoints

### User Management

- **POST /api/users**: Create a new user
  - Body: `{ "name": "John Doe", "email": "john@example.com", "password": "password123" }`
  - Returns: JWT token

- **GET /api/users**: Fetch all users (requires authentication)

- **GET /api/users/:id**: Fetch a single user by ID (requires authentication)

### Webhook

- **POST /api/webhook**: Webhook endpoint
  - Requires `x-webhook-signature` header for verification

## Testing the API

You can use cURL or any API testing tool like Postman to test the endpoints. Here are some example cURL commands:

1. Create a user:

   ```bash
   curl -X POST http://localhost:3000/api/users \
   -H "Content-Type: application/json" \
   -d '{"name":"John Doe","email":"john@example.com","password":"password123"}'
   ```

2. Fetch all users (replace `<YOUR_TOKEN>` with the JWT token received from user creation):

   ```bash
   curl http://localhost:3000/api/users \
   -H "Authorization: Bearer <YOUR_TOKEN>"
   ```

3. Fetch a single user (replace `<USER_ID>` and `<YOUR_TOKEN>`):

   ```bash
   curl http://localhost:3000/api/users/<USER_ID> \
   -H "Authorization: Bearer <YOUR_TOKEN>"
   ```

4. Test webhook (replace `<GENERATED_SIGNATURE>` with a valid HMAC SHA-256 signature):

   ```bash
   curl -X POST http://localhost:3000/api/webhook \
   -H "Content-Type: application/json" \
   -H "x-webhook-signature: <GENERATED_SIGNATURE>" \
   -d '{"eventType":"test","data":{"message":"Hello, webhook!"}}'
   ```

## Security Considerations

- This project uses a simple JSON file for data storage. In a production environment, you should use a proper database system.
- Ensure to keep your JWT_SECRET and WEBHOOK_SECRET secure and never commit them to version control.
- The current implementation stores passwords in plain text. In a real-world application, always hash passwords before storing them.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License.

