# 🔧 MapMitra Backend

A robust Node.js/Express backend API for the MapMitra smart campus navigation system, providing authentication, user management, and core business logic for the platform.

## 📋 Overview

The backend serves as the central API layer for MapMitra, handling user authentication via Google OAuth, user management with role-based access control, and integration with the ride-matching and routing services. Built with modern Node.js technologies and following RESTful API principles.

## ✨ Features

### 🔐 Authentication & Authorization
- **Google OAuth 2.0**: Secure authentication via Passport.js
- **JWT Tokens**: Access and refresh token management
- **Session Management**: Express sessions with secure cookies
- **Role-based Access**: Multi-tier user permissions (student, visitor, driver, admin)

### 👥 User Management
- **User Registration**: Account creation with email/phone validation
- **Profile Management**: User profile updates and preferences
- **Multi-role Support**: Different access levels for various user types
- **Data Validation**: Input sanitization and validation

### 🛡️ Security Features
- **CORS Protection**: Configurable cross-origin resource sharing
- **Rate Limiting**: API request throttling (if implemented)
- **Input Sanitization**: Protection against injection attacks
- **Secure Headers**: Security-focused HTTP headers

### 🗄️ Data Management
- **MongoDB Integration**: NoSQL database with Mongoose ODM
- **Data Pagination**: Efficient large dataset handling
- **Schema Validation**: Mongoose schema-based data validation
- **Database Indexing**: Optimized query performance

## 🛠️ Tech Stack

### Core Technologies
![Node.js](https://img.shields.io/badge/-Node.js-339933?logo=node.js&logoColor=white&style=flat-square)
![Express.js](https://img.shields.io/badge/-Express.js-000000?logo=express&logoColor=white&style=flat-square)
![JavaScript](https://img.shields.io/badge/-JavaScript-F7DF1E?logo=javascript&logoColor=black&style=flat-square)

### Database & ODM
![MongoDB](https://img.shields.io/badge/-MongoDB-47A248?logo=mongodb&logoColor=white&style=flat-square)
![Mongoose](https://img.shields.io/badge/-Mongoose-880000?logo=mongoose&logoColor=white&style=flat-square)

### Authentication & Security
![Passport.js](https://img.shields.io/badge/-Passport.js-34E27A?logo=passport&logoColor=white&style=flat-square)
![JWT](https://img.shields.io/badge/-JWT-000000?logo=json-web-tokens&logoColor=white&style=flat-square)
![bcrypt](https://img.shields.io/badge/-bcrypt-4A90E2?style=flat-square)

## 📦 Dependencies

### Core Dependencies
```json
{
  "express": "^4.21.1",
  "mongoose": "^8.8.1",
  "bcrypt": "^5.1.1",
  "jsonwebtoken": "^9.0.2",
  "dotenv": "^16.4.5"
}
```

### Authentication & Session Management
```json
{
  "passport": "^0.7.0",
  "passport-google-oauth20": "^2.0.0",
  "express-session": "^1.18.1",
  "cookie-parser": "^1.4.7"
}
```

### Security & Middleware
```json
{
  "cors": "^2.8.5",
  "mongoose-aggregate-paginate-v2": "^1.1.2"
}
```

### Development Dependencies
```json
{
  "nodemon": "^3.1.7",
  "prettier": "^3.3.3"
}
```

## 🚀 Quick Start

### Prerequisites
- **Node.js**: Version 18.x or higher
- **npm**: Version 8.x or higher
- **MongoDB**: Local installation or MongoDB Atlas account
- **Google Cloud Console**: For OAuth credentials

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yxshee/mapmitra.git
   cd mapmitra/backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```
   
   Configure the following variables:
   ```env
   # Database
   MONGODB_URI=mongodb://localhost:27017/mapmitra
   # or for MongoDB Atlas:
   # MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/mapmitra

   # JWT Secrets
   ACCESS_TOKEN_SECRET=your_access_token_secret_here
   ACCESS_TOKEN_EXPIRY=15m
   REFRESH_TOKEN_SECRET=your_refresh_token_secret_here
   REFRESH_TOKEN_EXPIRY=7d

   # Session Secret
   SESSION_SECRET=your_session_secret_here

   # Google OAuth
   GOOGLE_CLIENT_ID=your_google_client_id
   GOOGLE_CLIENT_SECRET=your_google_client_secret

   # CORS
   CORS_ORIGIN=http://localhost:5173

   # Server
   PORT=3000
   NODE_ENV=development
   ```

4. **Start the development server**
   ```bash
   npm run dev
   ```

   The server will be available at `http://localhost:3000`

### Production Build

```bash
# Start in production mode
npm start
```

## 📁 Project Structure

```
backend/
├── src/
│   ├── config/                # Configuration files
│   │   └── passportConfig.js  # Passport.js OAuth configuration
│   ├── controllers/           # Request handlers
│   │   ├── auth.controllers.js    # Authentication logic
│   │   └── user.controllers.js    # User management logic
│   ├── db/                    # Database configuration
│   │   └── index.js           # MongoDB connection setup
│   ├── middlewares/           # Express middlewares
│   │   ├── auth.middlewares.js        # Authentication middleware
│   │   └── authorizeRoles.middlewares.js  # Role-based authorization
│   ├── models/               # Mongoose schemas
│   │   └── User.models.js     # User data model
│   ├── routes/               # API route definitions
│   │   ├── auth.routes.js     # Authentication routes
│   │   └── user.routes.js     # User management routes
│   ├── utils/                # Utility functions
│   │   ├── ApiError.js        # Custom error handling
│   │   ├── ApiResponse.js     # Standardized API responses
│   │   └── AsyncHandler.js    # Async error wrapper
│   ├── app.js                # Express app configuration
│   └── index.js              # Server entry point
├── package.json              # Project dependencies and scripts
└── .env.example             # Environment variables template
```

## 🌐 API Endpoints

### Authentication Routes (`/api/auth`)

#### User Registration
```http
POST /api/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "+1234567890",
  "role": "student"
}
```

#### User Login
```http
POST /api/auth/login
Content-Type: application/json

{
  "phone": "+1234567890",
  "password": "securePassword123"
}
```

#### Google OAuth
```http
GET /api/auth/google
GET /api/auth/google/callback
```

#### Token Refresh
```http
POST /api/auth/refresh-token
Content-Type: application/json

{
  "refreshToken": "your_refresh_token_here"
}
```

#### Logout
```http
POST /api/auth/logout
Authorization: Bearer your_access_token_here
```

### User Management Routes (`/api/user`)

#### Get User Profile
```http
GET /api/user/profile
Authorization: Bearer your_access_token_here
```

#### Update User Profile
```http
PATCH /api/user/profile
Authorization: Bearer your_access_token_here
Content-Type: application/json

{
  "name": "Updated Name",
  "email": "updated@example.com"
}
```

#### Get All Users (Admin only)
```http
GET /api/user/all
Authorization: Bearer admin_access_token_here
```

## 🗄️ Database Schema

### User Model
```javascript
{
  googleId: {
    type: String,
    unique: true,
    sparse: true
  },
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    unique: true,
    sparse: true
  },
  phone: {
    type: String,
    required: true,
    unique: true
  },
  role: {
    type: String,
    enum: ["student", "visitor", "driver", "admin"],
    required: true
  },
  refreshToken: {
    type: String
  },
  createdAt: Date,
  updatedAt: Date
}
```

### Indexes
```javascript
// Composite indexes for optimized queries
{ phone: 1 }           // Unique index for login
{ email: 1 }           // Unique index for OAuth
{ googleId: 1 }        // Unique index for Google OAuth
{ role: 1 }            // Index for role-based queries
```

## 🔐 Authentication Flow

### JWT Token Management
```javascript
// Access Token (15 minutes)
{
  _id: "user_id",
  phone: "+1234567890",
  role: "student",
  iat: 1640995200,
  exp: 1640996100
}

// Refresh Token (7 days)
{
  _id: "user_id",
  iat: 1640995200,
  exp: 1641600000
}
```

### Google OAuth Flow
1. User clicks "Login with Google"
2. Redirected to Google OAuth consent screen
3. Google redirects to `/api/auth/google/callback`
4. Server validates OAuth response
5. User profile created/updated in database
6. JWT tokens generated and returned
7. Client stores tokens for API access

### Role-based Authorization
```javascript
// Middleware usage examples
router.get('/admin-only', 
  authenticateToken, 
  authorizeRoles(['admin']), 
  controller
);

router.get('/driver-or-admin', 
  authenticateToken, 
  authorizeRoles(['driver', 'admin']), 
  controller
);
```

## 🛡️ Security Features

### Password Security
- **bcrypt**: Password hashing with salt rounds
- **No plain text storage**: Passwords never stored in plain text
- **Secure comparison**: Timing-safe password verification

### CORS Configuration
```javascript
app.use(cors({
  origin: process.env.CORS_ORIGIN,
  credentials: true,
  methods: ['GET', 'POST', 'PUT', 'DELETE', 'PATCH'],
  allowedHeaders: ['Content-Type', 'Authorization']
}));
```

### Session Security
```javascript
app.use(session({
  secret: process.env.SESSION_SECRET,
  resave: false,
  saveUninitialized: false,
  cookie: { 
    secure: process.env.NODE_ENV === 'production',
    httpOnly: true,
    maxAge: 24 * 60 * 60 * 1000 // 24 hours
  }
}));
```

## 🔧 Configuration

### Database Connection
```javascript
// db/index.js
const connectDB = async () => {
  try {
    const connectionInstance = await mongoose.connect(
      process.env.MONGODB_URI,
      {
        useNewUrlParser: true,
        useUnifiedTopology: true,
      }
    );
    console.log(`MongoDB Connected: ${connectionInstance.connection.host}`);
  } catch (error) {
    console.error("MongoDB connection error:", error);
    process.exit(1);
  }
};
```

### Passport Configuration
```javascript
// config/passportConfig.js
passport.use(new GoogleStrategy({
  clientID: process.env.GOOGLE_CLIENT_ID,
  clientSecret: process.env.GOOGLE_CLIENT_SECRET,
  callbackURL: "/api/auth/google/callback"
}, async (accessToken, refreshToken, profile, done) => {
  // OAuth profile processing
}));
```

## 🧪 Development

### Development Scripts
```bash
# Start development server with auto-reload
npm run dev

# Start production server
npm start

# Format code with Prettier
npm run format
```

### Environment Setup
```bash
# Development environment
NODE_ENV=development
PORT=3000

# Production environment
NODE_ENV=production
PORT=5000
```

### Testing (when implemented)
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run tests with coverage
npm run test:coverage
```

## 🚀 Deployment

### Docker Deployment
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY src/ ./src/
COPY . .

EXPOSE 3000

USER node

CMD ["npm", "start"]
```

### Environment Variables for Production
```env
NODE_ENV=production
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/mapmitra
ACCESS_TOKEN_SECRET=production_access_secret
REFRESH_TOKEN_SECRET=production_refresh_secret
SESSION_SECRET=production_session_secret
GOOGLE_CLIENT_ID=production_google_client_id
GOOGLE_CLIENT_SECRET=production_google_client_secret
CORS_ORIGIN=https://yourdomain.com
PORT=3000
```

### Health Check Endpoint
```javascript
// Health check for monitoring
app.get('/health', (req, res) => {
  res.status(200).json({
    status: 'OK',
    timestamp: new Date().toISOString(),
    uptime: process.uptime(),
    environment: process.env.NODE_ENV
  });
});
```

## 🐛 Troubleshooting

### Common Issues

1. **MongoDB Connection Errors**
   ```bash
   # Check MongoDB service status
   sudo systemctl status mongod
   
   # Check connection string format
   # mongodb://localhost:27017/mapmitra
   # mongodb+srv://user:pass@cluster.mongodb.net/mapmitra
   ```

2. **JWT Token Issues**
   ```bash
   # Verify token secrets are set
   echo $ACCESS_TOKEN_SECRET
   echo $REFRESH_TOKEN_SECRET
   
   # Check token expiry times
   # 15m for access tokens
   # 7d for refresh tokens
   ```

3. **Google OAuth Errors**
   ```bash
   # Verify OAuth credentials
   # Check redirect URIs in Google Console
   # Ensure HTTPS in production
   ```

4. **CORS Issues**
   ```bash
   # Check CORS origin configuration
   # Verify frontend URL matches CORS_ORIGIN
   # Enable credentials for authenticated requests
   ```

### Debug Mode
```bash
# Enable debug logging
DEBUG=app:* npm run dev

# MongoDB debug mode
DEBUG=mongoose:* npm run dev
```

## 📊 Performance Optimization

### Database Optimization
- **Indexing**: Strategic index creation for frequent queries
- **Pagination**: Implement pagination for large datasets
- **Connection Pooling**: MongoDB connection pool configuration
- **Query Optimization**: Use aggregation pipelines for complex queries

### Middleware Optimization
- **Compression**: Response compression middleware
- **Caching**: Response caching for static data
- **Rate Limiting**: API rate limiting to prevent abuse

## 🔄 Integration with Other Services

### Quinjet (Ride Matching Service)
```javascript
// API calls to Quinjet service
const quinjertBaseURL = process.env.QUINJET_URL || 'http://localhost:8080';

// Create ride request
POST /api/v1/rides/new
GET  /api/v1/rides/status
```

### Routing Backend
```javascript
// API calls to routing service
const routingBaseURL = process.env.ROUTING_URL || 'http://localhost:5000';

// Get route instructions
POST /route_instructions
```

## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Follow coding standards**
   - Use ES6+ features
   - Follow RESTful API conventions
   - Add JSDoc comments for functions
   - Use async/await for asynchronous operations

4. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
5. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
6. **Open a Pull Request**

### Development Guidelines
- Follow Node.js best practices
- Use proper error handling with try-catch blocks
- Implement input validation for all endpoints
- Write meaningful commit messages
- Update API documentation for new endpoints

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](../LICENSE) file for details.

## 👥 Contributors

- **Ansh Midha** - [@AM0312](https://github.com/AM0312)
- **Leena Gupta** - [@leena153](https://github.com/leena153)
- **Madhur Gaba** - [@madhurgaba2603](https://github.com/madhurgaba2603)
- **Shourya De** - [@shouryade](https://github.com/shouryade)
- **Yash Dogra** - [@yxshee](https://github.com/yxshee)

---

<div align="center">
  <p>Made with ❤️ by TIET Students</p>
  <p>🔧 Powering Smart Campus Navigation! 🚀</p>
</div>
