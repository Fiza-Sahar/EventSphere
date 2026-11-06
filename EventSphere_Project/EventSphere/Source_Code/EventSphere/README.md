# EventSphere Management Platform 🚀

**EventSphere Management** is an advanced commercial-grade Expo and Event Management SaaS Platform. It provides an all-in-one ecosystem for trade show organizers, exhibitors, and attendees featuring interactive 3D floor plan layout navigation, Google Gemini AI event concierges, real-time Socket.IO synchronization, and comprehensive role-based analytics.

---

## 🌟 Key Features

1. **Interactive 3D Expo Floor (Three.js / React Three Fiber / Drei)**
   - Dynamic 3D rendering of booth structures, main stage, entrance/exit arches, restrooms, food court, and networking lounges.
   - Status color indicators for `AVAILABLE` (emerald), `RESERVED` (amber), and `OCCUPIED` (indigo) booths.
   - Smooth camera orbit/pan/zoom controls, hover highlight, booth inspector popovers, and interactive 2D fallback map.

2. **AI Event Assistant & Admin Analytics (Google Gemini Integration)**
   - Floating AI assistant widget available on every page.
   - Solves real user queries: exhibitors lookup, personal schedule generation without conflicts, booth locator, and session recommendations.
   - Admin AI Insights engine analyzing real database metrics to generate actionable recommendations.

3. **Real-Time Synchronicity (Socket.IO)**
   - Instant live updates across connected clients when booth assignments change, notifications are sent, or messages are transmitted.

4. **Multi-Role RBAC Security (JWT + bcryptjs)**
   - **Admin / Organizer**: Full CRUD for Expos, Exhibitors approval/rejection, Booth layout configuration, 3D Floor Builder, Schedule/Speaker management, and Analytics dashboards.
   - **Exhibitor**: Company profile showcase, product catalog, assigned 3D booth inspection, lead messaging.
   - **Attendee**: Public expo exploration, ticket pass registration, saved timetable builder with conflict alerts, favorite booth bookmarks.

---

## 🛠️ Technology Stack

- **Frontend**: React.js, Vite, React Router DOM, Three.js, `@react-three/fiber`, `@react-three/drei`, Recharts, Lucide React icons, Bootstrap 5.
- **Backend**: Node.js, Express.js (ES Modules), MongoDB, Mongoose, JWT, bcryptjs, Socket.IO, dotenv, CORS.
- **AI**: Google Gemini API integration with intelligent database fallback engine.

---

## 📁 Folder Structure

```
EventSphere/
├── client/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── ai/
│   │   │   │   └── AIAssistantModal.jsx
│   │   │   ├── Footer.jsx
│   │   │   ├── Navbar.jsx
│   │   │   └── Sidebar.jsx
│   │   ├── context/
│   │   │   ├── AuthContext.jsx
│   │   │   └── SocketContext.jsx
│   │   ├── layouts/
│   │   │   ├── DashboardLayout.jsx
│   │   │   └── PublicLayout.jsx
│   │   ├── pages/
│   │   │   ├── admin/
│   │   │   ├── attendee/
│   │   │   ├── exhibitor/
│   │   │   └── public/
│   │   ├── services/
│   │   │   └── api.js
│   │   ├── three/
│   │   │   ├── Booth.jsx
│   │   │   ├── CameraControls.jsx
│   │   │   ├── Entrance.jsx
│   │   │   ├── ExpoScene.jsx
│   │   │   ├── Floor.jsx
│   │   │   ├── FloorPlan2D.jsx
│   │   │   └── Stage.jsx
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
│
├── server/
│   ├── config/
│   │   ├── db.js
│   │   └── socket.js
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── scripts/
│   │   └── seed.js
│   ├── .env
│   ├── package.json
│   └── server.js
│
├── .env.example
├── README.md
└── package.json
```

---

## ⚡ Quick Start & Installation

### 1. Environment Variables Configuration
Copy `.env.example` to `server/.env`:
```env
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/eventsphere
JWT_SECRET=eventsphere_super_secret_jwt_key_2026_production
CLIENT_URL=http://localhost:5173
AI_API_KEY=your_gemini_api_key_here
```

### 2. Install Dependencies
Run from project root:
```bash
npm run install:all
```

### 3. Seed Database
Run the pre-populated seed script:
```bash
npm run seed
```
**Demo Accounts Generated**:
- **Admin**: `admin@eventsphere.com` / `password123`
- **Exhibitor**: `contact@techcorpglobal.com` / `password123`
- **Attendee**: `attendee1@gmail.com` / `password123`

### 4. Run Development Application
Run both client and server concurrently:
```bash
npm run dev
```
- Frontend: `http://localhost:5173`
- Backend API: `http://localhost:5000`

---

## 🔌 Core API Overview

| Method | Endpoint | Description | Access |
|---|---|---|---|
| `POST` | `/api/auth/register` | Register new user | Public |
| `POST` | `/api/auth/login` | Authenticate user & receive JWT | Public |
| `GET` | `/api/auth/me` | Fetch authenticated profile | Protected |
| `GET` | `/api/expos` | List all trade expos | Public |
| `GET` | `/api/booths` | Fetch 3D floor booth grid | Public |
| `PUT` | `/api/booths/:id` | Update booth coordinates & status | Admin / Exhibitor |
| `GET` | `/api/exhibitors` | Exhibitor directory & search | Public |
| `GET` | `/api/sessions` | Event schedule timetable | Public |
| `POST` | `/api/sessions/:id/register` | Bookmark session with conflict check | Protected |
| `POST` | `/api/ai/chat` | AI Event Assistant & Admin Analytics | Public |
| `GET` | `/api/analytics` | Admin metrics & aggregate data | Admin |

---

## 🔒 Security
- Passwords are strictly hashed with `bcryptjs`.
- JWT authentication headers (`Bearer <token>`).
- Centralized Express error handler middleware preventing stack leak in production.
- API keys kept exclusively server-side in `.env`.
