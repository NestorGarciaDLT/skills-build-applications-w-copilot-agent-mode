# Build Applications with GitHub Copilot Agent Mode

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

A hands-on GitHub Skills exercise that teaches you how to build full-stack web applications using **GitHub Copilot Agent Mode**. Learn to create the OctoFit Tracker - a fitness tracking application for students at Mergington High School.

[![](https://img.shields.io/badge/Go%20to%20Exercise-%E2%86%92-1f883d?style=for-the-badge&logo=github&labelColor=197935)](https://github.com/NestorGarciaDLT/skills-build-applications-w-copilot-agent-mode/issues/1)

## 📚 Table of Contents

- [About This Exercise](#about-this-exercise)
- [What You'll Learn](#what-youll-learn)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Application Features](#application-features)
- [Learning Path](#learning-path)
- [Additional Resources](#additional-resources)
- [Contributing](#contributing)
- [License](#license)

## 🎯 About This Exercise

This is a **self-paced, interactive GitHub Skills exercise** designed to teach you how to leverage GitHub Copilot Agent Mode to build modern web applications. Through this exercise, you'll build the **OctoFit Tracker** - a fitness application that helps students track their physical activities, compete in teams, and stay motivated.

The story behind OctoFit Tracker: Paul Octo, a PE teacher at Mergington High School, wanted to encourage students to stay active outside of class. Working with the IT department, he's using GitHub Copilot Agent Mode to build an app that makes fitness tracking fun through gamification and friendly competition.

## 🚀 What You'll Learn

- **GitHub Copilot Agent Mode**: How to use Copilot's autonomous development capabilities to build applications
- **Prompt Engineering**: Writing effective prompts to guide Copilot Agent Mode
- **Custom Instructions**: Creating reusable prompt files for common development tasks
- **Full-Stack Development**: Building a complete application with frontend, backend, and database
- **Modern Web Technologies**: Working with React, Django REST Framework, and MongoDB
- **Development Workflow**: Using GitHub Codespaces for cloud-based development

## 🛠 Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Frontend** | React.js | Modern, component-based UI framework |
| **Backend** | Django REST Framework | Python-based API server |
| **Database** | MongoDB | NoSQL document database |
| **Dev Environment** | GitHub Codespaces | Cloud-based IDE with VS Code |
| **AI Assistant** | GitHub Copilot | AI-powered code completion and agent mode |

## ✅ Prerequisites

- A GitHub account with access to GitHub Copilot
- Basic understanding of:
  - Web development concepts
  - Git version control
  - Command line basics
- No prior experience with React, Django, or MongoDB required!

## 🏁 Getting Started

### Step 1: Start the Exercise

Click the badge above or visit [the exercise issue](https://github.com/NestorGarciaDLT/skills-build-applications-w-copilot-agent-mode/issues/1) to begin.

### Step 2: Launch GitHub Codespace

1. Click the "Create Codespace" button in the exercise
2. Wait for your development environment to initialize
3. VS Code will open in your browser with all tools pre-configured

### Step 3: Follow the Learning Path

Complete the six steps outlined in the [Learning Path](#learning-path) section below. Each step builds on the previous one, guiding you through the complete application development process.

## 📂 Project Structure

```
skills-build-applications-w-copilot-agent-mode/
├── .devcontainer/           # Codespace configuration
│   ├── devcontainer.json   # Container and extension settings
│   ├── post_create.sh      # Setup script
│   └── post_start.sh       # Startup script
├── .github/
│   ├── instructions/       # Custom instructions for Copilot
│   │   ├── octofit_tracker_setup_project.instructions.md
│   │   ├── octofit_tracker_django_backend.instructions.md
│   │   └── octofit_tracker_react_frontend.instructions.md
│   ├── prompts/           # Reusable prompt files
│   │   ├── create-django-project.prompt.md
│   │   └── init-populate-octofit_db.prompt.md
│   ├── steps/             # Step-by-step exercise instructions
│   │   ├── 1-preparing.md
│   │   ├── 2-application-initial-setup.md
│   │   ├── 3-django-project-setup.md
│   │   ├── 4-setup-django-rest-framework.md
│   │   ├── 5-setup-frontend-react-framework.md
│   │   └── 6-copilot-on-github.md
│   └── workflows/         # GitHub Actions (if any)
├── .vscode/
│   └── launch.json        # Debug configurations for Django and React
├── docs/
│   ├── octofit_story.md   # Background story and context
│   └── octofitapp-small.png # App logo
├── octofit-tracker/       # Application code (created during exercise)
│   ├── backend/           # Django REST API
│   └── frontend/          # React application
├── .gitignore
├── LICENSE
└── README.md
```

## 🎮 Application Features

The **OctoFit Tracker** includes:

- **User Profiles**: Student registration and authentication
- **Activity Logging**: Track various types of physical activities
- **Team Management**: Create and join fitness teams
- **Leaderboard**: Competitive rankings to motivate students
- **Workout Suggestions**: Personalized exercise recommendations
- **Dashboard**: Visual progress tracking and statistics

## 🗺 Learning Path

### Step 1: Preparing (Hello GitHub Copilot Agent Mode)
- Introduction to Copilot Agent Mode
- Setting up your Codespace
- Creating and publishing your first branch with Copilot

### Step 2: Application Initial Setup
- Creating the project directory structure
- Setting up Python virtual environment
- Creating and installing dependencies from requirements.txt

### Step 3: Django Project Setup
- Initializing the Django project
- Setting up MongoDB database
- Creating Django models, serializers, and views
- Populating the database with test data

### Step 4: Django REST Framework Setup
- Configuring REST API endpoints
- Testing API with curl
- Starting the Django development server
- Verifying API functionality

### Step 5: React Frontend Setup
- Creating the React application
- Building UI components for each feature
- Connecting frontend to backend API
- Styling with Bootstrap

### Step 6: Using Copilot on GitHub
- Creating pull requests with Copilot-generated summaries
- Requesting Copilot code reviews
- Merging your completed work

## 📖 Additional Resources

### GitHub Copilot Documentation
- [Getting Started with GitHub Copilot Chat](https://docs.github.com/en/copilot/how-tos/use-chat/get-started-with-chat?tool=vscode)
- [Using Copilot Agent Mode](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)
- [Prompt Engineering for GitHub Copilot](https://docs.github.com/en/copilot/concepts/prompt-engineering)
- [Custom Instructions and Prompt Files](https://code.visualstudio.com/docs/copilot/customization/overview)

### Technology Documentation
- [React Documentation](https://react.dev/)
- [Django REST Framework](https://www.django-rest-framework.org/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [GitHub Codespaces](https://docs.github.com/en/codespaces)

### Helpful Blog Posts
- [How to Write Better Prompts for GitHub Copilot](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/)
- [Using GitHub Copilot in Your IDE: Tips, Tricks, and Best Practices](https://github.blog/2024-03-25-how-to-use-github-copilot-in-your-ide-tips-tricks-and-best-practices/)

## 🤝 Contributing

This is an educational exercise repository. While we don't accept contributions to the exercise itself, you're encouraged to:

- Share your completed OctoFit Tracker implementations
- Provide feedback on the learning experience
- Report issues or suggest improvements via GitHub Issues

## 📋 License

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

---

**Ready to get started?** Click the exercise badge at the top to begin your journey with GitHub Copilot Agent Mode! 🚀

