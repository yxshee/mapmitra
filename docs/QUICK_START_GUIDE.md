# 🚀 MapMitra - Quick Start Guide

## ⚡ Get Started in 5 Minutes

### 🐳 Docker Method (Easiest)

```bash
# 1. Clone the repository
git clone git@github.com:yxshee/mapmitra.git && cd mapmitra

# 2. Start all services
docker-compose up -d

# 3. Open your browser
# Frontend: http://localhost:5173
# Redis GUI: http://localhost:8001
```

That's it! All services are running. 🎉

---

## 📦 What's Running?

| Service | Port | Purpose | Status Check |
|---------|------|---------|--------------|
| **Frontend** | 5173 | React UI | Open http://localhost:5173 |
| **Backend** | 5000 | Node.js API | `curl http://localhost:5000/api/health` |
| **Routing Backend** | 5000 | Python API | `curl http://localhost:5000/docs` |
| **Quinjet** | 8080 | Go Tracking | `curl http://localhost:8080/api/v1/health` |
| **GraphHopper** | 8989 | Routing | `curl http://localhost:8989/health` |
| **Redis** | 6379 | Cache | `redis-cli ping` |
| **Redis GUI** | 8001 | Stack UI | Open http://localhost:8001 |

---

## 🛠️ Manual Setup (Development)

### Prerequisites
- Node.js 18+
- Python 3.9+
- Go 1.23+
- MongoDB (local or Atlas)
- Redis (local or cloud)

### Frontend
```bash
cd frontend
npm install
npm run dev
# Runs on http://localhost:5173
```

### Backend
```bash
cd backend

# Create .env file
cat > .env << EOF
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
CLIENT_URL=http://localhost:3000
EOF

npm install
npm run dev
# Runs on http://localhost:5000
```

### Routing Backend
```bash
cd routing-backend/api

# Create .env file
echo "GRAPHHOPPER_BASE_URL=http://localhost:8989/route" > .env

pip install pipenv
pipenv install
pipenv run python app.py
# Runs on http://localhost:5000
```

### Quinjet
```bash
cd quinjet

# Create .env file
cat > .env << EOF
REDIS_HOST=localhost
REDIS_PORT=6379
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASSWORD=password
MYSQL_DATABASE=mapmitra
EOF

go mod download
go run cmd/main.go
# Runs on http://localhost:8080
```

---

## 🗺️ Technology Stack at a Glance

```
Frontend:   React + Vite + TailwindCSS + Leaflet
Backend:    Node.js + Express + MongoDB + Passport
Tracking:   Go + WebSocket + Redis
Routing:    Python + FastAPI + GeoPandas + GraphHopper
DevOps:     Docker + Docker Compose
```

---

## 🎯 Key Features to Test

### 1. Map Navigation
- Open http://localhost:5173
- Click on the map to set destination
- View landmark-based directions

### 2. Real-Time Tracking
- Admin panel: http://localhost:5173/admin
- See live e-rickshaw positions
- Monitor driver status

### 3. Authentication
- Click "Login with Google"
- Or register with email/password
- View saved locations in profile

---

## 📁 Project Structure Overview

```
mapmitra/
├── frontend/          # React app (Vite + TailwindCSS)
├── backend/           # Node.js API (Express + MongoDB)
├── quinjet/           # Go tracking service (WebSocket + Redis)
├── routing-backend/   # Python routing (FastAPI + GraphHopper)
└── docker-compose.yml # All services orchestration
```

---

## 🔧 Common Commands

### Docker
```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f [service-name]

# Stop all services
docker-compose down

# Rebuild after code changes
docker-compose up -d --build

# View running containers
docker-compose ps
```

### Development
```bash
# Frontend
npm run dev          # Start dev server
npm run build        # Production build
npm run preview      # Preview production build

# Backend (Node.js)
npm run dev          # Start with nodemon
npm start            # Production start

# Routing Backend (Python)
pipenv run python app.py    # Start FastAPI
pipenv run pytest           # Run tests

# Quinjet (Go)
go run cmd/main.go   # Start server
go test ./...        # Run tests
```

---

## 🐛 Troubleshooting

### Frontend doesn't connect to backend
```bash
# Check CORS settings in backend/.env
CLIENT_URL=http://localhost:5173

# Restart backend
cd backend && npm run dev
```

### GraphHopper not responding
```bash
# Check GraphHopper health
curl http://localhost:8989/health

# Restart service
docker-compose restart graphhopper

# View logs
docker-compose logs graphhopper
```

### Redis connection failed
```bash
# Check Redis is running
docker-compose ps redis

# Test connection
docker exec -it redis redis-cli ping
# Should respond: PONG

# Restart Redis
docker-compose restart redis
```

### MongoDB connection error
```bash
# Verify MONGO_URI in backend/.env
# For local MongoDB:
MONGO_URI=mongodb://localhost:27017/mapmitra

# For MongoDB Atlas:
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/mapmitra
```

---

## 📡 API Testing

### Test Backend API
```bash
# Health check
curl http://localhost:5000/api/health

# Register user
curl -X POST http://localhost:5000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "fullName": "Test User",
    "email": "test@example.com",
    "password": "test123"
  }'
```

### Test Routing Backend
```bash
# Get route with landmark instructions
curl -X POST http://localhost:5000/route_instructions \
  -H "Content-Type: application/json" \
  -d '{
    "start_coordinates": [30.3549, 76.3644],
    "end_coordinates": [30.3565, 76.3658]
  }'

# View API documentation
open http://localhost:5000/docs
```

### Test Quinjet
```bash
# Health check
curl http://localhost:8080/api/v1/health

# Get all rickshaws
curl http://localhost:8080/api/v1/rickshaws
```

---

## 🌐 Environment Files Checklist

### ✅ Backend (.env)
- [x] PORT
- [x] MONGO_URI
- [x] JWT_SECRET
- [x] GOOGLE_CLIENT_ID
- [x] GOOGLE_CLIENT_SECRET
- [x] CLIENT_URL

### ✅ Routing Backend (.env)
- [x] GRAPHHOPPER_BASE_URL

### ✅ Quinjet (.env)
- [x] REDIS_HOST
- [x] REDIS_PORT
- [x] MYSQL_HOST
- [x] MYSQL_USER
- [x] MYSQL_PASSWORD
- [x] MYSQL_DATABASE

---

## 📚 Additional Resources

- **Full Documentation**: See [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md)
- **API Documentation**: http://localhost:5000/docs (FastAPI)
- **GraphHopper Docs**: https://docs.graphhopper.com/
- **Leaflet Docs**: https://leafletjs.com/reference.html
- **React Router**: https://reactrouter.com/

---

## 🔐 Default Credentials (Development)

**Note**: These should be changed in production!

- **Admin Panel**: Set up during first run
- **MongoDB**: No auth (local development)
- **Redis**: No auth (local development)
- **Google OAuth**: Configure in Google Cloud Console

---

## 🚦 Development Workflow

1. **Start Services**: `docker-compose up -d`
2. **Check Status**: `docker-compose ps`
3. **View Logs**: `docker-compose logs -f [service]`
4. **Make Changes**: Edit code in your IDE
5. **Rebuild**: `docker-compose up -d --build [service]`
6. **Test**: Open http://localhost:5173
7. **Stop**: `docker-compose down`

---

## 📊 Performance Tips

- **Frontend**: Use React DevTools to check component renders
- **Backend**: Enable DEBUG logging in .env
- **Database**: Add indexes for frequent queries
- **Redis**: Monitor cache hit rate at http://localhost:8001
- **GraphHopper**: Check response times in logs

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/name`
3. Make changes and test thoroughly
4. Commit: `git commit -m 'Add feature'`
5. Push: `git push origin feature/name`
6. Open Pull Request

---

## 💡 Quick Tips

- **Hot Reload**: Both frontend and backend support hot reload in dev mode
- **Database GUI**: Use MongoDB Compass for MongoDB
- **Redis GUI**: Access at http://localhost:8001
- **API Testing**: Use Postman or Thunder Client (VS Code)
- **Debugging**: Use VS Code debugger with launch.json

---

## 📞 Need Help?

- **Issues**: [GitHub Issues](https://github.com/yxshee/mapmitra/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yxshee/mapmitra/discussions)
- **Documentation**: Read [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md)

---

**🎉 Happy Coding! Made with ❤️ by TIET Students**
