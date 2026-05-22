# College Attendance Management System

A full-stack MERN attendance management platform with **geo-fenced staff check-ins** and real-time attendance reporting for students. Built to replace manual register-keeping with a verifiable, location-aware digital workflow.

## Overview

College attendance traditionally runs on paper registers prone to proxy attendance and post-hoc edits. This project replaces that with a digital system where staff attendance is validated against the college's physical coordinates (location-based check-in) and students get instant access to their own attendance records — driving accountability on both sides.

The system uses Redux for predictable state management on the frontend, and a Node/Express backend with MongoDB for the attendance ledger.

## Features

- 📍 **Location-validated staff attendance** — Staff check-ins are compared against college geo-coordinates to prevent off-campus marking
- 🎓 **Student attendance portal** — Students see live attendance percentages and history per course
- 👨‍🏫 **Staff dashboard** — Teachers mark attendance class-by-class with a clean UI
- 🗓️ **Per-course tracking** — Attendance is recorded against courses and sessions, not just dates
- 📊 **Attendance reports** — Aggregate views for staff and admins; per-student drill-downs
- 🔐 **Role-based access** — Separate flows for students, staff, and administrators
- ⚡ **Redux-powered state** — Predictable client-side state for offline-tolerant UX

## Tech Stack

| Layer | Tech |
|---|---|
| Frontend | React.js, Redux |
| Backend | Node.js, Express.js |
| Database | MongoDB |
| Auth | JWT-based authentication |
| Geolocation | Browser Geolocation API + server-side validation |

## Project Structure

```
.
├── Backend/      # Node.js + Express API
│   ├── models/   # User, Course, Attendance, Session schemas
│   ├── routes/   # Auth, attendance, reports
│   ├── middleware/  # Auth + location verification
│   └── server.js
├── Frontend/     # React + Redux client
│   ├── src/
│   │   ├── store/    # Redux slices
│   │   ├── pages/    # Student, Staff, Admin views
│   │   └── components/
│   └── public/
└── README.md
```

## Getting Started

### Prerequisites

- Node.js 16+
- MongoDB (local or Atlas)
- HTTPS for geolocation in production (required by browsers)

### Setup

```bash
# Clone
git clone https://github.com/ayyadurai-k/college-attendance-management-system.git
cd college-attendance-management-system

# Backend
cd Backend
npm install
cp .env.example .env
# Edit .env with MONGO_URI, JWT_SECRET, COLLEGE_LAT, COLLEGE_LNG, GEO_RADIUS_METERS
npm run dev

# Frontend (in another terminal)
cd ../Frontend
npm install
npm start
```

Backend runs on `http://localhost:5000`, frontend on `http://localhost:3000`.

## Location Validation Flow

1. Staff opens the attendance marking page; browser requests geolocation permission.
2. Browser sends lat/long with the check-in request.
3. Server validates the submitted coordinates against the college's configured coordinates within a configurable radius (e.g., 200m).
4. If outside the radius, the check-in is rejected with a clear error.
5. If inside, the attendance entry is saved with the timestamp and coordinates for audit.

This ensures staff cannot mark themselves present from home or another campus.

## Author

**K Ayyadurai** — Full Stack & DevOps Engineer
[GitHub](https://github.com/ayyadurai-k) · [Email](mailto:kmayyadurai286@gmail.com)
