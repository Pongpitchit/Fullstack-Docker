# Full-Stack-Deployment-with-Docker-Compose

A full-stack application built with Next.js frontend, Express.js API, and MySQL database, all containerized with Docker Compose.

## Project Structure

```
Fullstack-Docker/
├── api/              # Express.js backend API
├── frontend/         # Next.js frontend application
├── docker-compose.yml # Docker Compose configuration
└── init.sql          # Database initialization script
```

## Tech Stack

- **Frontend**: Next.js 15.5.0, React 19.1.0, TypeScript, Tailwind CSS
- **Backend API**: Express.js 5.1.0, Node.js
- **Database**: MySQL 8.0
- **Containerization**: Docker & Docker Compose

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- `.env.local` file with environment variables (see docker-compose.yml for required variables)

### Running with Docker Compose

```bash
docker-compose up -d
```

This will start:
- MySQL database on port 3306
- phpMyAdmin on port 8080
- Express API on port 5000
- Next.js frontend on port 3000

### Accessing the Application

- **Frontend**: http://localhost:3000
- **API**: http://localhost:5000
- **phpMyAdmin**: http://localhost:8080

---

## API Documentation

### Backend API (Express.js)

Base URL: `http://localhost:5000`

#### Health Check

**GET** `/health`

Check API and database connectivity.

**Response:**
```json
{
  "status": "ok",
  "db": true
}
```

#### Attractions

**GET** `/attractions`

Get all attractions from the database.

**Response:**
```json
[
  {
    "id": 1,
    "name": "Phi Phi Islands",
    "detail": "Phi Phi Islands are a group of islands...",
    "coverimage": "https://www.melivecode.com/attractions/1.jpg",
    "latitude": 7.737619,
    "longitude": 98.7068755
  }
]
```

---

### Frontend API Routes (Next.js)

Base URL: `http://localhost:3000/api`

#### Attractions

**GET** `/api/attractions`

Get all attractions, ordered by ID descending.

**Response:**
```json
[
  {
    "id": 12,
    "name": "Wat Phra Kaew",
    "detail": "Wat Phra Kaew, commonly known...",
    "coverimage": "https://www.melivecode.com/attractions/12.jpg",
    "latitude": 13.751389,
    "longitude": 100.4925
  }
]
```

**GET** `/api/attractions/[id]`

Get a single attraction by ID.

**Parameters:**
- `id` (number): The attraction ID

**Response:**
```json
{
  "id": 1,
  "name": "Phi Phi Islands",
  "detail": "Phi Phi Islands are a group of islands...",
  "coverimage": "https://www.melivecode.com/attractions/1.jpg",
  "latitude": 7.737619,
  "longitude": 98.7068755
}
```

**Error Responses:**
- `400`: Invalid ID format
- `404`: Attraction not found
- `500`: Internal server error

---

## Frontend Pages

### Public Pages

#### Home (`/`)

Main dashboard displaying attractions in a grid layout.

**Features:**
- Attraction cards with images
- Gradient hero section
- Responsive design

#### Attractions (`/attractions`)

Full attractions listing page with detailed information.

**Features:**
- Grid view of all attractions
- Navigation bar
- Link to individual attraction details

#### Attraction Detail (`/attractions/[id]`)

Individual attraction detail page showing complete information about a specific attraction.

**Features:**
- Full attraction details
- Image display
- Location coordinates
- Back navigation

### User Management Pages

**Note:** User management pages use an external API (melivecode.com) for demonstration purposes.

#### Users List (`/users`)

Display all users with management options.

**Features:**
- User list with cards
- Create new user button
- Edit and delete actions
- User detail links

#### Create User (`/users/create`)

Form to create a new user.

**Features:**
- User creation form
- Validation
- Redirect to users list after creation

#### User Detail (`/users/[id]`)

View individual user details.

**Features:**
- User information display
- Edit and delete buttons
- Back navigation

#### Edit User (`/users/[id]/edit`)

Edit existing user information.

**Features:**
- Pre-filled form with user data
- Update functionality
- Redirect to users list after update

### Example/Demo Pages

#### State Management (`/01_state`)

Demonstrates React state management with attractions viewer.

**Features:**
- Netflix-style grid layout
- State-driven rendering
- Attraction cards

#### Events & Props (`/02_event_pops`)

Example page showing React events and props usage.

#### useEffect Hook (`/03_use_effect`)

Demonstrates the `useEffect` hook with API data fetching.

#### Array of Objects (`/array_of_objects`)

Example page demonstrating working with arrays of objects and API data.

---

## Database Schema

### Attraction Table

```sql
CREATE TABLE `attraction` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(191) NOT NULL,
  `detail` varchar(191) NOT NULL,
  `coverimage` varchar(191) DEFAULT NULL,
  `latitude` double NOT NULL,
  `longitude` double NOT NULL,
  PRIMARY KEY (`id`)
)
```

**Sample Data:**
- 12 pre-loaded attractions including:
  - Phi Phi Islands (Thailand)
  - Eiffel Tower (France)
  - Times Square (USA)
  - Mount Fuji (Japan)
  - Big Ben (UK)
  - Taj Mahal (India)
  - And more...

---

## Development

### Running Frontend Locally

```bash
cd frontend
npm install
npm run dev
```

### Running API Locally

```bash
cd api
npm install
npm start
```

**Note:** Make sure MySQL is running and environment variables are configured.

---

## Environment Variables

Required environment variables (configure in `.env.local` or docker-compose.yml):

- `DB_HOST`: Database host (default: localhost)
- `DB_PORT`: Database port (default: 3306)
- `DB_NAME`: Database name
- `DB_USER`: Database user
- `DB_PASSWORD`: Database password
- `MYSQL_ROOT_PASSWORD`: MySQL root password
- `PORT`: API port (default: 5000)
- `CORS_ORIGIN`: Allowed CORS origin (default: *)

---

## Docker Services

The application consists of 4 Docker services:

1. **mysql**: MySQL 8.0 database
2. **phpmyadmin**: Database management interface
3. **api**: Express.js REST API
4. **frontend**: Next.js application

All services run on a shared Docker network called `stack`.

---

