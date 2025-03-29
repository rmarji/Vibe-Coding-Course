# Progressive Project: LearningPathAI

This document outlines the progressive project that will be developed throughout the 10 lessons of the Vibecoding with Roocode course. This project provides a practical, hands-on approach to learning AI-assisted development.

## Project Overview

**LearningPathAI** is an intelligent platform that creates personalized learning paths for users based on their existing knowledge, goals, and preferred learning style. The application will evolve from a simple concept to a fully-functional, deployed application by the end of the course.

## Project Evolution By Lesson

### Lesson 1: Project Setup and Planning

**Objectives:**
- Set up development environment
- Create project repository
- Generate initial project structure

**Deliverables:**
- GitHub repository
- Next.js frontend application skeleton
- FastAPI backend structure
- Initial documentation (README, project goals)

### Lesson 2: Requirements and Specifications

**Objectives:**
- Define comprehensive project requirements
- Create user stories
- Design database schema
- Define API specifications

**Deliverables:**
- Detailed requirements document
- User stories in GitHub issues
- Database schema diagram
- API endpoint specifications

### Lesson 3: Basic Frontend Components

**Objectives:**
- Develop key UI components
- Create project structure
- Set up styling with Tailwind CSS

**Deliverables:**
- Navigation component
- User profile component
- Learning goals input interface
- Basic responsive design

### Lesson 4: LLM Integration with Iterative Approach

**Objectives:**
- Implement OpenAI API integration
- Create Pydantic models for data validation
- Develop learning path generation logic

**Deliverables:**
- Knowledge assessment questionnaire
- LLM integration for path generation
- Topic sequencing algorithms
- Learning path visualization

### Lesson 5: Error Handling and Debugging

**Objectives:**
- Implement robust error handling
- Debug LLM response issues
- Add validation and error responses

**Deliverables:**
- Global error handler for API
- Form validation on frontend
- Error boundary components
- LLM response validation

### Lesson 6: Code Refactoring and Optimization

**Objectives:**
- Refactor components for better performance
- Optimize API calls
- Implement code splitting
- Improve state management

**Deliverables:**
- Optimized component architecture
- Lazy-loaded routes
- Efficient data fetching patterns
- Performance improvements

### Lesson 7: Perplexity Search Integration with Custom Modes

**Objectives:**
- Integrate Perplexity search API
- Develop content recommendation system
- Create resource filtering and ranking
- Extract content metadata

**Deliverables:**
- Search API integration
- Resource recommendation features
- Content relevance ranking
- Metadata extraction service

### Lesson 8: Testing Implementation

**Objectives:**
- Create comprehensive test suite
- Implement CI pipeline
- Ensure code quality
- Write tests for AI-based features

**Deliverables:**
- Unit tests for components
- API endpoint tests
- Integration tests for LLM functionality
- GitHub Actions workflow for CI

### Lesson 9: Deployment and Data Persistence

**Objectives:**
- Implement PostgreSQL database integration
- Set up deployment pipeline
- Configure environment variables
- Implement user progress tracking

**Deliverables:**
- Database integration with SQLAlchemy
- Deployment configuration for production
- Environment setup for different stages
- User progress tracking functionality

### Lesson 10: Capstone and Enhancement

**Objectives:**
- Implement interactive assessments
- Create user dashboard with analytics
- Polish user experience
- Finalize documentation

**Deliverables:**
- Complete application with all features
- Interactive assessment system
- User dashboard with learning analytics
- Comprehensive documentation

## Technical Stack

- **Frontend**: React.js, Next.js, Tailwind CSS
- **Backend**: Python, FastAPI, Pydantic AI
- **Database**: PostgreSQL with SQLAlchemy
- **Authentication**: JWT
- **External APIs**: OpenAI API, Perplexity Search API
- **Testing**: Jest, Pytest, React Testing Library
- **Deployment**: Docker, GitHub Actions
- **Version Control**: Git, GitHub
- **AI Integration**: Roocode for development assistance

## Git Branching Strategy

The repository will maintain branches for each lesson stage:
- `main` - Latest stable version
- `lesson-1` through `lesson-10` - Project state at end of each lesson
- `feature/[feature-name]` - For individual feature development

## Project Repository Structure

```
learningpath-ai/
├── frontend/                 # Next.js frontend application
│   ├── components/           # Reusable UI components
│   │   ├── common/           # Common UI elements
│   │   ├── layout/           # Layout components
│   │   └── learning/         # Learning path specific components
│   ├── contexts/             # React context providers
│   ├── hooks/                # Custom React hooks
│   ├── pages/                # Next.js pages
│   ├── public/               # Static assets
│   ├── styles/               # Global styles
│   └── utils/                # Utility functions
├── backend/                  # FastAPI backend
│   ├── app/                  # Main application package
│   │   ├── api/              # API endpoints
│   │   │   ├── routes/       # API route handlers
│   │   │   └── deps.py       # Dependency injection
│   │   ├── core/             # Core functionality
│   │   │   ├── config.py     # Application configuration
│   │   │   └── security.py   # Authentication and security
│   │   ├── db/               # Database related code
│   │   │   ├── models.py     # SQLAlchemy models
│   │   │   └── session.py    # Database sessions
│   │   ├── models/           # Pydantic models for validation
│   │   ├── services/         # Business logic services
│   │   │   ├── llm.py        # LLM integration service
│   │   │   ├── search.py     # Perplexity search service
│   │   │   └── path.py       # Learning path generation service
│   │   └── utils/            # Utility functions
│   ├── tests/                # Backend tests
│   └── main.py               # Application entry point
├── docs/                     # Documentation
├── tests/                    # End-to-end tests
└── .github/                  # GitHub Actions workflows
```

## Learning Outcomes

Through building this progressive project, students will learn:

1. How to use AI to scaffold a modern application
2. Techniques for integrating LLMs into a production application
3. Best practices for developing with AI assistance
4. Strategies for testing AI-integrated features
5. Deployment and CI/CD implementation for AI applications
6. Effective prompting for different development tasks

At each stage, we'll emphasize how Roocode can help accelerate development while maintaining code quality and developer understanding.