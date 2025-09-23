# 🛠️ MapMitra - Technology Stack Reference

## 📋 Complete Technology Breakdown

This document provides detailed information about every technology used in MapMitra and why it was chosen.

---

## 🎨 Frontend Technologies

### React 18.3.1
**Category**: UI Framework  
**Language**: JavaScript  
**Purpose**: Building interactive user interfaces

**Why React?**
- ✅ Component-based architecture for reusable code
- ✅ Virtual DOM for efficient rendering
- ✅ Large ecosystem and community support
- ✅ Excellent for building complex SPAs
- ✅ React Hooks for state management

**Used In MapMitra For**:
- Map component rendering
- User interface components
- State management across the app
- Route-based navigation

**Key React Features We Use**:
```javascript
// Hooks
useState()      // Component state
useEffect()     // Side effects (API calls, subscriptions)
useRef()        // DOM references (map instance)
useContext()    // Global state (auth, theme)

// Components
<MapContainer>  // Leaflet map wrapper
<Route>         // React Router navigation
```

---

### Vite 5.4.10
**Category**: Build Tool  
**Language**: JavaScript  
**Purpose**: Fast development server and production builds

**Why Vite?**
- ✅ Lightning-fast HMR (Hot Module Replacement)
- ✅ Native ES modules support
- ✅ Optimized production builds
- ✅ Out-of-box TypeScript, JSX, CSS support
- ✅ Much faster than Create React App or Webpack

**Performance Comparison**:
```
Cold Start:
Webpack: ~45 seconds
Vite:    ~2 seconds

Hot Reload:
Webpack: ~3-5 seconds
Vite:    ~50ms
```

**Configuration**:
```javascript
// vite.config.js
export default {
  plugins: [react()],
  server: { port: 5173 },
  build: { outDir: 'dist' }
}
```

---

### TailwindCSS 3.4.16
**Category**: CSS Framework  
**Language**: CSS  
**Purpose**: Utility-first styling

**Why Tailwind?**
- ✅ Rapid UI development
- ✅ Consistent design system
- ✅ Small production bundle (purges unused CSS)
- ✅ Responsive design utilities
- ✅ Easy customization

**Example Usage**:
```jsx
<button className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Navigate
</button>
```

**MapMitra Custom Theme**:
```javascript
// tailwind.config.js
theme: {
  extend: {
    colors: {
      primary: '#3B82F6',
      secondary: '#10B981',
      accent: '#F59E0B'
    }
  }
}
```

---

### DaisyUI 4.12.14
**Category**: Component Library  
**Built On**: TailwindCSS  
**Purpose**: Pre-built UI components

**Why DaisyUI?**
- ✅ Beautiful components out of the box
- ✅ Built on Tailwind (no additional CSS)
- ✅ Theme system with dark mode
- ✅ Accessibility-focused
- ✅ Zero JavaScript required

**Components We Use**:
- Buttons, Cards, Modals
- Navigation bars
- Forms and inputs
- Alerts and badges
- Loading spinners

---

### Leaflet 1.9.4
**Category**: Mapping Library  
**Language**: JavaScript  
**Purpose**: Interactive map rendering

**Why Leaflet?**
- ✅ Lightweight (~40KB)
- ✅ Mobile-friendly
- ✅ Extensive plugin ecosystem
- ✅ Open-source and free
- ✅ Works with any base map provider

**Alternatives Considered**:
- ❌ Google Maps: Expensive, requires API key
- ❌ Mapbox: Pricing limitations
- ✅ Leaflet: Free, flexible, powerful

**Core Features Used**:
```javascript
// Map initialization
const map = L.map('map').setView([30.3549, 76.3644], 15);

// Tile layer (OpenStreetMap)
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);

// Markers
L.marker([lat, lng]).addTo(map);

// Polylines (routes)
L.polyline(coordinates, {color: 'blue'}).addTo(map);

// Popups
marker.bindPopup('Location Info');
```

---

### React Leaflet 4.2.1
**Category**: React Bindings  
**Purpose**: React components for Leaflet

**Benefits**:
- ✅ Declarative map creation
- ✅ React component lifecycle integration
- ✅ Hooks for map interaction
- ✅ State management with React

**Example**:
```jsx
<MapContainer center={[30.3549, 76.3644]} zoom={15}>
  <TileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png" />
  <Marker position={position}>
    <Popup>Campus Location</Popup>
  </Marker>
</MapContainer>
```

---

### Leaflet Routing Machine 3.2.12
**Category**: Routing Plugin  
**Purpose**: Route display and turn-by-turn directions

**Features**:
- Route calculation and display
- Turn-by-turn instructions
- Alternative routes
- Waypoint management
- Customizable routing engines

**Integration**:
```javascript
L.Routing.control({
  waypoints: [
    L.latLng(startLat, startLng),
    L.latLng(endLat, endLng)
  ],
  router: customGraphHopperRouter
}).addTo(map);
```

---

### React Router DOM 7.5.2
**Category**: Routing Library  
**Purpose**: Client-side navigation

**Why React Router?**
- ✅ Industry standard for React routing
- ✅ Nested routes support
- ✅ Dynamic route matching
- ✅ Browser history management
- ✅ Protected routes for authentication

**Route Structure**:
```javascript
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/map" element={<User />} />
  <Route path="/admin" element={<ProtectedRoute><Admin /></ProtectedRoute>} />
</Routes>
```

---

### Axios 1.8.2
**Category**: HTTP Client  
**Purpose**: API requests

**Why Axios over Fetch?**
- ✅ Automatic JSON transformation
- ✅ Request/response interceptors
- ✅ Request cancellation
- ✅ Better error handling
- ✅ Progress tracking for uploads

**Usage in MapMitra**:
```javascript
// API client setup
const api = axios.create({
  baseURL: 'http://localhost:5000/api',
  withCredentials: true
});

// Request interceptor (add auth token)
api.interceptors.request.use(config => {
  config.headers.Authorization = `Bearer ${token}`;
  return config;
});

// Example request
const route = await api.post('/route_instructions', {
  start_coordinates: [lat, lng],
  end_coordinates: [lat2, lng2]
});
```

---

## 🔧 Backend Technologies (Node.js)

### Node.js 18.x
**Category**: Runtime Environment  
**Language**: JavaScript  
**Purpose**: Server-side JavaScript execution

**Why Node.js?**
- ✅ JavaScript on frontend and backend
- ✅ Non-blocking I/O (great for real-time apps)
- ✅ NPM ecosystem (1M+ packages)
- ✅ High performance for I/O-heavy tasks
- ✅ Easy to scale

**Node.js Event Loop Benefits**:
```javascript
// Non-blocking operations
const users = await User.find();  // Doesn't block other requests
const routes = await calculateRoute();
```

---

### Express 4.21.1
**Category**: Web Framework  
**Language**: JavaScript  
**Purpose**: HTTP server and routing

**Why Express?**
- ✅ Minimalist and flexible
- ✅ Extensive middleware ecosystem
- ✅ Industry standard for Node.js
- ✅ Great documentation
- ✅ Easy to learn and use

**Express App Structure**:
```javascript
const express = require('express');
const app = express();

// Middleware
app.use(express.json());
app.use(cors());
app.use(cookieParser());

// Routes
app.use('/api/v1/auth', authRoutes);
app.use('/api/v1/users', userRoutes);

// Error handling
app.use(errorHandler);

app.listen(5000);
```

**Middleware We Use**:
- `express.json()` - Parse JSON bodies
- `cors()` - Cross-origin requests
- `cookie-parser` - Parse cookies
- `express-session` - Session management
- `passport` - Authentication

---

### MongoDB 8.8.1 (via Mongoose)
**Category**: Database  
**Type**: NoSQL (Document Store)  
**Purpose**: Data persistence

**Why MongoDB?**
- ✅ Flexible schema (perfect for evolving project)
- ✅ JSON-like documents (natural for JavaScript)
- ✅ Scalable (horizontal scaling)
- ✅ Rich query language
- ✅ Great for location-based data (geospatial queries)

**Mongoose Benefits**:
- Schema validation
- Middleware (hooks)
- Query builders
- Population (joins)
- Virtuals and plugins

**User Schema Example**:
```javascript
const userSchema = new mongoose.Schema({
  fullName: { type: String, required: true },
  email: { 
    type: String, 
    required: true, 
    unique: true,
    index: true  // Index for fast lookups
  },
  password: { type: String, select: false },
  googleId: String,
  savedLocations: [{
    name: String,
    coordinates: {
      type: [Number],  // [lng, lat]
      index: '2dsphere'  // Geospatial index
    }
  }]
}, { timestamps: true });
```

**Geospatial Queries**:
```javascript
// Find locations near a point
User.find({
  'savedLocations.coordinates': {
    $near: {
      $geometry: { type: 'Point', coordinates: [lng, lat] },
      $maxDistance: 1000  // meters
    }
  }
});
```

---

### Passport.js 0.7.0
**Category**: Authentication Middleware  
**Purpose**: User authentication strategies

**Why Passport?**
- ✅ 500+ authentication strategies
- ✅ OAuth integration (Google, Facebook, GitHub)
- ✅ Session management
- ✅ Easy to extend
- ✅ Industry standard

**Strategies We Use**:
1. **Local Strategy** (email/password)
2. **Google OAuth 2.0** (social login)

**Google OAuth Flow**:
```javascript
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

### JWT (jsonwebtoken) 9.0.2
**Category**: Authentication  
**Purpose**: Stateless authentication tokens

**Why JWT?**
- ✅ Stateless (no server-side session storage)
- ✅ Scalable (works across multiple servers)
- ✅ Self-contained (carries user info)
- ✅ Secure (signed and optionally encrypted)
- ✅ Works with mobile apps and SPAs

**JWT Structure**:
```
Header.Payload.Signature

{
  "alg": "HS256",
  "typ": "JWT"
}
.
{
  "userId": "123",
  "email": "user@example.com",
  "iat": 1516239022,
  "exp": 1516325422
}
.
HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)
```

**Token Generation**:
```javascript
const token = jwt.sign(
  { userId: user._id, email: user.email },
  process.env.JWT_SECRET,
  { expiresIn: '7d' }
);
```

**Token Verification**:
```javascript
// Middleware
const verifyToken = (req, res, next) => {
  const token = req.cookies.token;
  if (!token) return res.status(401).json({ error: 'Unauthorized' });
  
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
};
```

---

### bcrypt 5.1.1
**Category**: Password Hashing  
**Purpose**: Secure password storage

**Why bcrypt?**
- ✅ Slow by design (prevents brute force)
- ✅ Built-in salt (prevents rainbow tables)
- ✅ Configurable work factor
- ✅ Industry standard
- ✅ Resistant to timing attacks

**How It Works**:
```javascript
// Hash password (registration)
const salt = await bcrypt.genSalt(10);  // 10 rounds
const hashedPassword = await bcrypt.hash(password, salt);

// Verify password (login)
const isMatch = await bcrypt.compare(inputPassword, hashedPassword);
```

**Security Notes**:
- Work factor of 10 = ~100ms to hash
- Higher work factor = more secure but slower
- Automatically handles salting

---

### CORS 2.8.5
**Category**: Security Middleware  
**Purpose**: Cross-Origin Resource Sharing

**Why CORS?**
- ✅ Browser security requirement
- ✅ Control which origins can access API
- ✅ Prevent CSRF attacks
- ✅ Configure allowed methods and headers

**Configuration**:
```javascript
app.use(cors({
  origin: process.env.CLIENT_URL,  // Only allow frontend
  credentials: true,  // Allow cookies
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization']
}));
```

---

## 🐍 Routing Backend (Python)

### FastAPI (Latest)
**Category**: Web Framework  
**Language**: Python  
**Purpose**: High-performance API for routing

**Why FastAPI?**
- ✅ Fast (on par with Node.js and Go)
- ✅ Automatic API documentation (Swagger/OpenAPI)
- ✅ Type hints and validation (Pydantic)
- ✅ Async support
- ✅ Modern Python features

**Performance**:
```
Requests/second:
Flask:    2,000
FastAPI:  25,000
Go:       30,000
```

**Example Endpoint**:
```python
@app.post("/route_instructions")
async def get_route_instructions(request: RouteRequest):
    # Pydantic automatically validates request
    route = await calculate_route(
        request.start_coordinates,
        request.end_coordinates
    )
    return route
```

**Auto-Generated Docs**:
- Swagger UI: http://localhost:5000/docs
- ReDoc: http://localhost:5000/redoc

---

### GeoPandas (Latest)
**Category**: Geospatial Library  
**Built On**: Pandas  
**Purpose**: Geospatial data manipulation

**Why GeoPandas?**
- ✅ Extends Pandas with geometry support
- ✅ Read/write geospatial formats (GeoJSON, Shapefile)
- ✅ Spatial operations (intersections, buffers, unions)
- ✅ Coordinate system transformations
- ✅ Integrates with Shapely and Fiona

**Usage in MapMitra**:
```python
import geopandas as gpd
from shapely.geometry import Point

# Load campus landmarks
landmarks = gpd.read_file('thaparMap.geojson')

# Transform coordinate system
landmarks = landmarks.to_crs(epsg=3857)

# Find nearby landmarks
point = gpd.GeoSeries([Point(lng, lat)], crs="EPSG:4326")
nearby = landmarks[landmarks.geometry.distance(point.iloc[0]) <= 50]
```

---

### Shapely (Latest)
**Category**: Geometric Operations  
**Purpose**: 2D geometry manipulation

**Features**:
- Points, Lines, Polygons
- Spatial operations (buffer, intersection, union)
- Distance calculations
- Coordinate transformations

**Example**:
```python
from shapely.geometry import Point, LineString

# Create shapes
point = Point(76.3644, 30.3549)
line = LineString([(76.364, 30.354), (76.366, 30.356)])

# Operations
distance = point.distance(line)
buffer = point.buffer(50)  # 50m radius
intersects = buffer.intersects(line)
```

---

### Uvicorn (Latest)
**Category**: ASGI Server  
**Purpose**: Run FastAPI applications

**Why Uvicorn?**
- ✅ Lightning-fast ASGI server
- ✅ WebSocket support
- ✅ HTTP/2 support
- ✅ Auto-reload in development
- ✅ Production-ready

**Running FastAPI**:
```bash
uvicorn app:app --host 0.0.0.0 --port 5000 --reload
```

---

## 🚀 Quinjet Service (Go)

### Go 1.23.0
**Category**: Programming Language  
**Purpose**: High-performance backend service

**Why Go?**
- ✅ Blazing fast (compiled language)
- ✅ Built-in concurrency (goroutines)
- ✅ Low memory footprint
- ✅ Simple syntax
- ✅ Great for microservices

**Concurrency Example**:
```go
// Handle multiple connections concurrently
go func() {
    for msg := range messages {
        processMessage(msg)  // Runs in parallel
    }
}()
```

**Performance**:
```
Language    Startup Time    Memory Usage
Node.js     300ms          50MB
Python      500ms          80MB
Go          10ms           10MB
```

---

### go-redis 9.7.0
**Category**: Redis Client  
**Purpose**: Redis integration

**Features**:
- Pub/Sub support
- Pipeline commands
- Transactions
- Cluster support
- Sentinel support

**Usage**:
```go
import "github.com/redis/go-redis/v9"

client := redis.NewClient(&redis.Options{
    Addr: "localhost:6379",
})

// Set data
client.Set(ctx, "rickshaw:123", locationJSON, 0)

// Get data
val, err := client.Get(ctx, "rickshaw:123").Result()

// Pub/Sub
pubsub := client.Subscribe(ctx, "location-updates")
```

---

### WebSocket in Go
**Purpose**: Real-time bidirectional communication

**Why WebSocket?**
- ✅ Low latency (perfect for tracking)
- ✅ Bidirectional communication
- ✅ Persistent connection
- ✅ Less overhead than HTTP polling

**Implementation**:
```go
import "github.com/gorilla/websocket"

// Upgrade HTTP to WebSocket
conn, _ := upgrader.Upgrade(w, r, nil)

// Send message
conn.WriteJSON(location)

// Receive message
var msg Message
conn.ReadJSON(&msg)

// Broadcast to all clients
for client := range clients {
    client.WriteJSON(update)
}
```

---

### godotenv 1.5.1
**Category**: Environment Variables  
**Purpose**: Load .env files

**Usage**:
```go
import "github.com/joho/godotenv"

godotenv.Load()
redisHost := os.Getenv("REDIS_HOST")
```

---

## 🗄️ Databases & Infrastructure

### Redis (Latest)
**Category**: In-Memory Data Store  
**Purpose**: Caching and real-time data

**Why Redis?**
- ✅ Extremely fast (in-memory)
- ✅ Rich data structures (strings, hashes, lists, sets)
- ✅ Pub/Sub messaging
- ✅ Persistence options
- ✅ Atomic operations

**Use Cases in MapMitra**:
1. **Caching**: Frequently accessed data
2. **Real-time Tracking**: E-rickshaw locations
3. **Session Storage**: User sessions
4. **Pub/Sub**: Location broadcasts

**Data Structures Used**:
```redis
# Hash for rickshaw data
HSET rickshaw:123 latitude 30.3549
HSET rickshaw:123 longitude 76.3644
HSET rickshaw:123 status "available"

# Get all data
HGETALL rickshaw:123

# Pub/Sub
PUBLISH location-updates "{...}"
SUBSCRIBE location-updates
```

**Performance**:
- 100,000+ operations/second
- Sub-millisecond latency
- Can handle millions of keys

---

### GraphHopper 10.0
**Category**: Routing Engine  
**Language**: Java  
**Purpose**: Route calculation

**Why GraphHopper?**
- ✅ Open-source (free)
- ✅ Fast routing algorithms
- ✅ Supports OpenStreetMap data
- ✅ Multiple routing profiles (car, bike, foot)
- ✅ Turn-by-turn navigation
- ✅ Elevation data support

**Algorithms**:
1. **Dijkstra**: Guaranteed shortest path
2. **A***: Faster with heuristic
3. **Contraction Hierarchies**: Pre-processed, ultra-fast

**Features**:
- Alternative routes
- Avoid areas
- Custom speeds
- Time-dependent routing
- Isochrone maps

**API Request**:
```json
POST /route
{
  "points": [[76.3644, 30.3549], [76.3658, 30.3565]],
  "profile": "foot",
  "points_encoded": false,
  "instructions": true
}
```

**Response**:
```json
{
  "paths": [{
    "distance": 450.5,
    "time": 324000,
    "points": {...},
    "instructions": [...]
  }]
}
```

---

## 🐳 DevOps & Infrastructure

### Docker
**Category**: Containerization  
**Purpose**: Package applications with dependencies

**Why Docker?**
- ✅ Consistent environments (dev/prod)
- ✅ Isolation (no dependency conflicts)
- ✅ Easy deployment
- ✅ Scalability
- ✅ Version control for infrastructure

**Dockerfile Example** (Quinjet):
```dockerfile
FROM golang:1.23-alpine
WORKDIR /app
COPY . .
RUN go mod download
RUN go build -o quinjet cmd/main.go
EXPOSE 8080
CMD ["./quinjet"]
```

---

### Docker Compose
**Category**: Multi-Container Orchestration  
**Purpose**: Define and run multi-container apps

**Benefits**:
- ✅ Single command to start all services
- ✅ Service dependencies management
- ✅ Network configuration
- ✅ Volume management
- ✅ Environment variable handling

**Key Features We Use**:
```yaml
services:
  graphhopper:
    image: israelhikingmap/graphhopper:10.0
    depends_on:
      - redis
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8989/health"]
    restart: on-failure
```

---

## 📊 Technology Selection Criteria

### How We Chose Our Stack

| Criteria | Weight | Winners |
|----------|--------|---------|
| **Performance** | 30% | Go, Redis, Vite, FastAPI |
| **Developer Experience** | 25% | React, Express, Tailwind |
| **Community Support** | 20% | Node.js, React, MongoDB |
| **Cost** | 15% | All open-source |
| **Scalability** | 10% | Docker, Redis, MongoDB |

---

## 🎯 Best Practices We Follow

### Frontend
- ✅ Component composition over inheritance
- ✅ Custom hooks for reusable logic
- ✅ Lazy loading for code splitting
- ✅ Error boundaries for error handling
- ✅ Accessible components (WCAG 2.1)

### Backend
- ✅ RESTful API design
- ✅ JWT for stateless authentication
- ✅ Input validation and sanitization
- ✅ Error handling middleware
- ✅ Logging and monitoring

### Database
- ✅ Indexing for frequently queried fields
- ✅ Connection pooling
- ✅ Data validation at schema level
- ✅ Backup strategies
- ✅ Migration scripts

### DevOps
- ✅ Environment-based configuration
- ✅ Health check endpoints
- ✅ Graceful shutdown handling
- ✅ Container security best practices
- ✅ Secret management

---

## 🔮 Future Technology Additions

### Planned Enhancements

1. **TypeScript** - Type safety across frontend/backend
2. **Redis Cluster** - Horizontal scaling for tracking
3. **Kubernetes** - Container orchestration
4. **GraphQL** - Flexible API queries
5. **WebRTC** - Peer-to-peer communication
6. **PWA** - Offline support and installability

---

**📚 For more details, see [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md)**
