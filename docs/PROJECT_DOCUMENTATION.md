# 🗺️ MapMitra - Complete Project Documentation

## 📚 Table of Contents
1. [Project Overview](#project-overview)
2. [System Architecture](#system-architecture)
3. [Technology Stack](#technology-stack)
4. [Project Structure](#project-structure)
5. [Core Components](#core-components)
6. [Data Flow](#data-flow)
7. [Setup & Installation](#setup--installation)
8. [How It Works](#how-it-works)
9. [API Documentation](#api-documentation)
10. [Deployment](#deployment)

---

## 🎯 Project Overview

**MapMitra** is a comprehensive campus navigation system designed for Thapar Institute of Engineering & Technology (TIET). The platform provides smart navigation, real-time e-rickshaw tracking, and personalized recommendations to help students and visitors navigate the campus effortlessly.

### Key Features
- 🧭 **Landmark-Based Navigation**: Get directions using campus monuments and familiar landmarks
- 🚌 **Real-Time E-Rickshaw Tracking**: Track e-rickshaw locations with 90% ETA accuracy
- 🎯 **Personalized Recommendations**: Custom route suggestions based on user preferences
- 👥 **User Authentication**: Secure login system with Google OAuth integration
- 🛠️ **Admin Dashboard**: Comprehensive driver management and route control

---

## 🏗️ System Architecture

MapMitra follows a **microservices architecture** with four main services:

```
┌─────────────────────────────────────────────────────────────┐
│                        Client Layer                          │
│  ┌────────────────────────────────────────────────────────┐ │
│  │        React Frontend (Vite + TailwindCSS)             │ │
│  │  - Map Interface (Leaflet/MapLibre)                    │ │
│  │  - User Dashboard                                      │ │
│  │  - Admin Panel                                         │ │
│  └────────────────────────────────────────────────────────┘ │
└───────────────────────┬─────────────────────────────────────┘
                        │
        ┌───────────────┼───────────────────────┐
        │               │                       │
        ▼               ▼                       ▼
┌──────────────┐ ┌──────────────┐     ┌──────────────┐
│   Backend    │ │   Quinjet    │     │   Routing    │
│  (Node.js)   │ │   (Go Lang)  │     │   Backend    │
│              │ │              │     │  (Python)    │
│  - Auth      │ │  - Real-time │     │              │
│  - User Mgmt │ │    Tracking  │     │  - Route     │
│  - API       │ │  - WebSocket │     │    Planning  │
│              │ │              │     │  - Landmarks │
└──────┬───────┘ └──────┬───────┘     └──────┬───────┘
       │                │                     │
       │                │                     │
       ▼                ▼                     ▼
┌──────────────┐ ┌──────────────┐     ┌──────────────┐
│   MongoDB    │ │    Redis     │     │ GraphHopper  │
│              │ │  (Cache +    │     │  (Routing    │
│  - Users     │ │   Real-time  │     │   Engine)    │
│  - Sessions  │ │   Data)      │     │              │
└──────────────┘ └──────────────┘     └──────────────┘
```

### Service Communication
- **Frontend ↔ Backend**: RESTful API (Express.js)
- **Frontend ↔ Quinjet**: WebSocket for real-time updates
- **Routing Backend ↔ GraphHopper**: HTTP requests for route calculation
- **Quinjet ↔ Redis**: Direct connection for caching and real-time data

---

## 🛠️ Technology Stack

### Frontend Technologies
| Technology | Version | Purpose |
|------------|---------|---------|
| **React** | 18.3.1 | UI framework for building interactive components |
| **Vite** | 5.4.10 | Lightning-fast build tool and dev server |
| **TailwindCSS** | 3.4.16 | Utility-first CSS framework for styling |
| **DaisyUI** | 4.12.14 | Component library built on Tailwind |
| **Leaflet** | 1.9.4 | Interactive map rendering library |
| **React Leaflet** | 4.2.1 | React bindings for Leaflet |
| **Leaflet Routing Machine** | 3.2.12 | Routing functionality for maps |
| **React Router DOM** | 7.5.2 | Client-side routing |
| **Axios** | 1.8.2 | HTTP client for API requests |

### Backend Technologies (Node.js)
| Technology | Version | Purpose |
|------------|---------|---------|
| **Node.js** | 18.x | JavaScript runtime environment |
| **Express** | 4.21.1 | Web application framework |
| **Mongoose** | 8.8.1 | MongoDB object modeling |
| **Passport** | 0.7.0 | Authentication middleware |
| **Passport Google OAuth20** | 2.0.0 | Google authentication strategy |
| **JWT** | 9.0.2 | JSON Web Token for secure authentication |
| **bcrypt** | 5.1.1 | Password hashing |
| **express-session** | 1.18.1 | Session management |
| **cookie-parser** | 1.4.7 | Cookie parsing middleware |
| **CORS** | 2.8.5 | Cross-Origin Resource Sharing |

### Routing Backend (Python)
| Technology | Version | Purpose |
|------------|---------|---------|
| **FastAPI** | Latest | Modern, fast web framework |
| **Uvicorn** | Latest | ASGI server for FastAPI |
| **GeoPandas** | Latest | Geospatial data processing |
| **Shapely** | Latest | Geometric operations |
| **Requests** | Latest | HTTP library for Python |

### Quinjet Service (Go)
| Technology | Version | Purpose |
|------------|---------|---------|
| **Go** | 1.23.0 | Programming language for high-performance backend |
| **go-redis** | 9.7.0 | Redis client for Go |
| **godotenv** | 1.5.1 | Environment variable management |
| **go-sql-driver/mysql** | 1.8.1 | MySQL database driver |
| **rs/cors** | 1.11.1 | CORS middleware for Go |

### Infrastructure & DevOps
| Technology | Purpose |
|------------|---------|
| **Docker** | Containerization of all services |
| **Docker Compose** | Multi-container orchestration |
| **GraphHopper** | Open-source routing engine |
| **MongoDB** | NoSQL database for user data |
| **Redis** | In-memory data store for caching and real-time data |

---

## 📁 Project Structure

```
mapmitra/
├── frontend/                    # React frontend application
│   ├── src/
│   │   ├── components/         # Reusable UI components
│   │   │   ├── MapComponent.jsx           # Main map interface
│   │   │   ├── UserMap.jsx                # User-specific map view
│   │   │   ├── BottomNavigation.jsx       # Navigation bar
│   │   │   ├── Login.jsx                  # Login component
│   │   │   ├── Register.jsx               # Registration component
│   │   │   ├── Modal.jsx                  # Modal dialogs
│   │   │   ├── RoutingControl.jsx         # Route control UI
│   │   │   └── GettingStarted.jsx         # Onboarding
│   │   ├── pages/              # Page components
│   │   │   ├── Home.jsx                   # Landing page
│   │   │   ├── User.jsx                   # User dashboard
│   │   │   ├── Admin.jsx                  # Admin panel
│   │   │   └── Auto.jsx                   # E-rickshaw page
│   │   ├── utils/              # Utility functions
│   │   ├── App.jsx             # Root component
│   │   ├── main.jsx            # Entry point
│   │   └── index.css           # Global styles
│   ├── public/                 # Static assets
│   ├── package.json            # Dependencies
│   ├── vite.config.js          # Vite configuration
│   └── tailwind.config.js      # Tailwind configuration
│
├── backend/                     # Node.js backend
│   ├── src/
│   │   ├── controllers/        # Request handlers
│   │   │   ├── auth.controller.js         # Authentication logic
│   │   │   └── user.controller.js         # User management
│   │   ├── routes/             # API route definitions
│   │   │   ├── auth.routes.js             # Auth routes
│   │   │   └── user.routes.js             # User routes
│   │   ├── models/             # Database schemas
│   │   │   └── User.models.js             # User model
│   │   ├── middlewares/        # Custom middleware
│   │   │   ├── auth.middleware.js         # Auth verification
│   │   │   └── error.middleware.js        # Error handling
│   │   ├── utils/              # Helper functions
│   │   │   ├── asyncHandler.js            # Async wrapper
│   │   │   ├── ApiError.js                # Error classes
│   │   │   └── ApiResponse.js             # Response formatter
│   │   ├── config/             # Configuration files
│   │   ├── db/                 # Database connection
│   │   ├── app.js              # Express app setup
│   │   └── index.js            # Server entry point
│   └── package.json            # Dependencies
│
├── quinjet/                     # Go service for real-time tracking
│   ├── cmd/                    # Command-line applications
│   ├── internal/               # Internal packages
│   │   └── services/
│   │       ├── health/                    # Health check service
│   │       └── rides/                     # Ride tracking service
│   ├── configs/                # Configuration files
│   ├── db/                     # Database utilities
│   ├── go.mod                  # Go module definition
│   ├── go.sum                  # Dependency checksums
│   └── quinjet.Dockerfile      # Docker configuration
│
├── routing-backend/             # Python routing service
│   ├── api/
│   │   ├── app.py              # FastAPI application
│   │   ├── landmark.py         # Landmark detection logic
│   │   ├── thaparMap.geojson   # Campus map data
│   │   ├── Pipfile             # Python dependencies
│   │   └── api.Dockerfile      # Docker configuration
│   └── graphhopper/            # GraphHopper routing engine
│       ├── thapar_map.osm      # OpenStreetMap data
│       └── config.yml          # GraphHopper configuration
│
├── docker-compose.yml           # Multi-service orchestration
├── README.md                    # Project overview
├── LICENSE                      # MIT License
└── SECURITY.md                  # Security policies
```

---

## 🔧 Core Components

### 1. Frontend Components

#### MapComponent.jsx
**Purpose**: Main interactive map interface with full navigation features

**Key Features**:
- Renders interactive Leaflet map
- Handles user location tracking
- Displays routes and waypoints
- Shows e-rickshaw positions in real-time
- Search functionality for destinations
- Route calculation and display

**Technologies**: React, Leaflet, React Leaflet, Axios

#### Admin.jsx
**Purpose**: Administrative dashboard for managing the system

**Capabilities**:
- Driver management (add/remove/update)
- Route monitoring and control
- User analytics dashboard
- System health monitoring
- Emergency alert broadcasting

#### UserMap.jsx
**Purpose**: Simplified map view for end users

**Features**:
- Clean, user-friendly interface
- Quick destination search
- Saved locations
- Recent routes history

### 2. Backend Services

#### Authentication System
**Files**: `auth.controller.js`, `auth.routes.js`, `auth.middleware.js`

**Flow**:
1. User submits credentials
2. Server validates against MongoDB
3. JWT token generated and returned
4. Token stored in HTTP-only cookie
5. Subsequent requests verified via middleware

**Supported Methods**:
- Email/Password authentication
- Google OAuth 2.0
- Session management

#### User Management
**Files**: `user.controller.js`, `user.routes.js`, `User.models.js`

**Schema** (MongoDB):
```javascript
{
  _id: ObjectId,
  fullName: String,
  email: String (unique, indexed),
  password: String (hashed),
  googleId: String (optional),
  savedLocations: [
    {
      name: String,
      coordinates: [Number, Number],
      timestamp: Date
    }
  ],
  recentSearches: [String],
  createdAt: Date,
  updatedAt: Date
}
```

### 3. Quinjet Service (Real-Time Tracking)

**Purpose**: Handles real-time e-rickshaw location updates using WebSocket and Redis

**Architecture**:
```
Client (WebSocket) → Quinjet Server → Redis
                                    ↓
                              MySQL (Persistence)
```

**Key Functions**:
- Real-time location broadcasting
- Driver status management
- ETA calculations
- Ride history tracking
- Health monitoring endpoint

**Redis Data Structure**:
```
HSET rickshaw:<id> {
  "latitude": 30.3549,
  "longitude": 76.3644,
  "driver_name": "John Doe",
  "status": "available",
  "last_updated": "2024-01-14T12:00:00Z"
}
```

### 4. Routing Backend (Python)

#### Route Calculation Engine
**File**: `app.py`

**Process**:
1. Receive start and end coordinates
2. Forward request to GraphHopper
3. Receive route with waypoints
4. Augment each waypoint with nearby landmarks
5. Generate human-readable instructions
6. Return enhanced route

**Endpoint**: `POST /route_instructions`

**Request**:
```json
{
  "start_coordinates": [30.3549, 76.3644],
  "end_coordinates": [30.3565, 76.3658]
}
```

**Response**:
```json
{
  "routePath": [
    [76.3644, 30.3549],
    [76.3650, 30.3555],
    ...
  ],
  "routeInstructions": [
    {
      "coordinate": {
        "latitude": 30.3555,
        "longitude": 76.3650
      },
      "instruction": "Continue straight towards Library for 150m."
    },
    ...
  ]
}
```

#### Landmark Detection
**File**: `landmark.py`

**Algorithm**:
1. Load campus GeoJSON data
2. Convert coordinates to projected CRS (EPSG:3857)
3. For each route waypoint:
   - Create 50m radius buffer
   - Find intersecting landmarks
   - Calculate distances
   - Select nearest landmark
4. Attach landmark to instruction

**Data Source**: `thaparMap.geojson` (703KB campus map data)

### 5. GraphHopper Routing Engine

**Purpose**: Open-source routing engine for calculating optimal paths

**Configuration** (`config.yml`):
- Profile: Foot (walking routes)
- Map data: Thapar campus OSM file
- Algorithms: Dijkstra, A*, Contraction Hierarchies
- Elevation: Disabled
- Turn costs: Enabled

---

## 🔄 Data Flow

### User Navigation Flow

```
1. User opens app → Frontend loads
                  ↓
2. User searches destination → MapComponent
                  ↓
3. Search query sent → Routing Backend (FastAPI)
                  ↓
4. Routing Backend requests route → GraphHopper
                  ↓
5. GraphHopper calculates optimal path → Returns waypoints
                  ↓
6. Routing Backend augments with landmarks → Processes instructions
                  ↓
7. Enhanced route returned → Frontend
                  ↓
8. Route displayed on map → User sees landmark-based directions
```

### Real-Time E-Rickshaw Tracking Flow

```
1. Driver app updates location → Quinjet Service (WebSocket)
                  ↓
2. Quinjet validates and stores → Redis (real-time cache)
                  ↓
3. Quinjet broadcasts update → All connected clients
                  ↓
4. Frontend receives update → Updates map marker position
                  ↓
5. Quinjet persists to database → MySQL (for history)
                  ↓
6. ETA calculated and sent → User sees updated ETA
```

### Authentication Flow

```
1. User clicks "Login with Google" → Frontend
                  ↓
2. Redirect to Google OAuth → Google Authentication
                  ↓
3. User authorizes → Google returns authorization code
                  ↓
4. Code sent to backend → Passport.js middleware
                  ↓
5. Backend exchanges code for user info → Google API
                  ↓
6. User created/retrieved from MongoDB → User model
                  ↓
7. JWT token generated → Signed with secret
                  ↓
8. Token sent in HTTP-only cookie → Frontend
                  ↓
9. Frontend stores session → User logged in
```

---

## 🚀 Setup & Installation

### Prerequisites
- **Node.js** 18.x or higher
- **Python** 3.9 or higher
- **Go** 1.23 or higher
- **Docker** & **Docker Compose**
- **MongoDB** instance (local or cloud)
- **Redis** instance (local or cloud)

### Environment Variables

#### Backend (.env)
```env
PORT=5000
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/mapmitra
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRES_IN=7d

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_CALLBACK_URL=http://localhost:5000/auth/google/callback

# CORS
CLIENT_URL=http://localhost:3000
```

#### Routing Backend (.env)
```env
GRAPHHOPPER_BASE_URL=http://localhost:8989/route
```

#### Quinjet (.env)
```env
REDIS_HOST=localhost
REDIS_PORT=6379
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASSWORD=password
MYSQL_DATABASE=mapmitra
```

### Installation Steps

#### Option 1: Docker (Recommended)

```bash
# 1. Clone the repository
git clone git@github.com:yxshee/mapmitra.git
cd mapmitra

# 2. Create environment files (see above)
touch backend/.env
touch routing-backend/api/.env
touch quinjet/.env

# 3. Start all services
docker-compose up -d

# 4. Verify services are running
docker-compose ps

# Services will be available at:
# - Frontend: http://localhost:5173
# - Backend: http://localhost:5000
# - Routing Backend: http://localhost:5000 (FastAPI)
# - Quinjet: http://localhost:8080
# - GraphHopper: http://localhost:8989
# - Redis GUI: http://localhost:8001
```

#### Option 2: Manual Setup

**Frontend**:
```bash
cd frontend
npm install
npm run dev
# Runs on http://localhost:5173
```

**Backend**:
```bash
cd backend
npm install
npm run dev
# Runs on http://localhost:5000
```

**Routing Backend**:
```bash
cd routing-backend/api
pip install pipenv
pipenv install
pipenv run python app.py
# Runs on http://localhost:5000
```

**Quinjet**:
```bash
cd quinjet
go mod download
go run cmd/main.go
# Runs on http://localhost:8080
```

**GraphHopper**:
```bash
# Download GraphHopper
docker run -p 8989:8989 \
  -v $(pwd)/routing-backend/graphhopper:/data \
  israelhikingmap/graphhopper:10.0 \
  --input /data/thapar_map.osm \
  --config /data/config.yml
```

---

## ⚙️ How It Works

### 1. Application Startup

**Frontend Initialization**:
```javascript
// main.jsx
ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
)

// App.jsx - Route setup
<Router>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/map" element={<User />} />
    <Route path="/admin" element={<AdminPage />} />
  </Routes>
</Router>
```

**Backend Initialization**:
```javascript
// index.js
dotenv.config();
connectDB()  // Connect to MongoDB
  .then(() => {
    app.listen(PORT, () => {
      console.log(`Server running on port ${PORT}`);
    });
  });
```

### 2. Map Rendering Process

**Leaflet Map Setup**:
```javascript
// MapComponent.jsx (simplified)
const MapComponent = () => {
  const [position, setPosition] = useState([30.3549, 76.3644]);
  const [route, setRoute] = useState(null);

  return (
    <MapContainer center={position} zoom={15}>
      <TileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png" />
      {route && <Polyline positions={route} />}
      <LocationMarker />
    </MapContainer>
  );
};
```

### 3. Route Calculation

**Step-by-Step**:

1. **User Input**: User selects destination on map
2. **Frontend Request**:
   ```javascript
   const response = await axios.post('/route_instructions', {
     start_coordinates: [startLat, startLng],
     end_coordinates: [endLat, endLng]
   });
   ```

3. **Routing Backend Processing**:
   ```python
   # app.py
   @app.post("/route_instructions")
   async def get_route_instructions(request: RouteRequest):
       # Request route from GraphHopper
       route_data = requests.post(GRAPHHOPPER_BASE_URL, json=request_body)
       
       # Augment with landmarks
       augmented_instructions = process_route(route_data)
       
       # Return enhanced route
       return {
           "routePath": coordinate_points,
           "routeInstructions": route_instructions
       }
   ```

4. **Landmark Augmentation**:
   ```python
   def find_nearby_landmarks(lat, lng, radius=50):
       point = gpd.GeoSeries([Point(lng, lat)], crs="EPSG:4326")
       nearby = landmarks[landmarks.geometry.distance(point) <= radius]
       return nearby_landmarks
   ```

5. **Frontend Display**:
   ```javascript
   setRoute(response.data.routePath);
   setInstructions(response.data.routeInstructions);
   ```

### 4. Real-Time Tracking

**WebSocket Connection**:
```javascript
// Frontend
const socket = new WebSocket('ws://localhost:8080');

socket.onmessage = (event) => {
  const update = JSON.parse(event.data);
  updateRickshawPosition(update);
};
```

**Quinjet Handler** (Go):
```go
// Simplified
func handleLocationUpdate(ws *websocket.Conn) {
    var location Location
    ws.ReadJSON(&location)
    
    // Store in Redis
    redis.HSet(ctx, "rickshaw:"+location.ID, location)
    
    // Broadcast to all clients
    broadcastUpdate(location)
    
    // Persist to MySQL
    db.Insert(location)
}
```

### 5. Authentication Process

**Google OAuth Flow**:
```javascript
// Backend - auth routes
passport.use(new GoogleStrategy({
    clientID: process.env.GOOGLE_CLIENT_ID,
    clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    callbackURL: "/auth/google/callback"
  },
  async (accessToken, refreshToken, profile, done) => {
    // Find or create user
    let user = await User.findOne({ googleId: profile.id });
    if (!user) {
      user = await User.create({
        googleId: profile.id,
        email: profile.emails[0].value,
        fullName: profile.displayName
      });
    }
    return done(null, user);
  }
));
```

---

## 📡 API Documentation

### Backend API (Node.js)

#### Authentication Endpoints

**POST `/api/v1/auth/register`**
- Register new user with email/password
- Request Body:
  ```json
  {
    "fullName": "John Doe",
    "email": "john@example.com",
    "password": "securePassword123"
  }
  ```
- Response: `{ user, token }`

**POST `/api/v1/auth/login`**
- Login with credentials
- Request Body:
  ```json
  {
    "email": "john@example.com",
    "password": "securePassword123"
  }
  ```
- Response: `{ user, token }`

**GET `/api/v1/auth/google`**
- Initiate Google OAuth flow
- Redirects to Google login

**GET `/api/v1/auth/google/callback`**
- Google OAuth callback
- Creates session and redirects to app

**POST `/api/v1/auth/logout`**
- Logout current user
- Clears session cookie

#### User Endpoints

**GET `/api/v1/users/profile`**
- Get current user profile
- Requires authentication
- Response: `{ user }`

**PUT `/api/v1/users/profile`**
- Update user profile
- Requires authentication
- Request Body: `{ fullName?, savedLocations? }`

### Routing Backend API (Python/FastAPI)

**POST `/route_instructions`**
- Calculate route with landmark-based instructions
- Request:
  ```json
  {
    "start_coordinates": [30.3549, 76.3644],
    "end_coordinates": [30.3565, 76.3658]
  }
  ```
- Response:
  ```json
  {
    "routePath": [[76.3644, 30.3549], ...],
    "routeInstructions": [
      {
        "coordinate": {"latitude": 30.3555, "longitude": 76.3650},
        "instruction": "Continue straight towards Library for 150m."
      }
    ]
  }
  ```

### Quinjet API (Go)

**GET `/api/v1/health`**
- Health check endpoint
- Response: `{ status: "ok" }`

**WebSocket `/ws/tracking`**
- Real-time location updates
- Message format:
  ```json
  {
    "type": "location_update",
    "rickshaw_id": "123",
    "latitude": 30.3549,
    "longitude": 76.3644,
    "timestamp": "2024-01-14T12:00:00Z"
  }
  ```

**GET `/api/v1/rickshaws`**
- Get all active rickshaw locations
- Response: Array of rickshaw objects

**POST `/api/v1/rides`**
- Record new ride
- Request Body: Ride details

---

## 🐳 Deployment

### Docker Compose Configuration

The `docker-compose.yml` orchestrates 4 services:

1. **GraphHopper**: Routing engine (port 8989)
2. **Routing Backend**: Python API (port 5000)
3. **Redis**: Cache and real-time data (ports 6379, 8001)
4. **Quinjet**: Go tracking service (port 8080)

**Service Dependencies**:
```yaml
routing-backend:
  depends_on:
    graphhopper:
      condition: service_healthy

quinjet:
  depends_on:
    redis:
      condition: service_healthy
```

**Health Checks**:
- GraphHopper: `curl http://localhost:8989/health`
- Redis: `redis-cli ping`
- Quinjet: `curl http://localhost:8080/api/v1/health`

### Production Deployment Options

#### Option 1: Cloud Platforms (Recommended for Frontend & Backend)
- **Vercel**: Frontend (React)
- **Heroku/Railway**: Backend (Node.js)
- **MongoDB Atlas**: Database (cloud MongoDB)
- **Redis Cloud**: Managed Redis

#### Option 2: Container Orchestration
- **AWS ECS**: Managed Docker containers
- **Google Cloud Run**: Serverless containers
- **DigitalOcean App Platform**: Simple container deployment

#### Option 3: Full Docker Deployment
- **AWS EC2** or **DigitalOcean Droplet**
- Install Docker & Docker Compose
- Clone repository and run `docker-compose up -d`
- Configure reverse proxy (Nginx) for SSL

### Environment-Specific Configurations

**Production Frontend**:
```javascript
// vite.config.js
export default defineConfig({
  plugins: [react()],
  build: {
    outDir: 'dist',
    sourcemap: false,
    minify: 'terser'
  }
});
```

**Production Backend**:
```javascript
// app.js
app.use(cors({
  origin: process.env.CLIENT_URL,
  credentials: true
}));

app.use(helmet());  // Security headers
app.use(compression());  // Response compression
```

---

## 🔐 Security Considerations

### Implemented Security Measures

1. **Authentication**:
   - JWT tokens with expiration
   - HTTP-only cookies
   - bcrypt password hashing (10 rounds)
   - Google OAuth 2.0

2. **API Security**:
   - CORS configuration
   - Rate limiting (recommended to implement)
   - Input validation with Pydantic (FastAPI)
   - Helmet.js for security headers

3. **Data Protection**:
   - Environment variables for secrets
   - MongoDB connection over TLS
   - Redis authentication (optional)

4. **Frontend Security**:
   - XSS prevention through React
   - CSRF tokens (recommended)
   - Secure WebSocket connections (wss://)

### Recommended Additions

- Rate limiting middleware (express-rate-limit)
- API key authentication for services
- Input sanitization
- SQL injection prevention (using ORMs)
- Regular security audits
- HTTPS enforcement in production

---

## 🧪 Testing

### Recommended Testing Strategy

**Frontend**:
- Unit tests: Jest + React Testing Library
- E2E tests: Cypress or Playwright
- Test map interactions and routing

**Backend**:
- Unit tests: Jest/Mocha
- Integration tests: Supertest
- API endpoint testing

**Routing Backend**:
- Unit tests: pytest
- Test landmark detection accuracy
- Route calculation validation

**Quinjet**:
- Unit tests: Go testing package
- WebSocket connection tests
- Redis integration tests

---

## 📊 Performance Optimization

### Current Optimizations

1. **Frontend**:
   - Vite for fast builds
   - Code splitting with React.lazy
   - Image optimization
   - Caching strategies

2. **Backend**:
   - MongoDB indexing on email field
   - Connection pooling
   - Redis caching for frequent queries

3. **Routing**:
   - GraphHopper Contraction Hierarchies
   - Geospatial indexing on landmarks
   - Response caching

### Monitoring

- **Recommended Tools**:
  - Sentry for error tracking
  - New Relic/DataDog for APM
  - Prometheus + Grafana for metrics
  - ELK stack for logging

---

## 🤝 Contributing

### Development Workflow

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open Pull Request

### Code Style

- **JavaScript**: ESLint configuration
- **Python**: PEP 8, Black formatter
- **Go**: gofmt, golint

---

## 📝 License

This project is licensed under the **MIT License**. See `LICENSE` file for details.

---

## 👥 Team

- **Ansh Midha** - [@AM0312](https://github.com/AM0312)
- **Leena Gupta** - [@leena153](https://github.com/leena153)
- **Madhur Gaba** - [@madhurgaba2603](https://github.com/madhurgaba2603)
- **Shourya De** - [@shouryade](https://github.com/shouryade)
- **Yash Dogra** - [@yxshee](https://github.com/yxshee)

---

## 📞 Support

For issues and questions:
- GitHub Issues: [MapMitra Issues](https://github.com/yxshee/mapmitra/issues)
- Email: Contact via GitHub profiles

---

**Made with ❤️ by TIET Students | 🧭 Happy Navigating!**
