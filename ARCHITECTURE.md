# OctoFit Tracker - Architecture Documentation

## Overview

The OctoFit Tracker is a modern, full-stack web application built using a three-tier architecture pattern, separating the presentation layer (React frontend), business logic layer (Django REST API), and data layer (MongoDB).

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                      GitHub Codespaces                       │
│  ┌───────────────────────────────────────────────────────┐  │
│  │                    Development Environment             │  │
│  │  ┌─────────────┐  ┌──────────────┐  ┌─────────────┐  │  │
│  │  │   VS Code   │  │  Port 3000   │  │  Port 8000  │  │  │
│  │  │   + Copilot │  │  (React)     │  │  (Django)   │  │  │
│  │  └─────────────┘  └──────────────┘  └─────────────┘  │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌───────────────┐    ┌─────────────────┐    ┌─────────────┐
│ React Frontend│◄───┤  Django REST    │◄───┤   MongoDB   │
│  (Port 3000)  │    │  API Framework  │    │ (Port 27017)│
│               │───►│  (Port 8000)    │───►│             │
└───────────────┘    └─────────────────┘    └─────────────┘
   Presentation           Business Logic        Data Layer
```

## Component Architecture

### 1. Frontend Layer (React)

**Technology**: React.js 18+ with React Router and Bootstrap

**Location**: `octofit-tracker/frontend/`

**Key Components**:
- `App.js`: Main application component with routing
- `components/Users.js`: User profile management
- `components/Activities.js`: Activity logging and display
- `components/Teams.js`: Team creation and management
- `components/Leaderboard.js`: Competitive rankings
- `components/Workouts.js`: Workout suggestions

**Responsibilities**:
- User interface rendering
- User interaction handling
- HTTP requests to backend API
- Client-side routing
- State management

**Communication**:
- Makes RESTful API calls to Django backend on port 8000
- Uses environment variable `REACT_APP_CODESPACE_NAME` for dynamic API URL construction
- Handles both paginated and non-paginated API responses

### 2. Backend Layer (Django REST Framework)

**Technology**: Python 3.x, Django 4.1.7, Django REST Framework 3.14.0

**Location**: `octofit-tracker/backend/octofit_tracker/`

**Key Files**:
- `settings.py`: Application configuration and database connection
- `models.py`: Data models (Users, Teams, Activities, Leaderboard, Workouts)
- `serializers.py`: JSON serialization/deserialization
- `views.py`: API endpoint logic
- `urls.py`: URL routing configuration
- `admin.py`: Django admin interface configuration

**Responsibilities**:
- REST API endpoint implementation
- Business logic processing
- Data validation and serialization
- Database operations via Django ORM
- CORS handling for frontend requests

**API Endpoints**:
```
GET/POST  /api/users/        - User management
GET/POST  /api/activities/   - Activity tracking
GET/POST  /api/teams/        - Team operations
GET       /api/leaderboard/  - Rankings
GET/POST  /api/workouts/     - Workout suggestions
```

**Communication**:
- Listens on port 8000
- Accepts requests from React frontend (port 3000)
- Communicates with MongoDB on port 27017
- Uses Djongo ORM for MongoDB integration

### 3. Data Layer (MongoDB)

**Technology**: MongoDB 6.x

**Database**: `octofit_db`

**Collections**:

#### Users Collection
```javascript
{
  _id: ObjectId,
  username: String,
  email: String (unique index),
  first_name: String,
  last_name: String,
  profile_info: String,
  created_at: Date
}
```

#### Teams Collection
```javascript
{
  _id: ObjectId,
  name: String,
  description: String,
  members: [ObjectId],  // References to Users
  created_at: Date
}
```

#### Activities Collection
```javascript
{
  _id: ObjectId,
  user_id: ObjectId,    // Reference to User
  activity_type: String,
  duration: Number,     // in minutes
  distance: Number,     // in miles/km
  calories: Number,
  date: Date,
  notes: String
}
```

#### Leaderboard Collection
```javascript
{
  _id: ObjectId,
  user_id: ObjectId,    // Reference to User
  team_id: ObjectId,    // Reference to Team
  total_points: Number,
  rank: Number,
  last_updated: Date
}
```

#### Workouts Collection
```javascript
{
  _id: ObjectId,
  name: String,
  description: String,
  difficulty: String,   // beginner, intermediate, advanced
  category: String,     // strength, cardio, flexibility
  duration: Number,     // in minutes
  instructions: String
}
```

**Responsibilities**:
- Persistent data storage
- Data indexing and querying
- Data integrity through unique indexes
- Document-based storage for flexibility

## Data Flow

### Example: Viewing Leaderboard

```
1. User clicks "Leaderboard" in React UI
   └─► React Router navigates to /leaderboard

2. Leaderboard component mounts
   └─► useEffect() triggers

3. Fetch request sent to backend
   └─► GET https://${CODESPACE_NAME}-8000.app.github.dev/api/leaderboard/

4. Django receives request
   └─► urls.py routes to LeaderboardViewSet
   └─► views.py executes list() method
   └─► models.py Leaderboard.objects.all()

5. Djongo translates to MongoDB query
   └─► db.leaderboard.find({})

6. MongoDB returns documents
   └─► Djongo converts to Django model instances

7. Django serializes data
   └─► serializers.py LeaderboardSerializer
   └─► Converts ObjectId to strings

8. JSON response sent to frontend
   └─► Status 200 with leaderboard data

9. React receives and processes response
   └─► Updates component state
   └─► Re-renders with new data

10. User sees leaderboard table
    └─► Bootstrap-styled table displays rankings
```

## Security Considerations

### Current Configuration (Development)

⚠️ **Note**: The current configuration is for development/learning purposes only.

- CORS is configured to allow all origins (`CORS_ALLOW_ALL_ORIGINS = True`)
- No authentication/authorization implemented
- MongoDB runs without authentication
- All hosts are allowed in Django (`ALLOWED_HOSTS = ['*']`)

### Production Recommendations

For a production deployment, implement:

1. **Authentication & Authorization**
   - Django REST Framework token authentication
   - JWT tokens for stateless authentication
   - Role-based access control (students, teachers, admins)

2. **CORS Configuration**
   - Restrict `CORS_ALLOWED_ORIGINS` to specific domains
   - Use environment variables for allowed origins

3. **Database Security**
   - Enable MongoDB authentication
   - Use strong passwords
   - Implement role-based access control in MongoDB
   - Encrypt sensitive data

4. **HTTPS**
   - Enforce HTTPS for all communications
   - Use proper SSL/TLS certificates

5. **Input Validation**
   - Validate all user inputs
   - Sanitize data before database storage
   - Implement rate limiting

## Scalability Considerations

### Current Limitations
- Single server architecture
- No caching layer
- Direct database connections

### Potential Improvements

1. **Horizontal Scaling**
   - Deploy multiple Django instances behind a load balancer
   - Use session storage (Redis) for shared state

2. **Caching**
   - Implement Redis for frequently accessed data
   - Cache leaderboard calculations
   - Use CDN for static assets

3. **Database Optimization**
   - Add appropriate indexes for frequent queries
   - Implement database sharding for large datasets
   - Use read replicas for read-heavy operations

4. **Microservices**
   - Separate activity tracking from user management
   - Dedicated service for leaderboard calculations
   - Event-driven architecture for real-time updates

## Development Workflow

### Local Development with Codespaces

1. **Environment Setup**
   - Codespace automatically runs `post_create.sh` and `post_start.sh`
   - Installs MongoDB, Node.js, and Python dependencies
   - Configures port forwarding (3000, 8000, 27017)

2. **Running the Application**
   - **Backend**: Use VS Code debugger "Launch Django Backend"
   - **Frontend**: Use VS Code debugger "Launch React Frontend"
   - **Database**: MongoDB service starts automatically

3. **Environment Variables**
   - `CODESPACE_NAME`: Auto-injected by GitHub Codespaces
   - `REACT_APP_CODESPACE_NAME`: Passed to React for API URL construction

### Custom Instructions & Prompts

The project uses GitHub Copilot's custom instructions feature:

- **Instructions** (`.github/instructions/`): Define "how" to perform tasks
- **Prompts** (`.github/prompts/`): Define "what" needs to be done

This separation allows for:
- Reusable development patterns
- Consistent code generation
- Team-wide best practices

## Technology Choices Rationale

| Technology | Reason |
|-----------|--------|
| **React** | Component-based architecture, large ecosystem, beginner-friendly |
| **Django REST Framework** | Rapid API development, batteries-included, strong ORM |
| **MongoDB** | Flexible schema, document-based storage suitable for evolving data models |
| **GitHub Codespaces** | Zero-setup development environment, cloud-based, consistent across users |
| **Bootstrap** | Quick UI development, responsive design, minimal CSS knowledge needed |

## Future Enhancements

1. **Real-time Features**
   - WebSocket integration for live leaderboard updates
   - Real-time activity notifications

2. **Mobile Application**
   - React Native mobile app
   - Native iOS/Android apps

3. **Advanced Analytics**
   - Dashboard with charts and graphs
   - Progress tracking over time
   - Predictive workout suggestions using ML

4. **Social Features**
   - Activity sharing
   - Team chat functionality
   - Achievement badges and rewards

5. **Integration**
   - Fitness tracker integration (Fitbit, Apple Health)
   - Calendar integration for workout scheduling
   - Email/SMS notifications
