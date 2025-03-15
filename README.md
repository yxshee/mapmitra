
# 🗺️ MapMitra: Navigate Effortlessly 🚀

<div align="center">
  <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License">
  <img src="https://img.shields.io/badge/React-18.2-blue?logo=react" alt="React">
  <img src="https://img.shields.io/badge/Node.js-18.x-green?logo=node.js" alt="Node.js">
</div>

![MapMitra Banner](https://github.com/user-attachments/assets/3e56dbf6-8b08-4ec3-8a6b-1b52c3d78319)

## 🌟 Overview
MapMitra is your **smart campus companion** 🧭 at Thapar Institute of Engineering & Technology (TIET). Designed to eliminate navigation headaches, we transform campus exploration with:

🚩 **Landmark-Based Navigation**  
🚌 **Real-Time E-Rickshaw Tracking**  
🎯 **Personalized Recommendations**

> "Because getting lost should be an adventure, not a daily routine!" 🔍

---

## 🚀 Features
### 🧭 Smart Navigation
| Feature | Description | Emoji |
|---------|-------------|-------|
| **Landmark Guidance** | Directions using campus monuments | 🗿 |
| **AR Pathfinding** | Augmented Reality waypoints (Coming Soon!) | 👓 |
| **Accessibility Mode** | Wheelchair-friendly routes | ♿ |

### 📱 Real-Time Tracking
```plaintext
🛺 Live E-Rickshaw Locations
⏱️ ETA Predictions (90% accuracy)
🔔 Availability Notifications
```

### 🛠️ Admin Tools
```diff
+ Driver Management Portal
+ Dynamic Route Updates
+ Emergency Alerts System
```

---

## 🛠️ Tech Stack
### Frontend
![React](https://img.shields.io/badge/-React-61DAFB?logo=react&logoColor=white)
![MapLibre](https://img.shields.io/badge/-MapLibre-4264FB)

### Backend
![Node.js](https://img.shields.io/badge/-Node.js-339933?logo=node.js&logoColor=white)
![Socket.io](https://img.shields.io/badge/-Socket.io-010101?logo=socket.io)

### Database
![MongoDB](https://img.shields.io/badge/-MongoDB-47A248?logo=mongodb&logoColor=white)
![Redis](https://img.shields.io/badge/-Redis-DC382D?logo=redis&logoColor=white)

---

## ⚡ Quick Start
```bash
# Clone with SSH
git clone git@github.com:shouryade/MapMitra.git

# Install dependencies
npm install

# Start development server
npm run dev
```

**Environment Setup** 🔧
```env
MONGO_URI=mongodb+srv://user:pass@cluster.mapmitra.mongodb.net
REDIS_URL=redis://default:pass@redis-12345.c8.us-east-1-2.ec2.cloud.redislabs.com:12345
```

---

## � Deployment Pipeline
```mermaid
graph TD
    A[Local Development] -->|Dockerize| B[CI/CD Pipeline]
    B --> C{Cloud Provider}
    C -->|Heroku| D[Production]
    C -->|AWS EC2| E[Production]
    C -->|DigitalOcean| F[Production]
```

### 🐳 Docker Deployment
```dockerfile
# Optimized Production Image
FROM node:18-alpine
WORKDIR /app
COPY --chown=node:node . .
RUN npm ci --only=production
USER node
EXPOSE 3000
CMD ["npm", "start"]
```

---


## 👥 Meet the Team
<table>
  <tr align="center">
    <td><a href="https://github.com/AM0312"><img src="https://avatars.githubusercontent.com/AM0312" width="100px"><br/>Ansh Midha</a></td>
    <td><a href="https://github.com/leena153"><img src="https://avatars.githubusercontent.com/leena153" width="100px"><br/>Leena Gupta</a></td>
    <td><a href="https://github.com/madhurgaba2603"><img src="https://avatars.githubusercontent.com/madhurgaba2603" width="100px"><br/>Madhur Gaba</a></td>
    <td><a href="https://github.com/shouryade"><img src="https://avatars.githubusercontent.com/shouryade" width="100px"><br/>Shourya De</a></td>
    <td><a href="https://github.com/yxshee"><img src="https://avatars.githubusercontent.com/yxshee" width="100px"><br/>Yash Dogra</a></td>
  </tr>
</table>

---

## 📜 License
```text
MIT License

Copyright (c) 2024 Yash Dogra 

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

<div align="center">
  Made with ❤️ by TIET Students | 🧭 Happy Navigating!
</div>
