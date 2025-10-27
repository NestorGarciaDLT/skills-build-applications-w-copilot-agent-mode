# OctoFit Tracker API Documentation

## Base URL

The API is accessible at:
- **Development**: `https://{CODESPACE_NAME}-8000.app.github.dev/api/`
- **Local**: `http://localhost:8000/api/`

Replace `{CODESPACE_NAME}` with your actual GitHub Codespace name.

## API Overview

The OctoFit Tracker REST API provides endpoints for managing users, teams, activities, leaderboard, and workout suggestions. All endpoints return JSON data.

### Response Format

#### Successful Response
```json
{
  "id": "507f1f77bcf86cd799439011",
  "field1": "value1",
  "field2": "value2"
}
```

#### Paginated Response
Some endpoints may return paginated results:
```json
{
  "count": 100,
  "next": "https://{CODESPACE_NAME}-8000.app.github.dev/api/endpoint/?page=2",
  "previous": null,
  "results": [...]
}
```

#### Error Response
```json
{
  "error": "Error message",
  "detail": "Detailed error information"
}
```

## Authentication

**Current Status**: No authentication required (development mode)

**Production Recommendation**: Implement token-based authentication using Django REST Framework's TokenAuthentication or JWT.

## API Endpoints

### Root Endpoint

#### GET /api/

Returns a list of all available API endpoints.

**Response:**
```json
{
  "users": "https://{CODESPACE_NAME}-8000.app.github.dev/api/users/",
  "teams": "https://{CODESPACE_NAME}-8000.app.github.dev/api/teams/",
  "activities": "https://{CODESPACE_NAME}-8000.app.github.dev/api/activities/",
  "leaderboard": "https://{CODESPACE_NAME}-8000.app.github.dev/api/leaderboard/",
  "workouts": "https://{CODESPACE_NAME}-8000.app.github.dev/api/workouts/"
}
```

---

## Users

Manage user profiles and information.

### List Users

#### GET /api/users/

Retrieve a list of all users.

**Request:**
```bash
curl -X GET https://{CODESPACE_NAME}-8000.app.github.dev/api/users/
```

**Response:**
```json
[
  {
    "id": "507f1f77bcf86cd799439011",
    "username": "ironman",
    "email": "tony.stark@avengers.com",
    "first_name": "Tony",
    "last_name": "Stark",
    "profile_info": "Genius, billionaire, playboy, philanthropist",
    "created_at": "2025-01-15T10:30:00Z"
  },
  {
    "id": "507f1f77bcf86cd799439012",
    "username": "captainamerica",
    "email": "steve.rogers@avengers.com",
    "first_name": "Steve",
    "last_name": "Rogers",
    "profile_info": "Super soldier, leader of the Avengers",
    "created_at": "2025-01-15T10:31:00Z"
  }
]
```

### Get User

#### GET /api/users/{id}/

Retrieve a specific user by ID.

**Request:**
```bash
curl -X GET https://{CODESPACE_NAME}-8000.app.github.dev/api/users/507f1f77bcf86cd799439011/
```

**Response:**
```json
{
  "id": "507f1f77bcf86cd799439011",
  "username": "ironman",
  "email": "tony.stark@avengers.com",
  "first_name": "Tony",
  "last_name": "Stark",
  "profile_info": "Genius, billionaire, playboy, philanthropist",
  "created_at": "2025-01-15T10:30:00Z"
}
```

### Create User

#### POST /api/users/

Create a new user.

**Request:**
```bash
curl -X POST https://{CODESPACE_NAME}-8000.app.github.dev/api/users/ \
  -H "Content-Type: application/json" \
  -d '{
    "username": "spiderman",
    "email": "peter.parker@avengers.com",
    "first_name": "Peter",
    "last_name": "Parker",
    "profile_info": "Friendly neighborhood Spider-Man"
  }'
```

**Response:**
```json
{
  "id": "507f1f77bcf86cd799439013",
  "username": "spiderman",
  "email": "peter.parker@avengers.com",
  "first_name": "Peter",
  "last_name": "Parker",
  "profile_info": "Friendly neighborhood Spider-Man",
  "created_at": "2025-01-15T11:00:00Z"
}
```

### Update User

#### PUT /api/users/{id}/

Update an existing user.

**Request:**
```bash
curl -X PUT https://{CODESPACE_NAME}-8000.app.github.dev/api/users/507f1f77bcf86cd799439013/ \
  -H "Content-Type: application/json" \
  -d '{
    "username": "spiderman",
    "email": "peter.parker@avengers.com",
    "first_name": "Peter",
    "last_name": "Parker",
    "profile_info": "Your friendly neighborhood Spider-Man with new web shooters!"
  }'
```

### Delete User

#### DELETE /api/users/{id}/

Delete a user.

**Request:**
```bash
curl -X DELETE https://{CODESPACE_NAME}-8000.app.github.dev/api/users/507f1f77bcf86cd799439013/
```

**Response:** 204 No Content

---

## Teams

Manage fitness teams.

### List Teams

#### GET /api/teams/

Retrieve a list of all teams.

**Response:**
```json
[
  {
    "id": "507f1f77bcf86cd799439021",
    "name": "Team Marvel",
    "description": "Earth's Mightiest Heroes",
    "members": [
      "507f1f77bcf86cd799439011",
      "507f1f77bcf86cd799439012"
    ],
    "created_at": "2025-01-15T09:00:00Z"
  }
]
```

### Create Team

#### POST /api/teams/

Create a new team.

**Request:**
```bash
curl -X POST https://{CODESPACE_NAME}-8000.app.github.dev/api/teams/ \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Team DC",
    "description": "Justice League members",
    "members": []
  }'
```

---

## Activities

Track physical activities.

### List Activities

#### GET /api/activities/

Retrieve a list of all activities.

**Query Parameters:**
- `user_id` (optional): Filter activities by user ID
- `activity_type` (optional): Filter by activity type
- `date` (optional): Filter by date (YYYY-MM-DD format)

**Response:**
```json
[
  {
    "id": "507f1f77bcf86cd799439031",
    "user_id": "507f1f77bcf86cd799439011",
    "activity_type": "running",
    "duration": 45,
    "distance": 5.2,
    "calories": 450,
    "date": "2025-01-15",
    "notes": "Morning run in the park"
  },
  {
    "id": "507f1f77bcf86cd799439032",
    "user_id": "507f1f77bcf86cd799439012",
    "activity_type": "strength_training",
    "duration": 60,
    "distance": 0,
    "calories": 320,
    "date": "2025-01-15",
    "notes": "Full body workout at the gym"
  }
]
```

### Create Activity

#### POST /api/activities/

Log a new activity.

**Request:**
```bash
curl -X POST https://{CODESPACE_NAME}-8000.app.github.dev/api/activities/ \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "507f1f77bcf86cd799439011",
    "activity_type": "cycling",
    "duration": 30,
    "distance": 8.5,
    "calories": 280,
    "date": "2025-01-16",
    "notes": "Evening bike ride"
  }'
```

**Activity Types:**
- `running`
- `walking`
- `cycling`
- `swimming`
- `strength_training`
- `yoga`
- `other`

### Get Activity

#### GET /api/activities/{id}/

Retrieve a specific activity.

### Update Activity

#### PUT /api/activities/{id}/

Update an existing activity.

### Delete Activity

#### DELETE /api/activities/{id}/

Delete an activity.

---

## Leaderboard

View competitive rankings.

### Get Leaderboard

#### GET /api/leaderboard/

Retrieve the current leaderboard rankings.

**Query Parameters:**
- `team_id` (optional): Filter by team
- `limit` (optional): Limit number of results (default: 100)

**Response:**
```json
[
  {
    "id": "507f1f77bcf86cd799439041",
    "user_id": "507f1f77bcf86cd799439011",
    "team_id": "507f1f77bcf86cd799439021",
    "total_points": 1250,
    "rank": 1,
    "last_updated": "2025-01-16T12:00:00Z"
  },
  {
    "id": "507f1f77bcf86cd799439042",
    "user_id": "507f1f77bcf86cd799439012",
    "team_id": "507f1f77bcf86cd799439021",
    "total_points": 1100,
    "rank": 2,
    "last_updated": "2025-01-16T12:00:00Z"
  }
]
```

**Points Calculation:**
Points are calculated based on:
- Activity duration
- Activity type intensity
- Consistency bonuses
- Team collaboration points

---

## Workouts

Get workout suggestions and plans.

### List Workouts

#### GET /api/workouts/

Retrieve available workout suggestions.

**Query Parameters:**
- `difficulty` (optional): Filter by difficulty (beginner, intermediate, advanced)
- `category` (optional): Filter by category (strength, cardio, flexibility)
- `duration` (optional): Maximum duration in minutes

**Response:**
```json
[
  {
    "id": "507f1f77bcf86cd799439051",
    "name": "Morning Cardio Blast",
    "description": "High-intensity cardio workout to start your day",
    "difficulty": "intermediate",
    "category": "cardio",
    "duration": 30,
    "instructions": "1. Warm-up: 5 min jogging\n2. Sprint intervals: 10 min\n3. Jump rope: 5 min\n4. Cool-down: 10 min walk"
  },
  {
    "id": "507f1f77bcf86cd799439052",
    "name": "Beginner Strength Training",
    "description": "Build foundational strength with basic exercises",
    "difficulty": "beginner",
    "category": "strength",
    "duration": 45,
    "instructions": "1. Warm-up: 5 min\n2. Squats: 3x10\n3. Push-ups: 3x8\n4. Planks: 3x30sec\n5. Cool-down: 5 min stretch"
  }
]
```

### Get Workout

#### GET /api/workouts/{id}/

Retrieve a specific workout.

### Create Workout

#### POST /api/workouts/

Create a new workout suggestion.

**Request:**
```bash
curl -X POST https://{CODESPACE_NAME}-8000.app.github.dev/api/workouts/ \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Evening Yoga Flow",
    "description": "Relaxing yoga session for flexibility and stress relief",
    "difficulty": "beginner",
    "category": "flexibility",
    "duration": 20,
    "instructions": "1. Child pose: 2 min\n2. Cat-cow: 3 min\n3. Downward dog: 5 min\n4. Warrior poses: 5 min\n5. Savasana: 5 min"
  }'
```

---

## HTTP Status Codes

| Code | Meaning | Description |
|------|---------|-------------|
| 200 | OK | Request successful |
| 201 | Created | Resource created successfully |
| 204 | No Content | Resource deleted successfully |
| 400 | Bad Request | Invalid request data |
| 404 | Not Found | Resource not found |
| 500 | Internal Server Error | Server error |

## Error Handling

### Validation Errors

```json
{
  "username": ["This field is required."],
  "email": ["Enter a valid email address."]
}
```

### Not Found Error

```json
{
  "detail": "Not found."
}
```

## Rate Limiting

**Current Status**: No rate limiting (development mode)

**Production Recommendation**: Implement rate limiting to prevent abuse (e.g., 100 requests per minute per IP).

## CORS Configuration

**Current Status**: All origins allowed (development mode)

```python
CORS_ALLOW_ALL_ORIGINS = True
```

**Production Recommendation**: Configure specific allowed origins:
```python
CORS_ALLOWED_ORIGINS = [
    "https://octofit-tracker.com",
    "https://www.octofit-tracker.com",
]
```

## Data Validation Rules

### Users
- `username`: Required, unique, 3-30 characters, alphanumeric
- `email`: Required, unique, valid email format
- `first_name`: Optional, max 50 characters
- `last_name`: Optional, max 50 characters
- `profile_info`: Optional, max 500 characters

### Activities
- `user_id`: Required, must be valid user ID
- `activity_type`: Required, must be from allowed list
- `duration`: Required, positive integer (minutes)
- `distance`: Optional, non-negative float (miles/km)
- `calories`: Optional, non-negative integer
- `date`: Required, valid date
- `notes`: Optional, max 500 characters

### Teams
- `name`: Required, unique, 3-50 characters
- `description`: Optional, max 500 characters
- `members`: Optional, array of valid user IDs

### Workouts
- `name`: Required, 3-100 characters
- `description`: Required, max 500 characters
- `difficulty`: Required, one of: beginner, intermediate, advanced
- `category`: Required, one of: strength, cardio, flexibility
- `duration`: Required, positive integer (minutes)
- `instructions`: Required, max 2000 characters

## Testing the API

### Using cURL

```bash
# Test connection
curl https://${CODESPACE_NAME}-8000.app.github.dev/api/

# Get all users
curl https://${CODESPACE_NAME}-8000.app.github.dev/api/users/

# Create a user
curl -X POST https://${CODESPACE_NAME}-8000.app.github.dev/api/users/ \
  -H "Content-Type: application/json" \
  -d '{"username": "test", "email": "test@example.com"}'
```

### Using Python

```python
import requests

base_url = f"https://{CODESPACE_NAME}-8000.app.github.dev/api"

# Get all users
response = requests.get(f"{base_url}/users/")
users = response.json()

# Create a user
new_user = {
    "username": "testuser",
    "email": "test@example.com",
    "first_name": "Test",
    "last_name": "User"
}
response = requests.post(f"{base_url}/users/", json=new_user)
created_user = response.json()
```

### Using JavaScript (fetch)

```javascript
const baseUrl = `https://${process.env.CODESPACE_NAME}-8000.app.github.dev/api`;

// Get all users
fetch(`${baseUrl}/users/`)
  .then(response => response.json())
  .then(users => console.log(users));

// Create a user
fetch(`${baseUrl}/users/`, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    username: 'testuser',
    email: 'test@example.com',
    first_name: 'Test',
    last_name: 'User'
  })
})
  .then(response => response.json())
  .then(user => console.log(user));
```

## Database Schema

For detailed information about the database structure and relationships, see [ARCHITECTURE.md](ARCHITECTURE.md#data-layer-mongodb).

## Future API Enhancements

Planned features for future versions:

1. **Authentication & Authorization**
   - JWT token-based authentication
   - Role-based access control
   - OAuth integration

2. **Advanced Filtering**
   - Date range filtering
   - Multi-field sorting
   - Full-text search

3. **Webhooks**
   - Activity notifications
   - Leaderboard updates
   - Team invitations

4. **WebSocket Support**
   - Real-time leaderboard updates
   - Live activity feeds
   - Team chat

5. **API Versioning**
   - `/api/v1/` and `/api/v2/` endpoints
   - Backward compatibility

---

**Questions or feedback?** Open an issue on GitHub or check the [CONTRIBUTING.md](CONTRIBUTING.md) guide.
