# 📖 MapMitra - Documentation Index

Welcome to the complete documentation for **MapMitra** - A Smart Campus Navigation System! 🗺️

---

## 📚 Documentation Structure

We've created comprehensive documentation organized into multiple files for easy navigation:

### 1. 📘 [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md) - **Main Documentation**
**Read this first!** Complete technical documentation covering:
- 🎯 Project Overview & Features
- 🏗️ System Architecture (with diagrams)
- 🛠️ Complete Technology Stack
- 📁 Detailed Project Structure
- 🔧 Core Components Breakdown
- 🔄 Data Flow Explanations
- ⚙️ How Everything Works
- 📡 API Documentation
- 🐳 Deployment Guide
- 🔐 Security Considerations

**Best for**: Understanding the complete system, architecture decisions, and technical details

---

### 2. 🚀 [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md) - **Get Running Fast**
Quick reference for developers to get started:
- ⚡ 5-minute setup with Docker
- 📦 Manual installation steps
- 🛠️ Common commands
- 🐛 Troubleshooting tips
- 📊 Port reference
- 🧪 API testing examples

**Best for**: New developers joining the project, quick setup, debugging

---

### 3. 🛠️ [TECHNOLOGY_STACK.md](./TECHNOLOGY_STACK.md) - **Tech Deep Dive**
Detailed explanation of every technology:
- Why each technology was chosen
- Alternatives considered
- How it's used in the project
- Code examples and configurations
- Performance characteristics
- Best practices

**Best for**: Understanding technology decisions, learning about the stack, onboarding

---

### 4. 📋 [README.md](./README.md) - **Project Overview**
Quick project introduction:
- Feature highlights
- Tech stack badges
- Quick start commands
- Team information
- License details

**Best for**: First-time visitors, GitHub landing page

---

## 🖼️ Visual Documentation

### Architecture Diagrams

#### 1. **System Architecture Diagram**
![MapMitra Architecture](/.gemini/antigravity/brain/c4cc1015-0f87-47c6-a21f-486b7773d803/mapmitra_architecture_diagram_1768398958609.png)

Shows the complete system with:
- Frontend (React + Vite + Leaflet)
- Backend Services (Node.js, Go, Python)
- Data Layer (MongoDB, Redis, GraphHopper)
- Communication protocols

---

#### 2. **Data Flow Diagram**
![Data Flow](/.gemini/antigravity/brain/c4cc1015-0f87-47c6-a21f-486b7773d803/mapmitra_data_flow_1768399049681.png)

Illustrates two main workflows:
- **Navigation Flow**: User → Frontend → Routing Backend → GraphHopper
- **Real-time Tracking**: Driver → Quinjet → Redis → Users

---

#### 3. **Technology Stack Visualization**
![Tech Stack](/.gemini/antigravity/brain/c4cc1015-0f87-47c6-a21f-486b7773d803/tech_stack_overview_1768399216844.png)

Four-layer stack visualization:
- Layer 1: Frontend (React, Vite, Tailwind, Leaflet)
- Layer 2: Backend Services (Node.js, Go, Python)
- Layer 3: Data Layer (MongoDB, Redis, GraphHopper)
- Layer 4: Infrastructure (Docker, Docker Compose)

---

## 🎯 Quick Navigation by Task

### I want to...

#### 🚀 Get Started Quickly
→ Read: [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md)  
→ Run: `docker-compose up -d`

#### 📖 Understand the Architecture
→ Read: [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md) - Section 2  
→ View: System Architecture Diagram (above)

#### 🛠️ Learn About a Specific Technology
→ Read: [TECHNOLOGY_STACK.md](./TECHNOLOGY_STACK.md)  
→ Find your technology in the detailed breakdown

#### 🔧 Add a New Feature
→ Read: [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md) - Core Components  
→ Review: Data Flow section for integration points

#### 🐛 Debug an Issue
→ Check: [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md) - Troubleshooting  
→ Run: `docker-compose logs -f [service-name]`

#### 📡 Test APIs
→ Read: [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md) - API Documentation  
→ Visit: http://localhost:5000/docs (FastAPI Swagger)

#### 🐳 Deploy the Application
→ Read: [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md) - Deployment  
→ Review: docker-compose.yml configuration

---

## 📊 Project Statistics

```
Total Services:        7
  - Frontend:         1 (React)
  - Backend APIs:     3 (Node.js, Go, Python)  
  - Databases:        2 (MongoDB, Redis)
  - Routing Engine:   1 (GraphHopper)

Lines of Code:         ~15,000+
  - Frontend:         ~5,000
  - Backend:          ~3,000
  - Quinjet:          ~2,000
  - Routing Backend:  ~1,000
  - Config/Docker:    ~500

Technologies Used:     25+
  - Languages:        4 (JavaScript, Python, Go, SQL)
  - Frameworks:       6 (React, Express, FastAPI, etc.)
  - Libraries:        15+ (Leaflet, Mongoose, Redis, etc.)
  - Tools:            5+ (Vite, Docker, GraphHopper, etc.)

Database Collections:  3
  - Users
  - Sessions  
  - Rides (in MySQL for Quinjet)

API Endpoints:         15+
  - Auth:             5
  - User:             4
  - Routing:          2
  - Tracking:         4
```

---

## 🏗️ Architecture Overview (Quick Reference)

### Service Architecture
```
┌─────────────────────────────────────────────────────────┐
│                    FRONTEND (React)                      │
│  http://localhost:5173                                   │
└───────────────┬─────────────────────────────────────────┘
                │
        ┌───────┼───────┬────────────────┐
        ▼       ▼       ▼                ▼
    ┌──────┐ ┌────────┐ ┌──────────┐ ┌────────┐
    │Node.js│ │Quinjet│ │ Routing  │ │Graphics│
    │  API  │ │  (Go) │ │ (Python) │ │Hopper │
    │ :5000 │ │ :8080 │ │  :5000   │ │ :8989 │
    └───┬──┘ └───┬────┘ └────┬─────┘ └────────┘
        │        │            │
        ▼        ▼            ▼
    ┌────────┐ ┌──────┐   (GraphHopper)
    │MongoDB │ │Redis │
    │ :27017 │ │:6379 │
    └────────┘ └──────┘
```

### Data Flow Summary

**Navigation Request**:
```
User → Frontend → Routing Backend → GraphHopper
                ↓                        ↓
            Display Route  ←  Landmark Augmentation
```

**Real-time Tracking**:
```
Driver App → Quinjet (WebSocket) → Redis (Cache)
                        ↓              ↓
                   All Users  ← Broadcast Update
```

**Authentication**:
```
User → Frontend → Backend API → MongoDB
                     ↓
                  JWT Token → Cookie → Authenticated Session
```

---

## 🔑 Key Technologies Summary

| Layer | Primary Tech | Purpose | Alternative |
|-------|-------------|---------|-------------|
| **Frontend** | React 18.3 | UI Framework | Vue, Angular |
| **Build Tool** | Vite 5.4 | Fast bundler | Webpack, Parcel |
| **Styling** | TailwindCSS | Utility CSS | Bootstrap, MUI |
| **Maps** | Leaflet 1.9 | Map rendering | Google Maps, Mapbox |
| **Backend API** | Node.js 18 + Express | REST API | Django, Spring |
| **Tracking Service** | Go 1.23 | Real-time WS | Node.js, Rust |
| **Routing Service** | Python + FastAPI | Route calc | Node.js, Go |
| **Database** | MongoDB | User data | PostgreSQL, MySQL |
| **Cache** | Redis | Real-time data | Memcached, Hazelcast |
| **Routing Engine** | GraphHopper | Path finding | OSRM, Valhalla |
| **Auth** | JWT + Passport | Authentication | Auth0, Firebase |
| **Deployment** | Docker Compose | Orchestration | Kubernetes, Swarm |

---

## 📁 File Structure Quick Reference

```
mapmitra/
├── 📄 Documentation
│   ├── README.md                      # Project overview
│   ├── PROJECT_DOCUMENTATION.md       # Complete technical docs
│   ├── QUICK_START_GUIDE.md          # Setup guide
│   ├── TECHNOLOGY_STACK.md           # Tech explanations
│   └── DOCUMENTATION_INDEX.md        # This file
│
├── 🎨 Frontend (React)
│   ├── src/
│   │   ├── components/               # UI components
│   │   ├── pages/                    # Route pages
│   │   ├── utils/                    # Helper functions
│   │   └── App.jsx                   # Main app
│   └── package.json
│
├── 🔧 Backend (Node.js)
│   ├── src/
│   │   ├── controllers/              # Request handlers
│   │   ├── routes/                   # API routes
│   │   ├── models/                   # Database schemas
│   │   ├── middlewares/              # Custom middleware
│   │   └── utils/                    # Helpers
│   └── package.json
│
├── 🚀 Quinjet (Go)
│   ├── cmd/                          # Entry points
│   ├── internal/                     # Internal packages
│   │   └── services/                 # Business logic
│   └── go.mod
│
├── 🗺️ Routing Backend (Python)
│   └── api/
│       ├── app.py                    # FastAPI app
│       ├── landmark.py               # Landmark detection
│       └── thaparMap.geojson        # Campus map
│
└── 🐳 DevOps
    ├── docker-compose.yml            # Service orchestration
    └── */Dockerfile                  # Container configs
```

---

## 🌟 Feature Highlights

### Core Features
✅ **Smart Navigation**
   - Landmark-based directions
   - Walking path optimization
   - Turn-by-turn instructions

✅ **Real-Time Tracking**
   - Live e-rickshaw positions
   - WebSocket updates
   - ETA predictions

✅ **User Management**
   - Email/password auth
   - Google OAuth login
   - Saved locations
   - Search history

✅ **Admin Dashboard**
   - Driver management
   - Route monitoring
   - System analytics

### Technical Excellence
✅ Microservices architecture
✅ RESTful API design
✅ Real-time WebSocket communication
✅ Geospatial data processing
✅ Docker containerization
✅ Scalable infrastructure

---

## 🎓 Learning Path

### For New Developers

#### Week 1: Frontend Basics
1. Read [README.md](./README.md)
2. Follow [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md)
3. Explore `frontend/src/components/`
4. Understand React + Leaflet integration

#### Week 2: Backend Understanding
1. Read [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md) - Backend section
2. Explore `backend/src/` structure
3. Test APIs using Postman
4. Understand authentication flow

#### Week 3: Advanced Services
1. Study Quinjet (Go) service
2. Learn routing backend (Python)
3. Understand WebSocket communication
4. Explore geospatial operations

#### Week 4: Full Stack Integration
1. Trace complete data flows
2. Add a small feature
3. Write tests
4. Deploy with Docker

---

## 🔗 External Resources

### Official Documentation
- [React Docs](https://react.dev/)
- [Express.js Guide](https://expressjs.com/)
- [FastAPI Docs](https://fastapi.tiangolo.com/)
- [Go Documentation](https://go.dev/doc/)
- [Leaflet Tutorials](https://leafletjs.com/examples.html)
- [MongoDB Manual](https://docs.mongodb.com/)
- [Redis Documentation](https://redis.io/docs/)
- [GraphHopper Docs](https://docs.graphhopper.com/)

### Learning Resources
- [React Tutorial](https://react.dev/learn)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)
- [Go by Example](https://gobyexample.com/)
- [FastAPI Tutorial](https://fastapi.tiangolo.com/tutorial/)
- [Docker Getting Started](https://docs.docker.com/get-started/)

---

## 🤝 Contributing

### Before Contributing
1. ✅ Read [PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md)
2. ✅ Set up development environment using [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md)
3. ✅ Understand the architecture
4. ✅ Check existing issues on GitHub

### Contribution Workflow
```bash
# 1. Fork and clone
git clone git@github.com:yourusername/mapmitra.git

# 2. Create feature branch
git checkout -b feature/amazing-feature

# 3. Make changes and test
npm run dev  # Test locally

# 4. Commit with descriptive message
git commit -m "feat: Add amazing feature"

# 5. Push and create PR
git push origin feature/amazing-feature
```

### Code Style
- **JavaScript**: ESLint configuration
- **Python**: Black formatter, PEP 8
- **Go**: gofmt, golint
- **Commit Messages**: Conventional Commits format

---

## 🐛 Getting Help

### Troubleshooting Steps
1. Check [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md) - Troubleshooting section
2. View service logs: `docker-compose logs [service-name]`
3. Check service health: `docker-compose ps`
4. Search GitHub Issues
5. Ask in GitHub Discussions

### Common Issues
- **Port conflicts**: Change ports in docker-compose.yml
- **Database connection**: Verify MONGO_URI in .env
- **Redis errors**: Ensure Redis is running
- **Build failures**: Clear Docker cache and rebuild

---

## 📞 Contact & Support

- **GitHub Issues**: [MapMitra Issues](https://github.com/yxshee/mapmitra/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yxshee/mapmitra/discussions)
- **Team**: See [README.md](./README.md) for team member profiles

---

## 📝 License

This project is licensed under the **MIT License**. See [LICENSE](./LICENSE) file for details.

---

## 🙏 Acknowledgments

- OpenStreetMap for map data
- GraphHopper for routing engine
- TIET for project inspiration
- All open-source contributors

---

## 📅 Version History

### v1.0.0 (Current)
- ✅ Complete system architecture
- ✅ Frontend with React + Leaflet
- ✅ Backend APIs (Node.js, Go, Python)
- ✅ Real-time tracking with WebSocket
- ✅ Landmark-based navigation
- ✅ User authentication
- ✅ Admin dashboard
- ✅ Docker deployment

### Upcoming Features (v2.0)
- 🔜 Mobile app (React Native)
- 🔜 Offline support (PWA)
- 🔜 AR navigation
- 🔜 Voice guidance
- 🔜 Route preferences
- 🔜 Analytics dashboard

---

**🎉 Welcome to MapMitra! Happy Navigating!**

Made with ❤️ by TIET Students

---

## 📖 Documentation Quick Links

- **[README.md](./README.md)** - Project Overview
- **[PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md)** - Complete Technical Docs
- **[QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md)** - Setup & Installation
- **[TECHNOLOGY_STACK.md](./TECHNOLOGY_STACK.md)** - Technology Deep Dive
- **[LICENSE](./LICENSE)** - MIT License
- **[SECURITY.md](./SECURITY.md)** - Security Policy

---

*Last Updated: January 2026*
