# 🛣️ MapMitra Routing Backend

A powerful Python-based routing and navigation service that provides landmark-aware turn-by-turn directions for the MapMitra smart campus navigation system. Built with FastAPI and integrated with GraphHopper for optimal route calculation.

## 📋 Overview

The routing backend serves as the intelligent navigation engine for MapMitra, transforming standard GPS coordinates into landmark-aware directions that are meaningful for campus navigation. It integrates with GraphHopper for route calculation and enhances the instructions with nearby landmark information to provide intuitive, human-readable directions.

## ✨ Features

### 🗺️ Smart Route Calculation
- **GraphHopper Integration**: Leverages industry-standard routing engine
- **Campus-Optimized Routes**: Tailored for TIET campus navigation
- **Pedestrian-Focused**: Optimized for walking routes and pathways
- **Multi-point Routing**: Support for waypoints and complex routes

### 🏛️ Landmark-Aware Navigation
- **GeoJSON Landmark Data**: Rich campus landmark database
- **Proximity-Based References**: Directions using nearby landmarks
- **Contextual Instructions**: Human-readable, location-specific guidance
- **Cultural Relevance**: Campus-specific landmark references

### 🚶 Pedestrian-Optimized Directions
- **Walking-Specific Routes**: Optimized for pedestrian movement
- **Turn-by-Turn Instructions**: Detailed step-by-step guidance
- **Distance-Aware Messaging**: Appropriate distance measurements
- **Natural Language Processing**: Human-friendly instruction generation

### 🚀 High-Performance API
- **FastAPI Framework**: Modern, fast, and automatically documented API
- **Async Processing**: Non-blocking request handling
- **CORS Support**: Cross-origin resource sharing for web integration
- **RESTful Design**: Standard HTTP methods and status codes

## 🛠️ Tech Stack

### Core Technologies
![Python](https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white&style=flat-square)
![FastAPI](https://img.shields.io/badge/-FastAPI-009688?logo=fastapi&logoColor=white&style=flat-square)
![GraphHopper](https://img.shields.io/badge/-GraphHopper-2E8B57?style=flat-square)

### Geospatial & Data Processing
![GeoPandas](https://img.shields.io/badge/-GeoPandas-139C5A?style=flat-square)
![Shapely](https://img.shields.io/badge/-Shapely-3776AB?style=flat-square)
![OpenStreetMap](https://img.shields.io/badge/-OpenStreetMap-7EBC6F?logo=openstreetmap&logoColor=white&style=flat-square)

### Web & API
![Uvicorn](https://img.shields.io/badge/-Uvicorn-499848?style=flat-square)
![Requests](https://img.shields.io/badge/-Requests-3776AB?style=flat-square)
![Pydantic](https://img.shields.io/badge/-Pydantic-E92063?style=flat-square)

## 📦 Dependencies

### Core Dependencies (Pipfile)
```toml
[packages]
geopandas = "*"
shapely = "*" 
requests = "*"
fastapi = {extras = ["standard"], version = "*"}

[requires]
python_version = "3.12"
```

### Expanded Dependencies
```python
# Core API Framework
fastapi[standard]>=0.104.0
uvicorn[standard]>=0.24.0
pydantic>=2.5.0

# Geospatial Libraries
geopandas>=0.14.0
shapely>=2.0.0
pyproj>=3.6.0

# HTTP and Data Processing
requests>=2.31.0
numpy>=1.24.0
pandas>=2.1.0

# Development Dependencies
pytest>=7.4.0
pytest-asyncio>=0.21.0
black>=23.0.0
flake8>=6.0.0
```

## 🚀 Quick Start

### Prerequisites
- **Python**: Version 3.12 or higher
- **pipenv**: For dependency management
- **GraphHopper**: Local instance or containerized deployment
- **Docker**: For containerized deployment (optional)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yxshee/mapmitra.git
   cd mapmitra/routing-backend/api
   ```

2. **Install dependencies with pipenv**
   ```bash
   # Install pipenv if not already installed
   pip install pipenv
   
   # Install project dependencies
   pipenv install
   
   # For development dependencies
   pipenv install --dev
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```
   
   Configure the following variables:
   ```env
   # GraphHopper Configuration
   GRAPHHOPPER_BASE_URL=http://localhost:8989/route
   
   # Server Configuration
   HOST=0.0.0.0
   PORT=5000
   
   # Development Settings
   DEBUG=True
   RELOAD=True
   
   # CORS Settings
   CORS_ORIGINS=["http://localhost:3000", "http://localhost:5173"]
   
   # Logging
   LOG_LEVEL=INFO
   ```

4. **Prepare landmark data**
   ```bash
   # Ensure thaparMap.geojson is in the correct location
   ls thaparMap.geojson
   ```

5. **Start GraphHopper (if not using Docker)**
   ```bash
   # Download and start GraphHopper with campus map
   java -jar graphhopper-web-*.jar --input thapar_map.osm
   ```

6. **Start the development server**
   ```bash
   # Using pipenv
   pipenv run python app.py
   
   # Or activate shell and run
   pipenv shell
   python app.py
   ```

   The service will be available at `http://localhost:5000`

### Docker Deployment

```bash
# Build the container
docker build -f api.Dockerfile -t routing-backend .

# Run the container
docker run -p 5000:5000 --env-file .env routing-backend

# Or use with docker-compose (from project root)
docker-compose up routing-backend
```

## 📁 Project Structure

```
routing-backend/
├── api/                      # Main API application
│   ├── app.py               # FastAPI application entry point
│   ├── landmark.py          # Landmark processing utilities
│   ├── thaparMap.geojson   # Campus landmark data
│   ├── Pipfile             # Pipenv dependencies
│   ├── Pipfile.lock        # Locked dependency versions
│   └── api.Dockerfile      # Docker build configuration
├── graphhopper/            # GraphHopper configuration
│   ├── config.yml         # GraphHopper server configuration
│   └── thapar_map.osm     # OpenStreetMap data for campus
└── README.md              # This documentation
```

## 🌐 API Endpoints

### Route Instructions

#### POST `/route_instructions`

Generate landmark-aware turn-by-turn directions between two points.

**Request Body:**
```json
{
  "start_coordinates": [30.354123, 76.362456],
  "end_coordinates": [30.356789, 76.365123]
}
```

**Response:**
```json
{
  "routePath": [
    [76.362456, 30.354123],
    [76.362500, 30.354200],
    [76.362600, 30.354350],
    [76.365123, 30.356789]
  ],
  "routeInstructions": [
    {
      "coordinate": {
        "latitude": 30.354123,
        "longitude": 76.362456
      },
      "instruction": "Continue straight towards Main Building for 150m."
    },
    {
      "coordinate": {
        "latitude": 30.354500,
        "longitude": 76.363000
      },
      "instruction": "Turn right, continue straight towards Library for 200m."
    },
    {
      "coordinate": {
        "latitude": 30.356789,
        "longitude": 76.365123
      },
      "instruction": "Arrived at Computer Science Block."
    }
  ]
}
```

### Health Check

#### GET `/health`
```json
{
  "status": "healthy",
  "timestamp": "2024-08-15T10:30:00Z",
  "graphhopper_status": "connected",
  "landmarks_loaded": true
}
```

### API Documentation

#### GET `/docs`
Interactive Swagger UI documentation

#### GET `/redoc`
ReDoc API documentation

## 🗺️ Landmark Processing

### GeoJSON Data Structure
```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "name": "Main Building",
        "type": "academic",
        "description": "Administrative and academic building"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [76.362456, 30.354123]
      }
    }
  ]
}
```

### Landmark Search Algorithm
```python
def find_nearby_landmarks(lat, lng, radius=50):
    """
    Find landmarks within specified radius of a point
    
    Args:
        lat (float): Latitude of search point
        lng (float): Longitude of search point
        radius (int): Search radius in meters
        
    Returns:
        list: Nearby landmarks with distance information
    """
    point = gpd.GeoSeries([Point(lng, lat)], crs="EPSG:4326")
    point = point.to_crs(landmarks.crs)
    
    nearby = landmarks[landmarks.geometry.distance(point.iloc[0]) <= radius]
    
    return [
        {
            "name": landmark.get("name", "Unknown Landmark"),
            "distance": landmark.geometry.distance(point.iloc[0]),
            "type": landmark.get("type", "general")
        }
        for _, landmark in nearby.iterrows()
        if landmark.get("name") is not None
    ]
```

### Instruction Enhancement
```python
def enhance_instruction(instruction_text, landmark_name, distance, turn_angle=None):
    """
    Convert basic routing instruction to landmark-aware instruction
    
    Args:
        instruction_text (str): Original GraphHopper instruction
        landmark_name (str): Nearby landmark name
        distance (float): Distance to travel
        turn_angle (float, optional): Turn angle in radians
        
    Returns:
        str: Enhanced human-readable instruction
    """
    if instruction_text.lower() == "continue":
        return f"Continue straight towards {landmark_name} for {distance:.0f}m."
    
    elif "turn" in instruction_text.lower():
        direction = "left" if "left" in instruction_text.lower() else "right"
        return f"Turn {direction}, continue straight towards {landmark_name} for {distance:.0f}m."
    
    elif instruction_text.lower() == "arrive at destination":
        return f"Arrived at {landmark_name}."
    
    else:
        return f"Head towards {landmark_name} for {distance:.0f}m."
```

## 🔧 Configuration

### GraphHopper Configuration
```yaml
# graphhopper/config.yml
graphhopper:
  datareader.file: thapar_map.osm
  graph.location: ./graph-cache
  
  profiles:
    - name: foot
      vehicle: foot
      weighting: fastest
      
  profiles_ch:
    - profile: foot
    
server:
  application_connectors:
    - type: http
      port: 8989
      bind_host: 0.0.0.0
```

### FastAPI Configuration
```python
# App configuration
app = FastAPI(
    title="MapMitra Routing API",
    description="Landmark-aware routing for campus navigation",
    version="1.0.0",
    docs_url="/docs",
    redoc_url="/redoc"
)

# CORS configuration
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Configure based on deployment
    allow_credentials=True,
    allow_methods=["GET", "POST"],
    allow_headers=["*"],
)
```

### Environment Configuration
```python
import os
from pydantic import BaseSettings

class Settings(BaseSettings):
    graphhopper_base_url: str = "http://localhost:8989/route"
    host: str = "0.0.0.0"
    port: int = 5000
    debug: bool = False
    reload: bool = False
    log_level: str = "INFO"
    
    class Config:
        env_file = ".env"

settings = Settings()
```

## 🧮 Geospatial Processing

### Coordinate System Handling
```python
# Load and transform coordinate systems
landmarks = gpd.read_file("thaparMap.geojson")

# Ensure landmarks use projected CRS for accurate distance calculations
if landmarks.crs.is_geographic:
    landmarks = landmarks.to_crs(epsg=3857)  # Web Mercator
```

### Distance Calculation
```python
from shapely.geometry import Point

def calculate_distance(point1, point2, crs="EPSG:4326"):
    """
    Calculate distance between two points
    
    Args:
        point1 (tuple): (lat, lng) of first point
        point2 (tuple): (lat, lng) of second point
        crs (str): Coordinate reference system
        
    Returns:
        float: Distance in meters
    """
    p1 = gpd.GeoSeries([Point(point1[1], point1[0])], crs=crs)
    p2 = gpd.GeoSeries([Point(point2[1], point2[0])], crs=crs)
    
    # Convert to projected CRS for accurate distance
    p1_proj = p1.to_crs(epsg=3857)
    p2_proj = p2.to_crs(epsg=3857)
    
    return p1_proj.distance(p2_proj).iloc[0]
```

### Campus Boundary Validation
```python
# TIET Campus boundaries
CAMPUS_BOUNDS = {
    "min_lat": 30.3501,
    "max_lat": 30.35875,
    "min_lng": 76.35831,
    "max_lng": 76.37416
}

def is_within_campus(lat, lng):
    """Check if coordinates are within campus bounds"""
    return (CAMPUS_BOUNDS["min_lat"] <= lat <= CAMPUS_BOUNDS["max_lat"] and
            CAMPUS_BOUNDS["min_lng"] <= lng <= CAMPUS_BOUNDS["max_lng"])
```

## 🚀 Performance Optimization

### Async Processing
```python
import asyncio
import aiofiles
from concurrent.futures import ThreadPoolExecutor

# Async landmark processing
async def process_route_async(route_data):
    """Process route data asynchronously"""
    with ThreadPoolExecutor() as executor:
        tasks = []
        for instruction in route_data["paths"][0]["instructions"]:
            task = asyncio.get_event_loop().run_in_executor(
                executor, process_instruction, instruction
            )
            tasks.append(task)
        
        results = await asyncio.gather(*tasks)
        return results
```

### Caching Strategy
```python
from functools import lru_cache

@lru_cache(maxsize=1000)
def get_nearest_landmark(lat, lng, radius=50):
    """Cache frequently requested landmark lookups"""
    return find_nearby_landmarks(lat, lng, radius)

# Clear cache periodically if landmark data updates
def clear_landmark_cache():
    get_nearest_landmark.cache_clear()
```

### Memory Optimization
```python
# Optimize GeoPandas operations
landmarks = landmarks[['name', 'type', 'geometry']]  # Keep only needed columns
landmarks = landmarks.dropna(subset=['name'])  # Remove unnamed landmarks
landmarks.spatial_index  # Build spatial index for faster queries
```

## 🐳 Docker Configuration

### Multi-stage Dockerfile
```dockerfile
FROM python:3.12-slim AS base

# Setup env
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONFAULTHANDLER 1

FROM base AS python-deps

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    g++ \
    libgeos-dev \
    libproj-dev \
    libgdal-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
RUN pip install pipenv
COPY Pipfile .
COPY Pipfile.lock .
RUN PIPENV_VENV_IN_PROJECT=1 pipenv install --deploy

FROM base AS runtime

# Copy virtual environment
COPY --from=python-deps /.venv /.venv
ENV PATH="/.venv/bin:$PATH"

# Create non-root user
RUN useradd --create-home appuser
WORKDIR /home/appuser
USER appuser

# Copy application code
COPY . .

EXPOSE 5000

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:5000/health || exit 1

# Run the application
ENTRYPOINT ["python", "app.py"]
```

### Docker Compose Integration
```yaml
# From docker-compose.yml
routing-backend:
  build:
    context: ./routing-backend/api
    dockerfile: api.Dockerfile
  container_name: routing-backend
  depends_on:
    graphhopper:
      condition: service_healthy
  environment:
    GRAPHHOPPER_BASE_URL: http://graphhopper:8989/route
  ports:
    - "5000:5000"
  volumes:
    - ./routing-backend/api/thaparMap.geojson:/home/appuser/thaparMap.geojson:ro
  healthcheck:
    test: ["CMD", "curl", "-f", "http://localhost:5000/health"]
    interval: 30s
    timeout: 10s
    retries: 3
```

## 🧪 Development

### Development Commands
```bash
# Start development server with auto-reload
pipenv run python app.py

# Run with custom host/port
pipenv run uvicorn app:app --host 0.0.0.0 --port 5000 --reload

# Run tests
pipenv run pytest

# Format code
pipenv run black .

# Lint code
pipenv run flake8

# Install new package
pipenv install new-package

# Install development package
pipenv install --dev pytest
```

### Testing
```python
# tests/test_routing.py
import pytest
from fastapi.testclient import TestClient
from app import app

client = TestClient(app)

def test_route_instructions():
    response = client.post("/route_instructions", json={
        "start_coordinates": [30.354123, 76.362456],
        "end_coordinates": [30.356789, 76.365123]
    })
    
    assert response.status_code == 200
    data = response.json()
    assert "routePath" in data
    assert "routeInstructions" in data
    assert len(data["routeInstructions"]) > 0

def test_invalid_coordinates():
    response = client.post("/route_instructions", json={
        "start_coordinates": [0, 0],  # Invalid campus coordinates
        "end_coordinates": [30.356789, 76.365123]
    })
    
    assert response.status_code == 422  # Validation error
```

### Environment Setup for Development
```bash
# Create development environment
pipenv install --dev

# Activate shell
pipenv shell

# Set development environment variables
export DEBUG=True
export RELOAD=True
export LOG_LEVEL=DEBUG

# Start with auto-reload
python app.py
```

## 🐛 Troubleshooting

### Common Issues

1. **GraphHopper Connection Failed**
   ```bash
   # Check GraphHopper status
   curl http://localhost:8989/health
   
   # Check GraphHopper logs
   docker logs graphhopper
   
   # Verify network connectivity
   docker network ls
   docker network inspect mapmitra_default
   ```

2. **Landmark Data Not Loading**
   ```bash
   # Check file exists
   ls -la thaparMap.geojson
   
   # Validate GeoJSON format
   python -c "import geopandas as gpd; print(gpd.read_file('thaparMap.geojson').head())"
   
   # Check file permissions
   chmod 644 thaparMap.geojson
   ```

3. **Memory Issues with GeoPandas**
   ```bash
   # Monitor memory usage
   docker stats routing-backend
   
   # Optimize GeoPandas operations
   # Use smaller radius for landmark search
   # Limit number of features loaded
   ```

4. **CORS Errors**
   ```python
   # Update CORS settings in app.py
   app.add_middleware(
       CORSMiddleware,
       allow_origins=["http://localhost:3000", "http://localhost:5173"],
       allow_credentials=True,
       allow_methods=["GET", "POST"],
       allow_headers=["*"],
   )
   ```

### Performance Tuning
```python
# Optimize landmark search
LANDMARK_SEARCH_RADIUS = 100  # meters
MAX_LANDMARKS_PER_INSTRUCTION = 1

# Optimize GeoPandas
import geopandas as gpd
gpd.options.use_pygeos = True  # Use faster geometry operations

# Memory optimization
import gc
gc.collect()  # Force garbage collection after heavy operations
```

## 📊 Monitoring & Logging

### Health Monitoring
```python
import psutil
import time

@app.get("/health")
async def health_check():
    # Check GraphHopper connectivity
    try:
        response = requests.get(f"{GRAPHHOPPER_BASE_URL.replace('/route', '/health')}")
        graphhopper_status = "connected" if response.status_code == 200 else "disconnected"
    except:
        graphhopper_status = "disconnected"
    
    return {
        "status": "healthy",
        "timestamp": datetime.utcnow().isoformat(),
        "graphhopper_status": graphhopper_status,
        "landmarks_loaded": len(landmarks) > 0,
        "memory_usage": psutil.virtual_memory().percent,
        "cpu_usage": psutil.cpu_percent()
    }
```

### Logging Configuration
```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('routing.log'),
        logging.StreamHandler()
    ]
)

logger = logging.getLogger(__name__)

# Log route requests
logger.info(f"Route request: {start_coordinates} -> {end_coordinates}")
logger.info(f"Route calculated: {len(route_instructions)} instructions, {total_distance}m")
```

## 🔄 Integration with Other Services

### Frontend Integration
```javascript
// Frontend API call
const response = await fetch('http://localhost:5000/route_instructions', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    start_coordinates: [30.354123, 76.362456],
    end_coordinates: [30.356789, 76.365123]
  })
});

const data = await response.json();
```

### GraphHopper Integration
```python
# GraphHopper API call
request_body = {
    "points": [
        [start_coordinates[1], start_coordinates[0]],  # [lng, lat]
        [end_coordinates[1], end_coordinates[0]]
    ],
    "profile": "foot",
    "instructions": True,
    "locale": "en_US",
    "points_encoded": False,
    "snap_preventions": ["ferry"]
}

response = requests.post(GRAPHHOPPER_BASE_URL, json=request_body)
route_data = response.json()
```

## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Set up development environment**
   ```bash
   pipenv install --dev
   pipenv shell
   ```
4. **Follow Python conventions**
   - Use Black for code formatting
   - Follow PEP 8 style guidelines
   - Add type hints where appropriate
   - Write comprehensive docstrings

5. **Write tests**
   ```bash
   # Add tests for new features
   pipenv run pytest tests/
   ```

6. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
7. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
8. **Open a Pull Request**

### Code Quality Guidelines
- Use type hints for function parameters and return values
- Write comprehensive docstrings for all functions
- Add unit tests for new functionality
- Follow FastAPI best practices
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
  <p>🛣️ Smart Navigation, Landmark-Aware Directions! 🗺️</p>
</div>
