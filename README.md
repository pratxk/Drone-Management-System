# 🚁 Drone Management System

A comprehensive, full-stack drone management platform for mission planning, fleet management, real-time monitoring, and analytics. Built with modern technologies for scalability, security, and performance.

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Quick Start](#quick-start)
- [Backend (Falcon) Setup](#backend-falcon-setup)
- [Frontend (Redwing) Setup](#frontend-redwing-setup)
- [Environment Configuration](#environment-configuration)
- [Database Setup](#database-setup)
- [Authentication](#authentication)
- [API Documentation](#api-documentation)
- [Deployment](#deployment)
- [Development](#development)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

The Drone Management System is a complete solution for organizations managing drone fleets. It provides:

- **Mission Planning**: Create, schedule, and manage drone missions
- **Fleet Management**: Monitor and control drone fleets in real-time
- **Site Management**: Manage operational sites and locations
- **User Management**: Role-based access control for team members
- **Real-time Monitoring**: Live tracking and status updates
- **Analytics**: Comprehensive reporting and performance metrics
- **WebSocket Integration**: Real-time communication with drones

## 🏗️ Architecture

The application follows a modern microservices-inspired architecture:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Backend       │    │   Database      │
│   (Redwing)     │◄──►│   (Falcon)      │◄──►│   (PostgreSQL)  │
│   Next.js 15    │    │   Node.js 18    │    │   + Redis       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │              ┌─────────────────┐              │
         └──────────────►│   WebSocket     │◄─────────────┘
                        │   Server        │
                        │   Real-time     │
                        └─────────────────┘
```

### Key Components:

- **Falcon (Backend)**: GraphQL API server with authentication, caching, and real-time features
- **Redwing (Frontend)**: Modern React application with TypeScript and real-time updates
- **Database**: PostgreSQL with Prisma ORM for data persistence
- **Cache**: Redis for session management and query caching
- **WebSocket**: Real-time communication for live drone updates

## ✨ Features

### 🎯 Mission Management
- Create and schedule drone missions
- Define waypoints and flight paths
- Real-time mission status tracking
- Mission history and analytics
- Automated mission execution

### 🚁 Drone Fleet Management
- Register and manage drone fleets
- Real-time drone status monitoring
- Battery level and GPS tracking
- Drone health monitoring
- Fleet utilization analytics

### 🗺️ Site Management
- Manage operational sites
- Site-specific mission planning
- Geographic data integration
- Site performance metrics

### 👥 User Management
- Role-based access control (RBAC)
- Organization-based user management
- User activity tracking
- Secure authentication system

### 📊 Analytics & Reporting
- Mission success rates
- Fleet utilization metrics
- Performance analytics
- Custom report generation
- Real-time dashboards

### 🔄 Real-time Features
- Live drone position tracking
- Real-time mission updates
- WebSocket-based communication
- Instant notifications

## 🛠️ Tech Stack

### Backend (Falcon)
- **Runtime**: Node.js 18
- **Framework**: Express.js 5
- **API**: GraphQL with Apollo Server
- **Database**: PostgreSQL with Prisma ORM
- **Cache**: Redis with ioredis
- **Authentication**: JWT with bcrypt
- **Real-time**: WebSocket (ws)
- **Validation**: Joi
- **Logging**: Winston
- **Testing**: Jest

### Frontend (Redwing)
- **Framework**: Next.js 15 with React 18
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **UI Components**: shadcn/ui
- **State Management**: React Context + Apollo Client
- **GraphQL Client**: Apollo Client
- **Real-time**: WebSocket integration
- **Charts**: Recharts
- **Icons**: Lucide React
- **Forms**: React Hook Form

### Infrastructure
- **Database**: PostgreSQL
- **Cache**: Redis
- **Containerization**: Docker
- **Deployment**: Vercel (Frontend), Render (Backend)

## 📁 Project Structure

```
Drone-Management_system/
├── falcon/                    # Backend API Server
│   ├── src/
│   │   ├── graphql/          # GraphQL schema and resolvers
│   │   ├── middleware/       # Authentication middleware
│   │   ├── routes/           # REST API routes
│   │   ├── utils/            # Utility functions
│   │   └── websocket/        # WebSocket server
│   ├── prisma/               # Database schema and migrations
│   ├── docs/                 # API documentation
│   └── Dockerfile            # Container configuration
│
├── redwing/                   # Frontend Application
│   ├── src/
│   │   ├── app/              # Next.js app router pages
│   │   ├── components/       # React components
│   │   ├── features/         # Feature-based modules
│   │   ├── hooks/            # Custom React hooks
│   │   ├── lib/              # Utility libraries
│   │   └── types/            # TypeScript type definitions
│   ├── public/               # Static assets
│   └── next.config.ts        # Next.js configuration
│
└── README.md                 # This file
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- Yarn package manager
- PostgreSQL database
- Redis server
- Docker (optional)

### 1. Clone the Repository
```bash
git clone <repository-url>
cd Drone-Management_system
```

### 2. Backend Setup
```bash
cd falcon
yarn install
cp .env.example .env
# Configure your environment variables
yarn prisma:generate
yarn prisma:migrate
yarn dev
```

### 3. Frontend Setup
```bash
cd redwing
yarn install
cp .env.local.example .env.local
# Configure your environment variables
yarn dev
```

## 🔧 Backend (Falcon) Setup

### Installation
```bash
cd falcon
yarn install
```

### Environment Configuration
Create a `.env` file in the `falcon` directory:

```env
# Database
DATABASE_URL="postgresql://username:password@localhost:5432/drone_management"

# Redis
REDIS_URL="redis://localhost:6379"

# JWT
JWT_SECRET="your-super-secret-jwt-key"

# Server
PORT=4000
NODE_ENV=development

# CORS
CORS_ORIGIN="http://localhost:3000"
```

### Database Setup
```bash
# Generate Prisma client
yarn prisma:generate

# Run migrations
yarn prisma:migrate

# Seed database (optional)
yarn prisma:seed
```

### Running the Server
```bash
# Development
yarn dev

# Production
yarn build
yarn start
```

### Docker Deployment
```bash
# Build image
docker build -t falcon-backend .

# Run container
docker run -p 4000:4000 falcon-backend
```

## 🎨 Frontend (Redwing) Setup

### Installation
```bash
cd redwing
yarn install
```

### Environment Configuration
Create a `.env.local` file in the `redwing` directory:

```env
# API Configuration
NEXT_PUBLIC_GRAPHQL_URL="http://localhost:4000/graphql"
NEXT_PUBLIC_API_URL="http://localhost:4000/api"
NEXT_PUBLIC_WS_URL="ws://localhost:4000/ws"

# Authentication
NEXTAUTH_SECRET="your-nextauth-secret"
NEXTAUTH_URL="http://localhost:3000"
```

### Running the Application
```bash
# Development
yarn dev

# Production build
yarn build
yarn start
```

## 🔐 Authentication

The system uses JWT-based authentication with role-based access control:

### User Roles
- **SUPER_ADMIN**: Full system access
- **ADMIN**: Organization-level management
- **MODERATOR**: Mission and drone management
- **OPERATOR**: Mission execution and monitoring
- **VIEWER**: Read-only access

### Authentication Flow
1. User logs in with email/password
2. Backend validates credentials and returns JWT token
3. Frontend stores token in secure HTTP-only cookie
4. Token is automatically included in all API requests
5. Backend validates token and checks user permissions

## 📚 API Documentation

### GraphQL Endpoint
- **URL**: `http://localhost:4000/graphql`
- **Playground**: `http://localhost:4000/graphql` (in development)

### Key Queries
```graphql
# Get user information
query Me {
  me {
    id
    email
    firstName
    lastName
    role
    organizationMemberships {
      organization {
        id
        name
      }
    }
  }
}

# Get missions
query Missions {
  missions {
    id
    name
    status
    createdAt
    waypoints {
      id
      latitude
      longitude
      altitude
    }
  }
}

# Get drones
query Drones {
  drones {
    id
    name
    status
    batteryLevel
    currentLatitude
    currentLongitude
  }
}
```

### Key Mutations
```graphql
# Login
mutation Login($email: String!, $password: String!) {
  login(email: $email, password: $password) {
    token
    user {
      id
      email
      role
    }
  }
}

# Create mission
mutation CreateMission($input: CreateMissionInput!) {
  createMission(input: $input) {
    id
    name
    status
  }
}
```

## 🚀 Deployment

### Backend Deployment (Render)
1. Connect your GitHub repository
2. Set environment variables
3. Configure build command: `yarn install && yarn build`
4. Configure start command: `yarn start`

### Frontend Deployment (Vercel)
1. Connect your GitHub repository
2. Set environment variables
3. Deploy automatically on push to main branch

### Environment Variables for Production

**Backend (.env)**
```env
DATABASE_URL="your-production-database-url"
REDIS_URL="your-production-redis-url"
JWT_SECRET="your-production-jwt-secret"
NODE_ENV=production
CORS_ORIGIN="https://your-frontend-domain.com"
```

**Frontend (.env.local)**
```env
NEXT_PUBLIC_GRAPHQL_URL="https://your-backend-domain.com/graphql"
NEXT_PUBLIC_API_URL="https://your-backend-domain.com/api"
NEXT_PUBLIC_WS_URL="wss://your-backend-domain.com/ws"
```

## 🛠️ Development

### Code Style
- **Backend**: ESLint + Prettier
- **Frontend**: ESLint + Prettier + TypeScript strict mode

### Testing
```bash
# Backend tests
cd falcon
yarn test

# Frontend tests
cd redwing
yarn test
```

### Database Migrations
```bash
cd falcon
# Create new migration
yarn prisma:migrate dev --name migration_name

# Apply migrations
yarn prisma:migrate deploy
```

### Real-time Development
The application supports real-time updates through WebSocket connections:

1. **Backend WebSocket Server**: Handles real-time drone updates
2. **Frontend WebSocket Client**: Receives and displays live updates
3. **Mission Updates**: Real-time mission status changes
4. **Drone Tracking**: Live position and status updates

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines
- Follow TypeScript best practices
- Write comprehensive tests
- Update documentation
- Follow the existing code style
- Ensure all tests pass before submitting

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support and questions:
- Create an issue in the GitHub repository
- Check the documentation in the `docs/` folder
- Review the API documentation at `/graphql` endpoint

## 🔮 Roadmap

- [ ] Mobile application (React Native)
- [ ] Advanced analytics dashboard
- [ ] Machine learning for mission optimization
- [ ] Integration with external drone APIs
- [ ] Multi-tenant architecture
- [ ] Advanced reporting features
- [ ] Real-time video streaming
- [ ] Weather integration
- [ ] Automated flight planning
- [ ] Fleet maintenance scheduling

---

**Built with ❤️ for the drone industry**