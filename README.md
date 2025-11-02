# Social Media Application

A full-stack social media platform built with Node.js, TypeScript, and GraphQL. This application provides real-time chat functionality, post management, friend requests, comments, and more.

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Database Models](#-database-models)
- [Contributing](#-contributing)
- [License](#-license)

## 🚀 Features

- **User Authentication & Authorization**: Secure JWT-based authentication with token revocation support
- **Real-time Chat**: WebSocket-based chat functionality using Socket.IO Gateway
- **Post Management**: Create, read, update, and delete posts with image upload support
- **Comments System**: Multi-level commenting on posts
- **Friend Requests**: Send and manage friend connections
- **GraphQL API**: Query and mutation support for users and posts
- **File Upload**: Cloudinary integration for media storage
- **Email Notifications**: Automated email service with custom templates
- **AWS S3 Integration**: Cloud storage configuration for scalable file management

## 🛠 Tech Stack

### Backend
- **Runtime**: Node.js with TypeScript
- **Database**: MongoDB with Mongoose ODM
- **API**: REST API + GraphQL
- **Real-time**: Socket.IO for WebSocket connections
- **Authentication**: JWT (JSON Web Tokens)
- **File Upload**: Multer with Cloudinary
- **Cloud Storage**: AWS S3
- **Email Service**: Nodemailer
- **Validation**: Custom validation middleware

### Frontend
- **HTML5 / CSS3 / JavaScript**
- Basic client interface for testing

## 📁 Project Structure

```
SocialMediaApp/
├── src/
│   ├── DB/
│   │   ├── connectionDB.ts          # Database connection setup
│   │   ├── model/                   # Mongoose schemas
│   │   │   ├── user.model.ts
│   │   │   ├── post.model.ts
│   │   │   ├── comment.model.ts
│   │   │   ├── chat.model.ts
│   │   │   ├── friendRequest.model.ts
│   │   │   └── revokeToken.model.ts
│   │   └── repositories/            # Data access layer
│   │       ├── db.repository.ts
│   │       ├── user.repository.ts
│   │       ├── post.repository.ts
│   │       ├── comment.repository.ts
│   │       ├── chat.repository.ts
│   │       ├── friendRequest.repository.ts
│   │       └── revokeToken.repository.ts
│   ├── middleware/
│   │   ├── Authentication.ts        # JWT authentication
│   │   ├── authorization.ts         # Role-based access control
│   │   ├── multer.cloud.ts         # File upload handler
│   │   └── validation.ts           # Request validation
│   ├── modules/
│   │   ├── users/                  # User management
│   │   │   ├── user.controller.ts
│   │   │   ├── user.service.ts
│   │   │   ├── user.validation.ts
│   │   │   └── graphql/
│   │   ├── post/                   # Post management
│   │   │   ├── post.controller.ts
│   │   │   ├── post.service.ts
│   │   │   ├── post.validation.ts
│   │   │   └── graphQl/
│   │   ├── comment/                # Comment management
│   │   │   ├── comment.controller.ts
│   │   │   ├── comment.service.ts
│   │   │   └── comment.validation.ts
│   │   ├── chat/                   # Real-time chat
│   │   │   ├── chat.controller.ts
│   │   │   ├── chat.service.ts
│   │   │   ├── chat.validation.ts
│   │   │   ├── chat.event.ts
│   │   │   └── chat.gatewat.ts
│   │   ├── gateway/                # WebSocket gateway
│   │   │   ├── gateway.ts
│   │   │   └── gateway.interface.ts
│   │   └── graphQl/                # GraphQL schema
│   │       └── schema.gql.ts
│   ├── service/
│   │   ├── sendEmail.ts            # Email service
│   │   └── email.temp.ts           # Email templates
│   ├── utils/
│   │   ├── classError.ts           # Custom error classes
│   │   ├── event.ts                # Event emitter utilities
│   │   ├── generalRules.ts         # Validation rules
│   │   ├── hash.ts                 # Password hashing
│   │   ├── request.types.ts        # TypeScript type definitions
│   │   ├── s3.config.ts            # AWS S3 configuration
│   │   └── token.ts                # JWT utilities
│   ├── app.controller.ts           # Main application controller
│   └── index.ts                    # Application entry point
├── FE/                             # Frontend client
│   ├── index.html
│   ├── index.js
│   └── package.json
├── config/
│   └── .env                        # Environment variables
├── .gitignore
├── package.json
├── tsconfig.json
└── SocialMediaApp API.json         # API documentation
```

## 🔧 Installation

### Prerequisites

- Node.js (v14 or higher)
- MongoDB (v4.4 or higher)
- npm or yarn
- AWS Account (for S3)
- Cloudinary Account (for image uploads)

### Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd SocialMediaApp
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the `config/` directory:
   ```env
   # Server Configuration
   PORT=3000
   NODE_ENV=development

   # Database
   MONGODB_URI=mongodb://localhost:27017/socialmedia

   # JWT
   JWT_SECRET=your_jwt_secret_key
   JWT_EXPIRES_IN=7d
   REFRESH_TOKEN_SECRET=your_refresh_token_secret

   # Cloudinary
   CLOUD_NAME=your_cloudinary_name
   API_KEY=your_cloudinary_api_key
   API_SECRET=your_cloudinary_api_secret

   # AWS S3
   AWS_ACCESS_KEY_ID=your_aws_access_key
   AWS_SECRET_ACCESS_KEY=your_aws_secret_key
   AWS_REGION=your_aws_region
   AWS_BUCKET_NAME=your_bucket_name

   # Email Service
   EMAIL_HOST=smtp.gmail.com
   EMAIL_PORT=587
   EMAIL_USER=your_email@gmail.com
   EMAIL_PASSWORD=your_email_password
   ```

4. **Build the project**
   ```bash
   npm run build
   ```

5. **Start the server**
   ```bash
   # Development
   npm run dev

   # Production
   npm start
   ```

## 🎮 Usage

### Starting the Application

```bash
# Development mode with hot-reload
npm run dev

# Production mode
npm run build
npm start
```

### Access Points

- **REST API**: `http://localhost:3000/api`
- **GraphQL Playground**: `http://localhost:3000/graphql`
- **WebSocket**: `ws://localhost:3000`
- **Frontend**: `http://localhost:3000` (if served)

## 📚 API Documentation

The API documentation is available in [SocialMediaApp API.json](SocialMediaApp%20API.json). Import this file into Postman or any API client for detailed endpoint information.

### Main Endpoints

#### Authentication
- `POST /api/users/register` - Register new user
- `POST /api/users/login` - User login
- `POST /api/users/refresh-token` - Refresh access token
- `POST /api/users/logout` - User logout

#### Posts
- `GET /api/posts` - Get all posts
- `POST /api/posts` - Create new post
- `GET /api/posts/:id` - Get post by ID
- `PUT /api/posts/:id` - Update post
- `DELETE /api/posts/:id` - Delete post

#### Comments
- `GET /api/comments/:postId` - Get comments for a post
- `POST /api/comments` - Create comment
- `PUT /api/comments/:id` - Update comment
- `DELETE /api/comments/:id` - Delete comment

#### Chat
- WebSocket events handled through Socket.IO Gateway
- Real-time message sending and receiving
- Online/offline status tracking

### GraphQL Schema

Access the GraphQL playground to explore:
- User queries and mutations
- Post queries and mutations
- Custom field resolvers

## 🗄 Database Models

### User Model
- Authentication and profile information
- Friend connections
- Post and comment relationships

### Post Model
- Content and media
- Author reference
- Like and comment tracking

### Comment Model
- Nested comment support
- User and post references

### Chat Model
- Message content
- Sender and receiver references
- Timestamps

### Friend Request Model
- Sender and receiver
- Request status (pending, accepted, rejected)

### Revoke Token Model
- Blacklisted JWT tokens
- Expiration tracking

## 🏗 Architecture

The application follows a **layered architecture**:

1. **Controller Layer**: Handles HTTP requests and responses
2. **Service Layer**: Contains business logic
3. **Repository Layer**: Data access and database operations
4. **Model Layer**: Database schemas and validation
5. **Middleware Layer**: Authentication, authorization, validation
6. **Utils Layer**: Helper functions and utilities

## 🔐 Security Features

- JWT-based authentication with refresh tokens
- Token revocation mechanism
- Password hashing using bcrypt
- Role-based authorization
- Input validation and sanitization
- Secure file upload with type checking
- Environment variable protection

## 🧪 Testing

```bash
# Run tests (if configured)
npm test

# Run tests with coverage
npm run test:coverage
```

## 🚀 Deployment

### Build for Production

```bash
npm run build
```

The compiled JavaScript will be in the `dist/` folder.

### Environment Setup

Ensure all environment variables are properly configured in your production environment.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 👥 Authors

-  Shehab El-Dein Ashraf🧑‍💻

---
