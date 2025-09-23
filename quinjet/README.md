# 🚀 Quinjet - Real-time Ride Matching Service

A high-performance Go microservice for real-time e-rickshaw ride matching and tracking in the MapMitra ecosystem. Built for speed, scalability, and reliability.

## 📋 Overview

Quinjet serves as the real-time ride matching engine for MapMitra, handling ride requests, driver-passenger matching, and live location tracking. Built with Go for optimal performance and Redis for lightning-fast data operations, it ensures minimal latency in ride matching and status updates.

## ✨ Features

### 🎯 Real-time Ride Matching
- **Instant Matching**: Sub-second ride request processing
- **Proximity-based Matching**: Geographic grid-based driver allocation
- **Request Queue Management**: Efficient handling of concurrent ride requests
- **Fallback Mechanisms**: Multi-level search for optimal driver matching

### 📍 Location Services
- **Live Tracking**: Real-time location updates for vehicles and passengers
- **Grid-based Partitioning**: Efficient spatial data organization
- **Distance Calculations**: Optimized proximity calculations
- **Location History**: Track movement patterns for analytics

### 🚗 Driver Management
- **Driver Status Tracking**: Online/offline/busy status management
- **Vehicle Assignment**: Dynamic vehicle-driver associations
- **Availability Management**: Real-time availability updates
- **Performance Metrics**: Driver performance tracking

### ⚡ High Performance
- **Redis Integration**: In-memory data storage for ultra-fast operations
- **Concurrent Processing**: Go's goroutine-based concurrent request handling
- **Connection Pooling**: Optimized database connection management
- **Health Monitoring**: Built-in health checks and monitoring

## 🛠️ Tech Stack

### Core Technologies
![Go](https://img.shields.io/badge/-Go-00ADD8?logo=go&logoColor=white&style=flat-square)
![Redis](https://img.shields.io/badge/-Redis-DC382D?logo=redis&logoColor=white&style=flat-square)
![Docker](https://img.shields.io/badge/-Docker-2496ED?logo=docker&logoColor=white&style=flat-square)

### Database & Storage
![MySQL](https://img.shields.io/badge/-MySQL-4479A1?logo=mysql&logoColor=white&style=flat-square)
![Redis Stack](https://img.shields.io/badge/-Redis_Stack-DC382D?logo=redis&logoColor=white&style=flat-square)

### Development & Deployment
![Docker Compose](https://img.shields.io/badge/-Docker_Compose-2496ED?logo=docker&logoColor=white&style=flat-square)
![CORS](https://img.shields.io/badge/-CORS-000000?style=flat-square)

## 📦 Dependencies

### Core Dependencies
```go
require (
    github.com/go-sql-driver/mysql v1.8.1
    github.com/joho/godotenv v1.5.1
    github.com/redis/go-redis/v9 v9.7.0
    github.com/rs/cors v1.11.1
)
```

### Indirect Dependencies
```go
require (
    filippo.io/edwards25519 v1.1.0 // indirect
    github.com/cespare/xxhash/v2 v2.3.0 // indirect
    github.com/dgryski/go-rendezvous v0.0.0-20200823014737-9f7001d12a5f // indirect
)
```

## 🚀 Quick Start

### Prerequisites
- **Go**: Version 1.23 or higher
- **Redis**: Version 6.0 or higher (Redis Stack recommended)
- **Docker**: For containerized deployment
- **MySQL**: Version 8.0 or higher (optional, for persistent data)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yxshee/mapmitra.git
   cd mapmitra/quinjet
   ```

2. **Install dependencies**
   ```bash
   go mod download
   go mod tidy
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```
   
   Configure the following variables:
   ```env
   # Server Configuration
   PORT=8080
   ENVIRONMENT=development
   
   # Redis Configuration
   REDIS_HOST=localhost
   REDIS_PORT=6379
   REDIS_PASSWORD=""
   REDIS_DB=0
   
   # MySQL Configuration (optional)
   MYSQL_HOST=localhost
   MYSQL_PORT=3306
   MYSQL_USER=quinjet
   MYSQL_PASSWORD=password
   MYSQL_DATABASE=quinjet
   
   # Service Configuration
   MAX_SEARCH_RADIUS=5000  # meters
   CLEANUP_INTERVAL=300    # seconds
   REQUEST_TIMEOUT=30      # seconds
   ```

4. **Run Redis (if not using Docker)**
   ```bash
   # Using Redis Docker
   docker run -d -p 6379:6379 redis/redis-stack:latest
   
   # Or install locally
   redis-server
   ```

5. **Start the development server**
   ```bash
   go run cmd/main.go
   ```

   The service will be available at `http://localhost:8080`

### Docker Deployment

```bash
# Build and run with Docker Compose
docker-compose up --build

# Or build manually
docker build -f quinjet.Dockerfile -t quinjet .
docker run -p 8080:8080 --env-file .env quinjet
```

## 📁 Project Structure

```
quinjet/
├── cmd/                       # Application entry points
│   ├── main.go               # Main application entry
│   ├── api/                  # API server setup
│   │   └── api.go           # HTTP server and routing
│   └── worker/              # Background workers
│       └── worker.go        # Cleanup and maintenance tasks
├── configs/                  # Configuration management
│   └── envs.go              # Environment variable handling
├── db/                      # Database connections
│   └── db.go                # Database initialization
├── internal/                # Internal packages
│   └── services/            # Business logic services
│       ├── health/          # Health check service
│       │   └── health.go
│       └── rides/           # Ride management service
│           ├── accept.go    # Ride acceptance logic
│           ├── actions.go   # Ride actions and status updates
│           └── rides.go     # Core ride matching logic
├── docker-compose.yml       # Multi-service orchestration
├── quinjet.Dockerfile      # Docker build configuration
├── Dockerfile              # Alternative Docker configuration
├── go.mod                  # Go module definition
└── go.sum                  # Go module checksums
```

## 🌐 API Endpoints

### Health Check

#### Get Service Health
```http
GET /api/v1/health/
```

**Response:**
```json
{
  "status": "healthy",
  "timestamp": "2024-08-15T10:30:00Z",
  "version": "1.0.0",
  "redis_status": "connected"
}
```

### Ride Management

#### Create New Ride Request
```http
POST /api/v1/rides/new
Content-Type: application/json

{
  "requestID": "user123_1692095400",
  "level": [
    {"x": 10, "y": 15},
    {"x": 11, "y": 15},
    {"x": 10, "y": 16}
  ],
  "pickup": [30.354123, 76.362456]
}
```

**Response:**
```json
{
  "success": true,
  "requestID": "user123_1692095400",
  "status": "searching",
  "estimatedWaitTime": "2-5 minutes"
}
```

#### Check Ride Status
```http
GET /api/v1/rides/status?requestID=user123_1692095400
```

**Response (Searching):**
```json
{
  "requestID": "user123_1692095400",
  "status": "searching",
  "message": "Looking for nearby drivers..."
}
```

**Response (Matched):**
```json
{
  "requestID": "user123_1692095400",
  "status": "matched",
  "autoID": "auto_456",
  "driver": {
    "name": "John Driver",
    "phone": "+919876543210",
    "vehicle": "TN 01 AB 1234"
  },
  "estimatedArrival": "3 minutes"
}
```

#### Accept Ride (Driver)
```http
POST /api/v1/rides/accept
Content-Type: application/json

{
  "autoID": "auto_456",
  "requestID": "user123_1692095400",
  "driverLocation": [30.355123, 76.363456]
}
```

#### Update Vehicle Location
```http
POST /api/v1/location/update
Content-Type: application/json

{
  "autoID": "auto_456",
  "location": [30.355123, 76.363456],
  "timestamp": "2024-08-15T10:30:00Z"
}
```

#### Get Vehicle Location
```http
GET /api/v1/location?autoID=auto_456
```

**Response:**
```json
{
  "autoID": "auto_456",
  "location": [30.355123, 76.363456],
  "lastUpdate": "2024-08-15T10:30:00Z",
  "status": "active"
}
```

## 🗄️ Data Models

### Ride Request
```go
type RideRequest struct {
    RequestID    string    `json:"requestID"`
    UserID       string    `json:"userID"`
    PickupPoint  []float64 `json:"pickup"`      // [lat, lng]
    SearchLevel  []Grid    `json:"level"`       // Grid coordinates
    Status       string    `json:"status"`      // searching, matched, completed, cancelled
    CreatedAt    time.Time `json:"createdAt"`
    MatchedAt    *time.Time `json:"matchedAt,omitempty"`
    AutoID       string    `json:"autoID,omitempty"`
}
```

### Grid Coordinate
```go
type Grid struct {
    X int `json:"x"`
    Y int `json:"y"`
}
```

### Vehicle Location
```go
type VehicleLocation struct {
    AutoID      string    `json:"autoID"`
    Location    []float64 `json:"location"`    // [lat, lng]
    Status      string    `json:"status"`      // active, inactive, busy
    LastUpdate  time.Time `json:"lastUpdate"`
    GridX       int       `json:"gridX"`
    GridY       int       `json:"gridY"`
}
```

### Driver Information
```go
type Driver struct {
    DriverID    string `json:"driverID"`
    Name        string `json:"name"`
    Phone       string `json:"phone"`
    VehicleNo   string `json:"vehicle"`
    Rating      float64 `json:"rating"`
    Status      string `json:"status"`     // online, offline, busy
}
```

## 🔧 Configuration

### Environment Variables
```go
// configs/envs.go
type Config struct {
    Port           string
    RedisHost      string
    RedisPort      string
    RedisPassword  string
    RedisDB        int
    MySQLHost      string
    MySQLPort      string
    MySQLUser      string
    MySQLPassword  string
    MySQLDatabase  string
    MaxSearchRadius int
    CleanupInterval int
    RequestTimeout  int
}
```

### Redis Configuration
```go
// Redis client setup
redisClient := redis.NewClient(&redis.Options{
    Addr:     fmt.Sprintf("%s:%s", config.RedisHost, config.RedisPort),
    Password: config.RedisPassword,
    DB:       config.RedisDB,
    PoolSize: 10,
    MinIdleConns: 5,
})
```

## 🎯 Ride Matching Algorithm

### Grid-based Spatial Partitioning
```go
// Convert latitude/longitude to grid coordinates
func latLngToGrid(lat, lng float64) (int, int) {
    // TIET Campus bounds
    const (
        minLat = 30.3501
        maxLat = 30.35875
        minLng = 76.35831
        maxLng = 76.37416
        gridSize = 0.001 // ~100 meters
    )
    
    x := int((lng - minLng) / gridSize)
    y := int((lat - minLat) / gridSize)
    
    return x, y
}
```

### Multi-level Search Strategy
1. **Level 0**: Exact grid match
2. **Level 1**: Adjacent grids (8 neighbors)
3. **Level 2**: Extended radius (24 neighbors)
4. **Level 3**: Campus-wide search

```go
// BFS-based grid expansion
func expandSearchGrid(centerX, centerY, level int) []Grid {
    var grids []Grid
    
    for dx := -level; dx <= level; dx++ {
        for dy := -level; dy <= level; dy++ {
            if abs(dx) == level || abs(dy) == level {
                grids = append(grids, Grid{
                    X: centerX + dx,
                    Y: centerY + dy,
                })
            }
        }
    }
    
    return grids
}
```

## ⚡ Performance Features

### Concurrent Request Handling
```go
// Goroutine-based request processing
func (h *RidesHandler) handleNewRide(w http.ResponseWriter, r *http.Request) {
    go func() {
        // Process ride request asynchronously
        h.processRideRequest(request)
    }()
    
    // Return immediate response
    w.WriteHeader(http.StatusAccepted)
}
```

### Redis Optimization
```go
// Pipeline operations for better performance
pipe := redisClient.Pipeline()
pipe.HSet(ctx, "ride:"+requestID, rideData)
pipe.Expire(ctx, "ride:"+requestID, 30*time.Minute)
pipe.SAdd(ctx, "active_requests", requestID)
_, err := pipe.Exec(ctx)
```

### Connection Pooling
```go
// Optimized connection pool settings
redisClient := redis.NewClient(&redis.Options{
    PoolSize:     20,
    MinIdleConns: 5,
    MaxRetries:   3,
    DialTimeout:  5 * time.Second,
    ReadTimeout:  3 * time.Second,
    WriteTimeout: 3 * time.Second,
})
```

## 🔄 Background Workers

### Cleanup Worker
```go
// Periodic cleanup of expired requests
func (w *Worker) StartCleanupWorker(intervalMinutes, maxAgeMinutes int) {
    ticker := time.NewTicker(time.Duration(intervalMinutes) * time.Minute)
    
    go func() {
        for {
            select {
            case <-ticker.C:
                w.cleanupExpiredRequests(maxAgeMinutes)
            }
        }
    }()
}
```

### Health Monitor
```go
// Continuous health monitoring
func (h *HealthHandler) monitorRedisHealth() {
    go func() {
        for {
            ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
            _, err := h.redis.Ping(ctx).Result()
            cancel()
            
            if err != nil {
                log.Printf("Redis health check failed: %v", err)
            }
            
            time.Sleep(30 * time.Second)
        }
    }()
}
```

## 🐳 Docker Configuration

### Multi-stage Dockerfile
```dockerfile
# Build stage
FROM golang:1.23 AS builder

WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o quinjet ./cmd

# Runtime stage
FROM alpine:latest

RUN apk --no-cache add ca-certificates tzdata
WORKDIR /root/

COPY --from=builder /app/quinjet .

EXPOSE 8080
CMD ["./quinjet"]
```

### Docker Compose Integration
```yaml
# docker-compose.yml
quinjet:
  build:
    context: ./quinjet
    dockerfile: quinjet.Dockerfile
  container_name: quinjet
  depends_on:
    redis:
      condition: service_healthy
  environment:
    REDIS_HOST: redis
    REDIS_PORT: 6379
  ports:
    - "8080:8080"
  healthcheck:
    test: ["CMD", "curl", "-f", "http://localhost:8080/api/v1/health/"]
    interval: 30s
    timeout: 10s
    retries: 3
```

## 🧪 Development

### Development Commands
```bash
# Run tests
go test ./...

# Run with race detection
go run -race cmd/main.go

# Build for production
go build -ldflags="-w -s" -o quinjet cmd/main.go

# Format code
go fmt ./...

# Vet code
go vet ./...

# Get dependencies
go mod tidy
```

### Testing
```bash
# Unit tests
go test ./internal/services/rides/

# Integration tests
go test -tags=integration ./...

# Benchmark tests
go test -bench=. ./...

# Coverage report
go test -cover ./...
```

## 🐛 Troubleshooting

### Common Issues

1. **Redis Connection Failed**
   ```bash
   # Check Redis status
   redis-cli ping
   
   # Check Redis logs
   docker logs redis
   
   # Verify connection string
   redis-cli -h localhost -p 6379
   ```

2. **High Memory Usage**
   ```bash
   # Monitor Redis memory
   redis-cli info memory
   
   # Check Go memory usage
   go tool pprof http://localhost:8080/debug/pprof/heap
   ```

3. **Request Timeouts**
   ```bash
   # Check Redis latency
   redis-cli --latency-history
   
   # Monitor active connections
   redis-cli info clients
   ```

4. **Grid Calculation Errors**
   ```bash
   # Verify campus bounds
   # minLat: 30.3501, maxLat: 30.35875
   # minLng: 76.35831, maxLng: 76.37416
   ```

### Performance Tuning
```go
// Optimize Redis operations
const (
    maxRetries = 3
    poolSize = 20
    minIdleConns = 5
    dialTimeout = 5 * time.Second
)

// Batch operations
pipe := client.Pipeline()
// ... add operations
pipe.Exec(ctx)
```

## 📊 Monitoring & Metrics

### Health Endpoints
```http
GET /api/v1/health/          # Overall health
GET /api/v1/health/redis     # Redis connectivity
GET /api/v1/health/detailed  # Detailed system info
```

### Performance Metrics
- **Request Latency**: Average response time for ride requests
- **Match Success Rate**: Percentage of successful ride matches
- **Redis Operations/sec**: Database operation throughput
- **Active Connections**: Current client connections
- **Memory Usage**: Application memory consumption

### Logging
```go
// Structured logging
log.Printf("Ride request created: requestID=%s, userID=%s, location=[%f,%f]", 
    request.RequestID, request.UserID, request.PickupPoint[0], request.PickupPoint[1])

log.Printf("Ride matched: requestID=%s, autoID=%s, matchTime=%dms", 
    request.RequestID, match.AutoID, matchDuration.Milliseconds())
```

## 🔄 Integration with Other Services

### Backend API Integration
```bash
# Health check from backend
curl http://quinjet:8080/api/v1/health/

# Create ride request from frontend
curl -X POST http://quinjet:8080/api/v1/rides/new \
  -H "Content-Type: application/json" \
  -d '{"requestID":"user123","level":[{"x":10,"y":15}],"pickup":[30.354,76.362]}'
```

### Redis Data Flow
```
Frontend → Backend → Quinjet → Redis
    ↓         ↓         ↓        ↓
   UI    → Auth     → Rides   → Cache
```

## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Follow Go conventions**
   - Use `gofmt` for formatting
   - Follow effective Go guidelines
   - Add comprehensive tests
   - Document public functions

4. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
5. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
6. **Open a Pull Request**

### Code Quality Guidelines
- Write idiomatic Go code
- Use meaningful variable and function names
- Add comprehensive error handling
- Include unit tests for new features
- Update documentation for API changes

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
  <p>🚀 Lightning-Fast Ride Matching! ⚡</p>
</div>
