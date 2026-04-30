# 🏙️ CivicTrack (CivIQ2)

> A civic complaint management platform that empowers citizens to report local issues, track their resolution, and engage with their community — built for hackathon.

---

## 📌 Overview

CivicTrack is a full-stack web application designed to bridge the gap between citizens and local governance. Citizens can submit civic complaints (potholes, broken streetlights, garbage overflow, etc.), while administrators and ward officials get aggregated dashboards to prioritize and resolve issues efficiently.

---

## ✨ Features

### 👤 User Authentication
- Secure **register and login** system using JWT tokens
- Tokens stored in `localStorage` and sent via `x-auth-token` header on protected routes
- Role-based access: **Citizens** and **Admins**

### 📋 Complaint Reporting
- Citizens can submit detailed civic complaints with category, description, and location
- Complaints are tagged to specific **wards** for geographic organization
- **Priority-based categorization** ensures urgent issues surface quickly

### 🤖 AI-Powered Duplicate Detection
- Integrates with **OpenAI API** to detect duplicate or similar complaints before submission
- Reduces redundancy in the complaints database and improves issue tracking accuracy

### 📊 Multiple Dashboards
- **Citizen Dashboard** (`/dashboard`) — Personal complaint history and status tracking
- **Admin Dashboard** — Full control over all complaints and resolution workflows
- **Ward Dashboard** (`/ward-dashboard`) — Ward-level aggregated view of issues, statistics, and trends

### 📈 Issue Aggregation
- Complaints are automatically **aggregated into Issues** by ward and category
- Helps officials see patterns (e.g., multiple pothole reports in the same area) instead of individual tickets

### ⬆️ Upvoting System
- Citizens can **upvote complaints and issues** to signal community priority
- Higher-voted issues get more visibility for faster resolution

### 🔄 Real-Time Updates
- Powered by **Socket.io** for live updates on complaint status changes without page refresh

### 🌐 Community Feed
- A public **Community Feed** (`/community`) where citizens can view and engage with issues in their area
- Promotes transparency and civic participation

### 📡 Public Stats API
- Ward-level statistics available via a **public API endpoint** — no authentication required
- Useful for open data integrations and transparency portals

### 🌱 Seed Data
- Comes with a `seed.js` script that creates **150+ realistic complaints**, 21 users (1 admin + 20 citizens), and aggregated issues for instant demo

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React.js, CSS |
| Backend | Node.js, Express.js |
| Database | MongoDB (local or Atlas) |
| Auth | JWT (JSON Web Tokens) |
| Real-Time | Socket.io |
| AI Feature | OpenAI API |
| HTTP Client | Axios |

---

## 📁 Project Structure

```
civicTrack-Hackthon/
├── backend/
│   ├── models/          # MongoDB schemas (User, Complaint, Issue)
│   ├── routes/          # API route handlers
│   ├── middleware/       # JWT authentication middleware
│   ├── services/        # Business logic (duplicate detection, aggregation)
│   ├── config/          # Database configuration
│   ├── server.js        # Express server entry point
│   └── seed.js          # Script to populate test data
│
└── frontend/
    └── src/
        ├── context/     # React Context (AuthContext)
        ├── services/    # API service layer (Axios config)
        ├── pages/       # Page-level components (Dashboard, Report, Issues, etc.)
        ├── components/  # Reusable UI components
        └── App.js       # Root component and routing
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js v14 or higher
- MongoDB (local instance or MongoDB Atlas)
- npm or yarn
- Ports **5000** (backend) and **3000** (frontend) must be free

---

### 🔧 Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in the `backend/` directory:

```env
MONGODB_URI=mongodb://localhost:27017/civictrack
JWT_SECRET=your_jwt_secret_key_change_this
PORT=5000
NODE_ENV=development
OPENAI_API_KEY=sk-your-openai-key-here   # Optional: enables AI duplicate detection
```

For **MongoDB Atlas**, replace `MONGODB_URI` with:

```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/civictrack
```

Optionally seed the database with sample data:

```bash
node seed.js
```

Start the server:

```bash
npm start        # Production
npm run dev      # Development (hot reload via nodemon)
```

Expected output:
```
🚀 Server running on http://localhost:5000
✅ MongoDB connected successfully
```

---

### 🎨 Frontend Setup

In a new terminal:

```bash
cd frontend
npm install
npm start
```

The app will open automatically at `http://localhost:3000`.

---

## 🔑 Test Accounts

After running `node seed.js`:

| Role | Email | Password |
|---|---|---|
| Admin | admin@civictrack.com | admin123 |
| Citizen | citizen1@example.com | password123 |
| Citizen | citizen2@example.com | password123 |
| ... | citizen20@example.com | password123 |

---

## 🌐 API Endpoints

### Authentication
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and receive JWT |

### Complaints
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/complaints` | Get all complaints (auth) |
| POST | `/api/complaints` | Submit a new complaint (auth) |
| GET | `/api/complaints/:id` | Get a specific complaint |
| PUT | `/api/complaints/:id/status` | Update complaint status (auth) |
| POST | `/api/complaints/:id/upvote` | Upvote a complaint (auth) |
| POST | `/api/complaints/check-duplicate` | AI duplicate check |

### Issues
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/issues` | Get all aggregated issues |
| GET | `/api/issues/:id` | Get a specific issue |
| PATCH | `/api/issues/:id/status` | Update issue status (auth) |
| POST | `/api/issues/:id/upvote` | Upvote an issue (auth) |

### Public
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/public/issues` | View issues (no auth required) |
| GET | `/api/public/stats/:ward` | Ward-level statistics |

### Users
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/users/me` | Get current user profile (auth) |

---

## 🧭 App Routes

| Route | Description |
|---|---|
| `/report` | Submit a new complaint |
| `/dashboard` | Citizen's personal dashboard |
| `/issues` | Browse aggregated civic issues |
| `/ward-dashboard` | Ward-level issues and statistics |
| `/community` | Community feed of local issues |

---

## 🐛 Troubleshooting

| Problem | Fix |
|---|---|
| MongoDB connection error | Ensure MongoDB is running or verify `MONGODB_URI` in `.env` |
| CORS error | Make sure backend is on port 5000 and frontend on port 3000 |
| Login fails | Clear browser storage: `localStorage.clear()` in browser console |
| API 404 errors | Verify backend is running and routes are registered in `server.js` |
| Port already in use | Kill the occupying process or change `PORT` in `.env` |

---

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## 🙌 Author

Built with ❤️ by **TEAM CIVIQ** for a hackathon.
