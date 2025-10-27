# Quick Start Guide - OctoFit Tracker

This guide will help you get the OctoFit Tracker application up and running quickly.

## Prerequisites Checklist

Before you begin, ensure you have:

- [ ] A GitHub account
- [ ] GitHub Copilot access (Free, Pro, or Enterprise)
- [ ] Basic familiarity with Git and GitHub
- [ ] Web browser (Chrome, Firefox, Edge, or Safari recommended)

## Quick Start (5 Minutes)

### Step 1: Launch Your Codespace

1. Navigate to the [exercise issue](https://github.com/NestorGarciaDLT/skills-build-applications-w-copilot-agent-mode/issues/1)
2. Click the **"Open in GitHub Codespaces"** badge or button
3. Wait 2-3 minutes for your development environment to initialize
4. VS Code will open in your browser automatically

### Step 2: Verify Your Environment

Once your Codespace loads, verify that:

1. **VS Code is open** in your browser
2. **GitHub Copilot extension** is active (look for the Copilot icon in the bottom status bar)
3. **Terminal is accessible** (press `` Ctrl+` `` or `Cmd+` to open if not visible)

### Step 3: Start the Exercise

1. Open the **Copilot Chat** panel (click the Copilot icon in the sidebar)
2. Follow the instructions in the exercise issue
3. Begin with Step 1: Creating and publishing your branch

## Full Setup Instructions

If you want to understand the complete setup process, follow these detailed steps:

### 1. Initial Repository Setup

```bash
# The Codespace automatically clones the repository
# You'll start in: /workspaces/skills-build-applications-w-copilot-agent-mode
```

### 2. Create Application Structure

During the exercise, you'll create:

```
octofit-tracker/
├── backend/                    # Django REST API
│   ├── venv/                  # Python virtual environment
│   ├── requirements.txt       # Python dependencies
│   └── octofit_tracker/       # Django project
└── frontend/                  # React application
    ├── node_modules/          # Node dependencies
    ├── public/                # Static files
    └── src/                   # React source code
```

### 3. Backend Setup (Django + MongoDB)

#### Install Python Dependencies

```bash
# Create virtual environment
python3 -m venv octofit-tracker/backend/venv

# Activate virtual environment
source octofit-tracker/backend/venv/bin/activate

# Install dependencies
pip install -r octofit-tracker/backend/requirements.txt
```

#### Initialize Django Project

```bash
# Create Django project
django-admin startproject octofit_tracker octofit-tracker/backend/

# Run migrations
python octofit-tracker/backend/manage.py migrate
```

#### Start MongoDB

```bash
# MongoDB starts automatically in Codespace
# Verify it's running:
ps aux | grep mongod

# Connect to MongoDB shell:
mongosh
```

### 4. Frontend Setup (React)

#### Install Node Dependencies

```bash
# Create React app
npx create-react-app octofit-tracker/frontend --use-npm

# Navigate to frontend directory
cd octofit-tracker/frontend

# Install additional dependencies
npm install bootstrap react-router-dom
```

#### Configure Environment

The Codespace automatically sets `CODESPACE_NAME` environment variable, which is used to construct URLs.

### 5. Running the Application

#### Option 1: Using VS Code Debugger (Recommended)

1. **For Django Backend**:
   - Press `F5` or click the "Run and Debug" icon in the sidebar
   - Select "Launch Django Backend" from the dropdown
   - Backend will start on port 8000

2. **For React Frontend**:
   - Open another debug session
   - Select "Launch React Frontend"
   - Frontend will start on port 3000

#### Option 2: Using Terminal

**Backend (Terminal 1)**:
```bash
source octofit-tracker/backend/venv/bin/activate
python octofit-tracker/backend/manage.py runserver 0.0.0.0:8000
```

**Frontend (Terminal 2)**:
```bash
cd octofit-tracker/frontend
REACT_APP_CODESPACE_NAME=$CODESPACE_NAME npm start
```

### 6. Access Your Application

Once both servers are running:

1. **Backend API**: 
   - URL: `https://{CODESPACE_NAME}-8000.app.github.dev`
   - You'll get a warning about proceeding - click "Continue"
   - You should see the Django REST Framework browsable API

2. **Frontend**:
   - URL: `https://{CODESPACE_NAME}-3000.app.github.dev`
   - You'll get a similar warning - click "Continue"
   - You should see the OctoFit Tracker React application

## Verifying Your Setup

### Check Backend

```bash
# Test the API endpoints with curl
curl https://${CODESPACE_NAME}-8000.app.github.dev/api/users/
curl https://${CODESPACE_NAME}-8000.app.github.dev/api/activities/
curl https://${CODESPACE_NAME}-8000.app.github.dev/api/teams/
```

Expected response: JSON data or empty arrays `[]`

### Check Frontend

1. Open the React app URL in your browser
2. You should see:
   - Navigation menu with links (Users, Activities, Teams, Leaderboard, Workouts)
   - OctoFit logo
   - Styled Bootstrap interface

### Check Database

```bash
# Connect to MongoDB
mongosh

# Switch to octofit_db
use octofit_db

# List collections
show collections

# Check data in users collection
db.users.find().pretty()

# Exit mongosh
exit
```

## Common Setup Issues

### Issue: MongoDB Not Running

**Symptoms**: Django errors about database connection

**Solution**:
```bash
# Check if MongoDB is running
ps aux | grep mongod

# If not running, start it
sudo systemctl start mongod

# Set it to start automatically
sudo systemctl enable mongod
```

### Issue: Port Already in Use

**Symptoms**: "Address already in use" error

**Solution**:
```bash
# Find process using port 8000 (or 3000)
lsof -i :8000

# Kill the process
kill -9 <PID>

# Or use a different port
python manage.py runserver 0.0.0.0:8001
```

### Issue: Module Not Found

**Symptoms**: Python import errors

**Solution**:
```bash
# Ensure virtual environment is activated
source octofit-tracker/backend/venv/bin/activate

# Reinstall requirements
pip install -r octofit-tracker/backend/requirements.txt
```

### Issue: React App Won't Start

**Symptoms**: npm errors or blank page

**Solution**:
```bash
# Clear cache and reinstall
cd octofit-tracker/frontend
rm -rf node_modules package-lock.json
npm install

# Start the app
npm start
```

### Issue: CORS Errors

**Symptoms**: Frontend can't fetch data from backend

**Solution**: Check that `settings.py` includes:
```python
CORS_ALLOW_ALL_ORIGINS = True  # For development only
ALLOWED_HOSTS = ['*']           # For development only
```

## Development Workflow

### Making Changes

1. **Backend Changes**:
   - Edit files in `octofit-tracker/backend/octofit_tracker/`
   - Django auto-reloads when you save files
   - Check the terminal for any errors

2. **Frontend Changes**:
   - Edit files in `octofit-tracker/frontend/src/`
   - React auto-reloads in the browser
   - Check browser console for errors

3. **Database Changes**:
   - Update models in `models.py`
   - Run `python manage.py makemigrations`
   - Run `python manage.py migrate`

### Using GitHub Copilot Agent Mode

Throughout the exercise, you'll use Copilot Agent Mode:

1. Open Copilot Chat panel
2. Switch to **Agent** mode (not Ask or Edit)
3. Use the provided prompts or create your own
4. Review suggested commands before executing
5. Click "Continue" to let Copilot run commands

**Example prompt**:
```
Let's create the Django models for the OctoFit Tracker.
- Create User, Team, Activity, Leaderboard, and Workout models
- Use MongoDB-compatible field types
- Add appropriate relationships
```

### Testing Your Changes

```bash
# Test Django backend
python octofit-tracker/backend/manage.py test

# Test API endpoints
curl -X GET https://${CODESPACE_NAME}-8000.app.github.dev/api/users/
curl -X POST https://${CODESPACE_NAME}-8000.app.github.dev/api/users/ \
  -H "Content-Type: application/json" \
  -d '{"username": "testuser", "email": "test@example.com"}'

# React doesn't have tests by default in this exercise
# but you can add them using Jest
```

## Next Steps

Once your environment is set up and running:

1. **Complete the Exercise Steps**: Work through each step in `.github/steps/`
2. **Experiment**: Try adding new features beyond the requirements
3. **Learn Prompting**: Practice writing effective prompts for Copilot
4. **Share**: Show your completed project to others

## Getting Help

If you're stuck:

1. **Check the Documentation**:
   - [ARCHITECTURE.md](ARCHITECTURE.md) - Understanding the app structure
   - [CONTRIBUTING.md](CONTRIBUTING.md) - Community guidelines
   - Step files in `.github/steps/` - Detailed instructions

2. **Use Copilot**:
   - Ask Copilot for help in Chat mode
   - Example: "Why is my Django API returning a 500 error?"

3. **Search Issues**:
   - Check existing GitHub Issues for similar problems
   - Search GitHub Discussions

4. **Create an Issue**:
   - If you find a bug, report it
   - Include error messages and steps to reproduce

## Environment Variables Reference

| Variable | Set By | Used By | Purpose |
|----------|--------|---------|---------|
| `CODESPACE_NAME` | GitHub | Django, React | Construct URLs for Codespace environment |
| `REACT_APP_CODESPACE_NAME` | launch.json | React | API URL configuration |
| `VIRTUAL_ENV` | venv | Python | Virtual environment path |
| `PATH` | venv | Shell | Include venv binaries |

## Useful Commands Reference

```bash
# Python/Django
source octofit-tracker/backend/venv/bin/activate  # Activate venv
python manage.py runserver 0.0.0.0:8000          # Start Django
python manage.py makemigrations                   # Create migrations
python manage.py migrate                          # Apply migrations
python manage.py createsuperuser                  # Create admin user
python manage.py shell                            # Django shell

# Node/React
npm start                                         # Start React dev server
npm install <package>                             # Install package
npm run build                                     # Build for production

# MongoDB
mongosh                                           # MongoDB shell
sudo systemctl status mongod                      # Check MongoDB status
sudo systemctl start mongod                       # Start MongoDB

# Git
git status                                        # Check status
git add .                                         # Stage all changes
git commit -m "message"                           # Commit changes
git push                                          # Push to GitHub
```

---

**Ready to build?** Head back to the [main README](README.md) and start the exercise! 🚀
