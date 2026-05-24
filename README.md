# 🌱 AgriConnect — Smart Agriculture Platform

<div align="center">

![AgriConnect Logo](https://img.shields.io/badge/AgriConnect-Smart%20Farming-2d6a4f?style=for-the-badge&logo=leaf&logoColor=white)

**Bridging farmers together through technology — equipment sharing, AI predictions, and smart advisory in one platform.**

[![Live Demo](https://img.shields.io/badge/🌐%20Live%20Frontend-agri--connecti.vercel.app-40916c?style=flat-square)](https://agri-connecti.vercel.app/)
[![Backend](https://img.shields.io/badge/🚀%20Backend%20API-Render%20Cloud-74c69d?style=flat-square)](https://agriconnect-mzwn.onrender.com)
[![GitHub](https://img.shields.io/badge/GitHub-adarshiiit0117%2FAgriConnect-black?style=flat-square&logo=github)](https://github.com/adarshiiit0117/AgriConnect)


</div>

---

## 📋 Table of Contents

- [Problem Statement](#-problem-statement)
- [Solution Overview](#-solution-overview)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Modules](#-modules)
- [AI & ML Components](#-ai--ml-components)
- [Database Design](#-database-design)
- [API Overview](#-api-overview)
- [Getting Started](#-getting-started)
- [Docker Deployment](#-docker-deployment)
- [Environment Variables](#-environment-variables)
- [Folder Structure](#-folder-structure)
- [Design Principles](#-design-principles)
- [Non-Functional Requirements](#-non-functional-requirements)
- [Future Roadmap](#-future-roadmap)
- [Contributing](#-contributing)
- [Team](#-team)


---

## 🔴 Problem Statement

India's agricultural sector is dominated by small and marginal farmers who struggle to afford expensive machinery like harvesters, seeders, and crop residue-to-fodder converters. Meanwhile, large farmers often own such equipment that sits idle for much of the year.

This results in:
- **Underutilized assets** owned by large farmers
- **Reduced productivity** for small farmers due to high capital barriers
- **Stubble burning** as a cheap alternative to crop residue management, contributing to severe air pollution in regions like Delhi-NCR
- **Limited crop yield** and reduced income for millions of farming families

---

## 💡 Solution Overview

**AgriConnect** is a SaaS-based digital platform that connects large farmers willing to rent out their machinery or agricultural property with small farmers in need. The platform enables:

- Equipment discovery and booking with secure transactions
- Efficient scheduling and booking management
- Promotion of crop residue-to-fodder machines to reduce stubble burning
- AI-powered crop recommendations, yield forecasting, and market price predictions
- A multilingual voice and text chatbot for real-time farmer support

> **Mission:** Empower farmers, reduce costs, and boost agricultural productivity through collaborative technology.

---

## ✨ Key Features

### 🚜 Farmer-to-Farmer Equipment Sharing
Direct rental marketplace where big farmers list underutilized machinery (tractors, harvesters, seeders) for small farmers to book — reducing idle time and increasing rural income.

### 🌿 Pollution Reduction via Fodder Conversion
Promotes machines that convert crop residue into animal fodder, directly tackling stubble burning and reducing air pollution in agricultural belts.

### 🤖 Multilingual AI Chatbot (AgriBot)
Voice and text chatbot in regional languages guiding farmers on equipment use, crop planning, weather queries, and government schemes. Powered by RAG (Retrieval-Augmented Generation) for accurate, context-aware answers.

### 📊 Integrated AI Prediction Tools
- **Crop Recommendation** — suggests best crops based on soil NPK, pH, temperature, humidity, and rainfall
- **Yield Prediction** — estimates yield per hectare using historical and real-time agricultural data
- **Market Price Prediction** — data-driven crop price forecasts to help farmers maximize profits

### 💰 Affordable Pay-Per-Use Model
No upfront capital required. Small farmers access modern agricultural technology through affordable rentals, removing the high entry barrier.

### 🌍 Offline + Low Bandwidth Friendly
Designed with rural connectivity in mind — lightweight frontend, progressive loading, and minimal data requirements ensure inclusivity.

### 🔐 Secure Transactions
JWT-based authentication, role-based access control, HTTPS encryption, and cloud-hosted secure PostgreSQL storage.

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | React.js + Redux + Tailwind CSS |
| **Backend (Core)** | Spring Boot + Spring Security |
| **Backend (AI/ML)** | FastAPI + LangChain + LangGraph |
| **Database (Production)** | PostgreSQL via Neon Cloud |
| **Database (ML/Chatbot)** | SQLite |
| **Authentication** | JWT (Spring Security) |
| **AI Assistant** | Groq LLM (LLaMA 3) + Pinecone (Vector DB) |
| **Speech-to-Text** | Whisper (Faster-Whisper) |
| **Embeddings** | HuggingFace Sentence Transformers |
| **Payment** | Razorpay (optional / phase 2) |
| **Notifications** | SMS / WhatsApp API |
| **Weather** | OpenWeatherMap API |
| **Containerization** | Docker + Docker Compose |
| **Hosting** | Render Cloud (Backend) + Vercel (Frontend) |
| **Version Control** | GitHub |

---

## 🏗 System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Frontend (React + Redux)                  │
│              Hosted on Vercel — agri-connecti.vercel.app    │
└──────────────────────────┬──────────────────────────────────┘
                           │ REST API calls
           ┌───────────────┴──────────────────┐
           │                                  │
┌──────────▼──────────┐          ┌────────────▼────────────┐
│  Spring Boot API    │          │   FastAPI (AI/ML)       │
│  (Core Platform)    │          │   (Chatbot + Predict)   │
│  - Auth (JWT)       │          │   - AgriBot (RAG)       │
│  - Equipment APIs   │          │   - Crop Recommendation │
│  - Booking APIs     │          │   - Yield Prediction    │
│  - User Mgmt        │          │   - Price Prediction    │
└──────────┬──────────┘          └────────────┬────────────┘
           │                                  │
┌──────────▼──────────┐          ┌────────────▼────────────┐
│  PostgreSQL         │          │  Pinecone (Vector DB)   │
│  (Neon Cloud)       │          │  SQLite (Chat History)  │
│  - Users            │          │  Groq LLM (LLaMA 3)     │
│  - Equipment        │          │  HuggingFace Embeddings │
│  - Bookings         │          └─────────────────────────┘
└─────────────────────┘
```

### End-to-End Booking Flow

```
Farmer A (Lender)          Farmer B (Borrower)         Platform
     │                           │                         │
     │── List Equipment ────────►│                         │
     │                           │── Browse & Search ─────►│
     │                           │◄── Equipment List ──────│
     │                           │── Ask AgriBot ─────────►│
     │                           │◄── Tips & Advice ───────│
     │                           │── Select & Book ────────►│
     │                           │    (Payment via Razorpay)│
     │◄── Booking Notification ──│◄── Confirmation ────────│
     │                           │── Receive Equipment     │
     │                           │── Submit Feedback ──────►│
     │◄── Feedback Notified ─────│                         │
```

---

## 📦 Modules

### 1. 👤 User Accounts & Dashboards
- Farmer and Vendor registration with role-based profiles
- Secure login with JWT token management
- Farmer Dashboard: bookings, AI recommendations, chatbot access
- Vendor Dashboard: listed equipment, incoming bookings, earnings
- My Profile, My Bookings, Requested Services views

### 2. 🚜 Lending & Equipment Management
- Equipment listing with title, description, price/unit, category, location
- Supported categories: Tractor, Harvester, Seeder, Labour Services, Crop Residue Machines
- Availability management and pricing configuration
- Equipment discovery with filters (location, type, price)

### 3. 📅 Booking System
- Slot selection and booking confirmation
- Booking lifecycle: Pending → Booked → Completed / Cancelled
- Real-time availability locking during booking
- Booking history for both lenders and borrowers
- Mark-as-Completed workflow for service fulfillment
- SMS/WhatsApp booking confirmation notifications

### 4. 🤖 AI-Powered Assistance (ML Module)
- **Crop Recommendation**: Input soil parameters (N, P, K, pH, temperature, humidity, rainfall) → get the best crop suggestion
- **Yield Prediction**: Input crop type, season, state, area, fertilizer/pesticide usage → estimated yield per hectare
- **Price Prediction**: Input crop, season, state, soil type, cultivated area → estimated market price

### 5. 🎙 ChatBot + Voice Assistant (AgriBot)
- Voice-to-text input via Whisper (Faster-Whisper)
- Text-to-text conversational chat
- RAG pipeline using LangChain + Pinecone for factual, context-aware answers
- Personalization via SQLite chat history
- Supports agricultural FAQs, weather, soil, government schemes
- Built on Groq LLM (LLaMA 3) for fast, cost-effective inference

---

## 🧠 AI & ML Components

### Crop Recommendation System
```
Input:  N, P, K (soil nutrients), Temperature (°C),
        Humidity (%), pH Level, Rainfall (mm)
Model:  Classification ML model (scikit-learn / Random Forest)
Output: Recommended crop name
```

### Yield Prediction
```
Input:  Crop, Season, State, Crop Year, Area (hectares),
        Production (tonnes), Annual Rainfall (mm),
        Fertilizer Usage (kg), Pesticide Usage (kg)
Model:  Regression ML model
Output: Estimated yield (tonnes/hectare)
```

### Price Prediction
```
Input:  Crop, Season, State, Cultivated Area, Soil Type,
        Pesticide Usage, Soil pH Level, Temperature,
        Fertilizer Usage, Rainfall (mm)
Model:  Regression ML model
Output: Estimated market price (₹/quintal)
```

### AgriBot (Voice + Text RAG Chatbot)
```
Speech Input → Whisper STT → Text
Text → HuggingFace Embeddings → Pinecone Vector Search
                                      ↓
                              Relevant Context
                                      ↓
                    Groq LLM (LLaMA 3) + Prompt + History
                                      ↓
                              Contextual Response
```

**Technologies used in chatbot pipeline:**

| Component | Technology | Purpose |
|---|---|---|
| API Framework | FastAPI | Handle speech, text, file upload endpoints |
| Speech-to-Text | Whisper (Faster-Whisper) | Convert voice → text |
| Orchestration | LangChain + LangGraph | RAG pipeline & chat flow management |
| Vector DB | Pinecone | Store & retrieve document embeddings |
| Local Vector Search | FAISS (optional) | Alternative for PDF-based queries |
| Embeddings | HuggingFace Transformers | Convert text → numerical vectors |
| LLM | Groq (LLaMA 3) | Generate contextual, factual responses |
| Chat History | SQLite | Store session history for personalization |
| Knowledge Ingestion | PyPDF2 + Text Splitter | Process PDF documents into chunks |

---

## 🗄 Database Design

### PostgreSQL (Production — Neon Cloud)

**Core Tables:**
- `users` — id, name, email, password_hash, role (FARMER/VENDOR), phone, state, pincode, address
- `equipment` — id, owner_id, title, description, category, price, price_unit, state, city, is_available
- `bookings` — id, equipment_id, renter_id, booking_date, status (PENDING/BOOKED/COMPLETED/CANCELLED), total_amount
- `feedback` — id, booking_id, rating, comment, created_at

### SQLite (ML/Chatbot Service)
- `chat_sessions` — session_id, user_id, created_at
- `chat_messages` — id, session_id, role (user/assistant), content, timestamp

---

## 🔌 API Overview

### Spring Boot — Core APIs

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/auth/register` | Register new farmer/vendor |
| `POST` | `/api/auth/login` | Login and receive JWT |
| `GET` | `/api/equipment` | Browse all available equipment |
| `POST` | `/api/equipment` | List new equipment (Vendor) |
| `GET` | `/api/equipment?filters` | Filter equipment by type/location |
| `POST` | `/api/bookings` | Create a new booking |
| `GET` | `/api/bookings/my` | View my bookings |
| `PUT` | `/api/bookings/{id}/cancel` | Cancel a booking |
| `PUT` | `/api/bookings/{id}/complete` | Mark booking as completed |
| `POST` | `/api/feedback` | Submit rating and feedback |
| `GET` | `/api/profile` | Get current user profile |

---

## 🚀 Getting Started

### Prerequisites

- Node.js v18+
- Java 17+
- Maven 3.8+
- Docker & Docker Compose (optional)
- PostgreSQL (or use Neon Cloud free tier)

### 1. Clone the Repository

```bash
git clone https://github.com/adarshiiit0117/agriConnect.git
cd agriConnect
```

### 2. Backend — Spring Boot

```bash
cd backend/AgriConnect

# Configure your database in src/main/resources/application.properties
# (see Environment Variables section)

mvn clean install
mvn spring-boot:run
```

Backend runs at: `http://localhost:8080`

### 3. Frontend — React

```bash
cd frontend

npm install
npm run dev
```

Frontend runs at: `http://localhost:5173`

---

## 🐳 Docker Deployment

Run the entire stack with a single command:

```bash
docker-compose up --build
```

This starts:
- Spring Boot backend on port `8080`
- React frontend on port `3000`
- PostgreSQL on port `5432`

To stop:
```bash
docker-compose down
```

---

## ⚙️ Environment Variables

### Backend (`application.properties`)

```properties
# Database
spring.datasource.url=jdbc:postgresql://<neon-host>/<db-name>
spring.datasource.username=<db-user>
spring.datasource.password=<db-password>

# JWT
jwt.secret=<your-jwt-secret>
jwt.expiration=86400000

# Razorpay (optional)
razorpay.key.id=<your-key>
razorpay.key.secret=<your-secret>
```

### Frontend (`.env`)

```env
VITE_API_BASE_URL=http://localhost:8080
VITE_AI_SERVICE_URL=http://localhost:8000
VITE_RAZORPAY_KEY=<your-razorpay-key-id>
```

---

## 📁 Folder Structure

```
agriConnect/
│
├── frontend/AgriConnect-main/           # React + Tailwind CSS
│   ├── public/                          # Static assets
│   ├── src/
│   │   ├── State/                       # Redux state management
│   │   ├── assets/                      # Images, icons
│   │   ├── component/                   # Reusable UI components
│   │   ├── App.css
│   │   ├── App.jsx                      # Root component & routing
│   │   ├── index.css
│   │   └── main.jsx                     # React entry point
│   ├── .gitignore
│   ├── eslint.config.js
│   ├── index.html
│   ├── package.json
│   ├── package-lock.json
│   ├── postcss.config.js
│   ├── tailwind.config.js
│   └── vite.config.js
│
├── backend/AgriConnect/                 # Spring Boot
│   ├── .idea/
│   ├── .mvn/wrapper/
│   ├── src/                             # Java source code
│   │   └── main/java/com/agriconnect/
│   │       ├── controller/              # REST Controllers
│   │       ├── service/                 # Business logic
│   │       ├── repository/              # JPA Repositories
│   │       ├── model/                   # Entity classes
│   │       ├── dto/                     # Data Transfer Objects
│   │       └── security/                # JWT + Spring Security
│   ├── target/classes/
│   ├── .dockerignore
│   ├── Dockerfile
│   ├── mvnw
│   ├── mvnw.cmd
│   └── pom.xml
│
├── IdeationAndPitch_Adarsh_Dubey.pdf
├── Software_requirement_specification.pdf
├── detailed_project_overview.pdf
└── README.md
```

---

## 🏛 Design Principles

### Microservices-Oriented Architecture
Each core function — Authentication, Equipment Booking, Crop Prediction, Chatbot — is designed as an independent, loosely coupled service. This enables independent scaling, deployment, and maintenance.

### Agile Development
Iterative and incremental development allowing continuous feedback, quick feature delivery, and adaptability to real farmer needs.

### Separation of Concerns
Clear division between frontend, backend core, and AI/ML service layers ensures modularity and reduces cross-cutting complexity.

### Loose Coupling & High Cohesion

| Module | Coupling | Cohesion |
|---|---|---|
| User Accounts & Dashboards | Low (Auth only) | High — all user-related tasks |
| Booking System | Medium (requires Auth + Equipment) | High — purely booking tasks |
| AI-Powered Assistance | Low (data inputs only) | High — crop intelligence only |
| AgriBot | Low (API-based) | Medium — navigation + agri queries |

### Cloud-Native
Containerized with Docker and deployed on Render Cloud + Vercel for scalability, resilience, and zero-downtime deployments.

---

## 📐 Non-Functional Requirements

| Attribute | Specification |
|---|---|
| **Availability** | 99.5% uptime via Docker + Render auto-scaling |
| **Performance** | Booking/chatbot responses under 3 seconds |
| **Scalability** | Supports 1,000+ concurrent users; expandable via microservices |
| **Security** | JWT auth, RBAC, HTTPS, encrypted PostgreSQL storage |
| **Usability** | Farmer-friendly UI, multilingual, fully mobile-responsive |
| **Accessibility** | Semantic HTML, ARIA labels, keyboard navigation |
| **Reliability** | Docker container orchestration with health checks |

---

## 🗺 Future Roadmap

- [ ] **Mobile App** (React Native) for offline-first farmer access
- [ ] **Razorpay Full Integration** — live payment processing
- [ ] **WhatsApp / SMS Notifications** — booking alerts via Twilio / MSG91
- [ ] **Geo-Location Equipment Discovery** — map-based equipment finder
- [ ] **Government Scheme Integration** — direct PM-Kisan and subsidy information via chatbot
- [ ] **Multilingual UI** — full Hindi, Punjabi, Marathi, Telugu support
- [ ] **Admin Dashboard** — platform analytics, dispute resolution
- [ ] **Weather-Based Scheduling** — smart booking recommendations based on forecast
- [ ] **Crop Insurance Advisory** — AI-powered risk assessment for farmers

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

```bash
# Fork the repository
# Create your feature branch
git checkout -b feature/your-feature-name

# Commit your changes
git commit -m "feat: add your feature description"

# Push to the branch
git push origin feature/your-feature-name

# Open a Pull Request
```

Please follow conventional commit messages and ensure all new features include relevant API documentation updates.

---

## 👨‍💻 Team

**Adarsh Dubey** — Full Stack Developer & ML Engineer  
IIIT Kottayam  
GitHub: [@adarshiiit0117](https://github.com/adarshiiit0117)



---


<div align="center">

**🌾 AgriConnect — Growing Tomorrow, Together**

[![Live Demo](https://img.shields.io/badge/Try%20It-agri--connecti.vercel.app-40916c?style=for-the-badge)](https://agri-connecti.vercel.app/)

*Made with ❤️ for Indian farmers*

</div>
