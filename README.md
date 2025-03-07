# order-processing-system

## Overview
This is a scalable, event-driven **Order Processing System** built with **Node.js, Express, MongoDB, Redis, and AWS**. The system enables users to place orders, processes them asynchronously, and sends notifications upon completion.

## Features
- **User Authentication** with JWT & Refresh Tokens
- **Order Management** (Create & Retrieve Orders)
- **Inventory Check** (Stock Validation Before Order Confirmation)
- **Asynchronous Processing** using AWS SQS
- **Caching** with Redis for quick order retrieval
- **Email Notifications** with AWS SES

## Tech Stack
- **Backend**: Node.js, Express.js
- **Database**: MongoDB
- **Authentication**: JWT (JSON Web Token)
- **Caching**: Redis
- **Queue Processing**: AWS SQS
- **Email Service**: AWS SES

## Folder Structure
```
ORDER PROCESSING SYSTEM
│── node_modules/
│── src/
│   ├── config/
│   │   ├── awsConfig.js
│   │   ├── redisConfig.js
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── orderController.js
│   │   ├── processOrder.js
│   ├── middlewares/
│   │   ├── authMiddleware.js
│   ├── models/
│   │   ├── inventoryModel.js
│   │   ├── orderModel.js
│   │   ├── userModel.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── orderRoutes.js
│   ├── validations/
│   │   ├── validations.js
│   ├── index.js
│── .env
│── package.json
│── package-lock.json
```

## Setup & Installation
### 1. Clone the repository
```sh
git clone <repository-url>
cd order-processing-system
```

### 2. Install dependencies
```sh
npm install
```

### 3. Set up environment variables
Create a `.env` file in the root directory and add the following details:
```ini
MONGO_URI=<your-mongodb-uri>
JWT_SECRET=<your-jwt-secret>
REDIS_HOST=127.0.0.1
REDIS_PORT=6379
AWS_ACCESS_KEY=<your-aws-access-key>
AWS_SECRET_KEY=<your-aws-secret-key>
AWS_REGION=<your-aws-region>
SQS_QUEUE_URL=<your-sqs-queue-url>
SES_EMAIL=<your-verified-ses-email>
```

### 4. Start the server
```sh
cd src
npm start
```

### 5. Run the Order Processing Worker
In a separate terminal, run:
```sh
node src/controllers/processOrder.js
```

## API Endpoints
### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | User Registration |
| POST | `/api/auth/login` | User Login |
| POST | `/api/auth/refresh` | Token Refresh |

### Orders
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/orders` | Create Order |
| GET | `/api/orders/:id` | Get Order Details |

## Notes
1. **AWS Credentials**: You need to attach your own `AWS_ACCESS_KEY`, `AWS_SECRET_KEY`, `AWS_REGION`, `SQS_QUEUE_URL`, and `SES_EMAIL` for AWS services.
2. **MongoDB**: The MongoDB connection uses a pre-configured cluster but can be replaced with your own.
3. **Redis**: Runs locally and can be accessed via `redis-cli`.
4. **Token Refreshing**: To get a new access token, send a request to `/api/auth/refresh` with the refresh token.
5. **Worker Process**: The `processOrder.js` file must be run in a separate terminal to fetch orders synchronously from SQS.

## Testing with Postman
- The **Postman collection** has been provided in the email thread for testing.
- Import the collection into **Postman** and test the API routes.

## License
This project is for **assessment purposes only** and not intended for production use.
