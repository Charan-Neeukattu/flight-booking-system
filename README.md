# ✈️ SkyBooker - Full Stack Flight Booking System

A full-stack flight search and booking web application built with **React 19**, **Vite**, **Tailwind CSS**, **Node.js**, **Express**, and **MongoDB**.

---

## 📑 Table of Contents
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Prerequisites](#-prerequisites)
- [Environment Variables](#-environment-variables)
- [Quick Start Guide](#-quick-start-guide)
  - [1. Database Setup](#1-database-setup)
  - [2. Backend Setup](#2-backend-setup)
  - [3. Frontend Setup](#3-frontend-setup)
- [Default Admin Credentials](#-default-admin-credentials)
- [API Endpoints Overview](#-api-endpoints-overview)

---

## ✨ Features

### 👤 User Features
* **Flight Search:** Search available flights by source city, destination city, and travel dates.
* **User Authentication:** 
  * Register with 6-digit email OTP verification (via Nodemailer).
  * Secure JWT authentication with hashed passwords (bcrypt).
* **Booking & Ticketing:** 
  * Book passenger tickets for selected flights.
  * View booking history, booking status, and download/view ticket details under "My Bookings".
* **User Profile:** Manage profile information and view personal bookings.

### 🛡️ Admin Dashboard (`/admin`)
* **Add Flights:** Schedule new flights by specifying airline, source, destination, departure/arrival times, and ticket prices.
* **Manage Bookings:** View master list of all bookings made by all passengers across the platform.
* **Filter by Date:** Filter passenger bookings for specific flight schedules.

---

## 🛠 Tech Stack

### Frontend
* **React 19** + **Vite**
* **Tailwind CSS** (Styling & Responsive UI)
* **React Router DOM v7** (Client-side routing)
* **Framer Motion** (Smooth animations & transitions)
* **Lucide React** (Icons)
* **Axios** (API communication)
* **date-fns** (Date formatting)

### Backend
* **Node.js** & **Express 5**
* **MongoDB** with **Mongoose 9** ODM
* **JSON Web Tokens (JWT)** for role-based authentication
* **bcryptjs** for secure password hashing
* **Nodemailer** for email OTP verification
* **Cors** & **dotenv**

---

## 📂 Project Architecture

```text
Project/
├── backend/
│   ├── config/             # Database connection (db.js)
│   ├── controllers/        # Business logic (auth, flights, bookings)
│   ├── middleware/         # Auth & Admin role verification (auth.js)
│   ├── models/             # Mongoose schemas (User, Flight, Booking, Ticket, OTP)
│   ├── routes/             # Express API routes
│   ├── .env                # Backend environment configuration
│   ├── createAdmin.js      # Script to seed default administrator
│   ├── seed.js             # Script to populate sample flight schedules
│   ├── server.js           # Server entry point
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── components/     # Reusable UI components (Navbar, etc.)
│   │   ├── context/        # AuthContext for global authentication state
│   │   ├── pages/          # Home, Login, Register, FlightSearch, Bookings, Admin, Profile
│   │   ├── App.jsx         # App routes & structure
│   │   └── main.jsx        # Entry point
│   ├── .env                # Frontend environment configuration
│   ├── package.json
│   ├── tailwind.config.js
│   └── vite.config.js
│
└── README.md
```

---

## 📋 Prerequisites

Ensure you have the following installed on your machine:
* [Node.js](https://nodejs.org/) (v18 or higher; v24 recommended)
* [MongoDB Community Server](https://www.mongodb.com/try/download/community) running locally on port `27017` (or MongoDB Atlas URI)
* [MongoDB Compass](https://www.mongodb.com/products/tools/compass) (Optional, for database GUI visualization)

---

## 🔐 Environment Variables

### Backend (`backend/.env`)
```properties
PORT=5000
MONGODB_URI=mongodb://localhost:27017/flightbooking
JWT_SECRET=supersecretjwtkey123
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_gmail_app_password
```
*(If `EMAIL_USER` / `EMAIL_PASS` are left empty or omitted, OTPs will automatically print to the backend terminal console for development mode).*

### Frontend (`frontend/.env`)
```properties
VITE_API_URL=http://localhost:5000
```

---

## 🚀 Quick Start Guide

### 1. Database Setup
Make sure MongoDB is running on your machine:
* **Windows Service:** `net start MongoDB`
* **MongoDB Compass:** Connect to `mongodb://localhost:27017`

### 2. Backend Setup
Open a terminal:
```powershell
# Navigate to backend directory
cd backend

# Install dependencies (if not already installed)
npm install

# Seed sample flights (IndiGo, Air India, Vistara)
npm run seed

# Create the initial admin account
npm run create-admin

# Start the backend server
npm start
```
> Server runs at `http://localhost:5000`

### 3. Frontend Setup
Open a **second terminal**:
```powershell
# Navigate to frontend directory
cd frontend

# Install dependencies (if not already installed)
npm install

# Start development server
npm run dev
```
> Frontend runs at `http://localhost:5173`

---

## 🔑 Default Admin Credentials

To access the Admin Dashboard at `http://localhost:5173/admin`:

* **URL:** `http://localhost:5173/login`
* **Email:** `admin@skybooker.com`
* **Password:** `admin123`

---

## 📡 API Endpoints Overview

| Method | Endpoint | Description | Access |
| :--- | :--- | :--- | :--- |
| **POST** | `/api/auth/send-otp` | Send verification OTP to email | Public |
| **POST** | `/api/auth/register` | Register new user with OTP | Public |
| **POST** | `/api/auth/login` | Login user & receive JWT token | Public |
| **GET** | `/api/flights` | Search and list available flights | Public |
| **POST** | `/api/flights` | Create a new flight schedule | Admin only |
| **POST** | `/api/bookings` | Book a flight ticket | Authenticated |
| **GET** | `/api/bookings/my-bookings`| Get current user's bookings | Authenticated |
| **GET** | `/api/bookings` | Get all platform bookings | Admin only |

