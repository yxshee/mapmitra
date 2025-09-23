# 🗺️ MapMitra Frontend

A modern React-based frontend application for the MapMitra smart campus navigation system at Thapar Institute of Engineering & Technology (TIET).

## 📋 Overview

The frontend provides an intuitive user interface for campus navigation with real-time e-rickshaw tracking, landmark-based directions, and interactive mapping features. Built with React 18 and modern web technologies, it offers a responsive and accessible experience across devices.

## ✨ Features

### 🧭 Smart Navigation
- **Interactive Campus Map**: Real-time interactive map powered by Leaflet and OpenStreetMap
- **Location Search**: Intelligent search with suggestions using Nominatim geocoding
- **Turn-by-Turn Navigation**: Step-by-step directions with landmark references
- **Route Visualization**: Visual route display with polylines and markers

### 🚌 E-Rickshaw Tracking
- **Real-time Tracking**: Live location updates of available e-rickshaws
- **Ride Hailing**: Request rides with automatic driver matching
- **Distance Calculation**: Real-time distance tracking to pickup points
- **Status Updates**: Live status notifications during ride requests

### 👤 User Management
- **Multi-role Support**: Students, visitors, drivers, and admin interfaces
- **Google OAuth**: Secure authentication via Google OAuth 2.0
- **Profile Management**: User profile and preferences management

### 📱 Responsive Design
- **Mobile-First**: Optimized for mobile devices and touch interactions
- **Cross-Platform**: Works seamlessly on iOS, Android, and desktop browsers
- **Accessibility**: Built with accessibility best practices

## 🛠️ Tech Stack

### Core Technologies
![React](https://img.shields.io/badge/-React-61DAFB?logo=react&logoColor=white&style=flat-square)
![Vite](https://img.shields.io/badge/-Vite-646CFF?logo=vite&logoColor=white&style=flat-square)
![JavaScript](https://img.shields.io/badge/-JavaScript-F7DF1E?logo=javascript&logoColor=black&style=flat-square)

### UI & Styling
![TailwindCSS](https://img.shields.io/badge/-TailwindCSS-38B2AC?logo=tailwind-css&logoColor=white&style=flat-square)
![DaisyUI](https://img.shields.io/badge/-DaisyUI-5A0EF8?logo=daisyui&logoColor=white&style=flat-square)

### Mapping & Navigation
![Leaflet](https://img.shields.io/badge/-Leaflet-199900?logo=leaflet&logoColor=white&style=flat-square)
![OpenStreetMap](https://img.shields.io/badge/-OpenStreetMap-7EBC6F?logo=openstreetmap&logoColor=white&style=flat-square)

### State Management & Routing
![React Router](https://img.shields.io/badge/-React_Router-CA4245?logo=react-router&logoColor=white&style=flat-square)
![Axios](https://img.shields.io/badge/-Axios-5A29E4?logo=axios&logoColor=white&style=flat-square)

## 📦 Dependencies

### Core Dependencies
```json
{
  "react": "^18.3.1",
  "react-dom": "^18.3.1",
  "react-router-dom": "^7.5.2",
  "vite": "^5.4.10"
}
```

### Mapping Libraries
```json
{
  "leaflet": "^1.9.4",
  "react-leaflet": "^4.2.1",
  "leaflet-routing-machine": "^3.2.12",
  "leaflet-control-geocoder": "^2.4.0",
  "leaflet-draw": "^1.0.4",
  "react-leaflet-draw": "^0.20.4"
}
```

### HTTP & Utilities
```json
{
  "axios": "^1.8.2",
  "lodash": "^4.17.21"
}
```

### Development Dependencies
```json
{
  "tailwindcss": "^3.4.16",
  "daisyui": "^4.12.14",
  "eslint": "^9.13.0",
  "@vitejs/plugin-react": "^4.3.3"
}
```

## 🚀 Quick Start

### Prerequisites
- **Node.js**: Version 18.x or higher
- **npm**: Version 8.x or higher (comes with Node.js)
- **Modern Browser**: Chrome 88+, Firefox 85+, Safari 14+, Edge 88+

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yxshee/mapmitra.git
   cd mapmitra/frontend
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
   VITE_API_BASE_URL=http://localhost:5000
   VITE_BACKEND_URL=http://localhost:3000
   VITE_QUINJET_URL=http://localhost:8080
   VITE_ROUTING_URL=http://localhost:5000
   VITE_GOOGLE_CLIENT_ID=your_google_client_id
   ```

4. **Start development server**
   ```bash
   npm run dev
   ```

   The application will be available at `http://localhost:5173`

### Build for Production

```bash
# Build the application
npm run build

# Preview the production build
npm run preview
```

## 📁 Project Structure

```
frontend/
├── public/                     # Static assets
│   ├── destination.png         # Destination marker icon
│   ├── rickshaw.png           # E-rickshaw marker icon
│   ├── userloc.png            # User location marker icon
│   ├── ripple.gif             # Loading animations
│   ├── thaparMap.geojson      # Campus map data
│   └── vite.svg               # Vite logo
├── src/
│   ├── components/            # Reusable React components
│   │   ├── BottomNavigation.jsx   # Bottom navigation bar
│   │   ├── GettingStarted.jsx     # Onboarding component
│   │   ├── Login.jsx              # Login form
│   │   ├── MapComponent.jsx       # Main map interface
│   │   ├── Modal.jsx              # Modal dialogs
│   │   ├── Register.jsx           # Registration form
│   │   ├── RoutingControl.jsx     # Route control component
│   │   └── UserMap.jsx            # User-specific map view
│   ├── pages/                 # Page components
│   │   ├── Admin.jsx              # Admin dashboard
│   │   ├── Auto.jsx               # Auto/driver interface
│   │   ├── Home.jsx               # Landing page
│   │   └── User.jsx               # User dashboard
│   ├── utils/                 # Utility functions
│   │   ├── axiosInstance.js       # Configured Axios instance
│   │   ├── bfs.js                 # BFS algorithm for pathfinding
│   │   └── constants.js           # Application constants
│   ├── mockData.js            # Mock data for development
│   ├── App.jsx                # Main App component
│   ├── App.css                # Global styles
│   ├── index.css              # Base styles
│   └── main.jsx               # Application entry point
├── mockbackend/               # Mock backend for development
│   └── mockServer.js
├── package.json               # Project dependencies and scripts
├── vite.config.js            # Vite configuration
├── tailwind.config.js        # Tailwind CSS configuration
├── postcss.config.js         # PostCSS configuration
├── eslint.config.js          # ESLint configuration
└── vercel.json               # Vercel deployment configuration
```

## 🔧 Configuration

### Vite Configuration
```javascript
// vite.config.js
export default defineConfig({
  plugins: [react()],
  server: {
    host: '0.0.0.0',
    port: 5173
  },
  build: {
    outDir: 'dist',
    sourcemap: true
  }
})
```

### Tailwind CSS Configuration
```javascript
// tailwind.config.js
module.exports = {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {
      colors: {
        primary: '#1D4ED8',
        secondary: '#9333EA'
      }
    }
  },
  plugins: [require("daisyui")]
}
```

## 🌐 API Integration

### Backend Services
- **Authentication API**: `http://localhost:3000/api/auth`
- **User Management**: `http://localhost:3000/api/user`
- **Ride Matching**: `http://localhost:8080/api/v1/rides`
- **Routing Service**: `http://localhost:5000/route_instructions`

### API Endpoints Used
```javascript
// Authentication
POST /api/auth/login
POST /api/auth/register
POST /api/auth/logout
GET  /api/auth/google

// Ride Management
POST /api/v1/rides/new
GET  /api/v1/rides/status
GET  /api/v1/location

// Routing
POST /route_instructions
```

## 🗺️ Map Features

### Interactive Elements
- **User Location Marker**: Real-time user position tracking
- **Destination Markers**: Visual destination indicators
- **E-Rickshaw Markers**: Live vehicle locations
- **Route Polylines**: Visual route representation
- **Search Overlay**: Location search interface

### Map Controls
- **Zoom Controls**: Zoom in/out functionality
- **Pan Controls**: Map dragging and panning
- **Bounds Restriction**: Limited to TIET campus area
- **Responsive Gestures**: Touch-friendly interactions

## 🔐 Authentication Flow

### Google OAuth Integration
```javascript
// OAuth configuration
const googleConfig = {
  clientId: process.env.VITE_GOOGLE_CLIENT_ID,
  redirectUri: `${window.location.origin}/auth/callback`,
  scope: 'openid email profile'
}
```

### User Roles
- **Student**: Basic navigation and ride booking
- **Visitor**: Limited navigation features
- **Driver**: Vehicle management and ride acceptance
- **Admin**: Full system administration

## 📱 Responsive Design

### Breakpoints
```css
/* Mobile First */
@media (min-width: 640px) { /* sm */ }
@media (min-width: 768px) { /* md */ }
@media (min-width: 1024px) { /* lg */ }
@media (min-width: 1280px) { /* xl */ }
```

### Mobile Optimizations
- Touch-friendly button sizes (minimum 44px)
- Optimized map controls for touch devices
- Responsive navigation patterns
- Performance optimizations for mobile networks

## 🧪 Development

### Development Scripts
```bash
# Start development server with hot reload
npm run dev

# Run linting
npm run lint

# Build for production
npm run build

# Preview production build
npm run preview
```

### Code Quality
- **ESLint**: Code linting and style enforcement
- **Prettier**: Code formatting (via dev dependencies)
- **Husky**: Git hooks for pre-commit checks (if configured)

### Mock Backend
For development without backend services:
```bash
# Start mock server
node mockbackend/mockServer.js
```

## 🚀 Deployment

### Vercel Deployment
```json
{
  "buildCommand": "npm run build",
  "outputDirectory": "dist",
  "framework": "vite",
  "env": {
    "VITE_API_BASE_URL": "@api_base_url",
    "VITE_GOOGLE_CLIENT_ID": "@google_client_id"
  }
}
```

### Build Optimization
- **Tree Shaking**: Automatic dead code elimination
- **Code Splitting**: Route-based code splitting
- **Asset Optimization**: Automatic image and asset optimization
- **Compression**: Gzip compression for production builds

## 🐛 Troubleshooting

### Common Issues

1. **Map not loading**
   - Check internet connection for tile loading
   - Verify Leaflet CSS import
   - Check browser console for errors

2. **Location not detected**
   - Ensure HTTPS for geolocation API
   - Check browser location permissions
   - Verify geolocation support

3. **API connection issues**
   - Check backend service status
   - Verify API endpoint URLs
   - Check CORS configuration

4. **Build errors**
   - Clear node_modules and reinstall
   - Check Node.js version compatibility
   - Verify environment variables

### Performance Optimization
- Use React.memo for expensive components
- Implement virtual scrolling for large lists
- Optimize map rendering with clustering
- Lazy load non-critical components

## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Development Guidelines
- Follow React best practices
- Use TypeScript for new components (migration in progress)
- Write meaningful commit messages
- Test on multiple devices and browsers
- Update documentation for new features

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
  <p>🗺️ Navigate Smart, Navigate Easy! 🚀</p>
</div>
