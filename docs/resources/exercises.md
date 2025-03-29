# Exercises

This page provides practice exercises to reinforce your learning throughout the Vibecoding with Roocode course. These exercises are designed to help you apply the concepts you've learned to build the LearningPathAI application as well as develop general AI-assisted development skills.

## Beginner Level Exercises

These exercises are ideal for those just starting with Vibecoding and focus on basic skills and concepts.

### Lesson 1: Introduction to Vibe Coding and Roocode Setup

1. **Environment Setup Verification**
   - Install Roocode extension in VS Code
   - Configure API access
   - Create a new project using Roocode's initial scaffolding
   - Verify your setup by generating a simple "Hello World" component

2. **Project Structure Generation**
   - Use Roocode to generate a basic file structure for a Next.js project
   - Ask Roocode to create the initial directory structure for the LearningPathAI frontend
   - Compare and analyze the AI-generated structure with best practices

3. **README Creation**
   - Use Roocode to help create a comprehensive README.md file for the LearningPathAI project
   - Include sections for project overview, features, tech stack, and setup
   - Refine the AI-generated README to accurately represent the project vision

4. **Basic Component Creation**
   - Use Roocode to generate a simple React component for a user profile card
   - Modify the generated component to match the LearningPathAI application's needs
   - Add styling to the component using Tailwind CSS

### Lesson 2: Effective Prompting and Specification Writing

1. **Requirements Document Creation**
   - Create a comprehensive requirements document for the LearningPathAI application
   - Include functional and non-functional requirements
   - Use Roocode to refine and expand your initial requirements draft

2. **API Endpoint Specification**
   - Design specifications for 3-5 core API endpoints for the LearningPathAI backend
   - Include endpoint paths, methods, request/response formats, and error handling
   - Use Roocode to validate and enhance your API design

3. **Data Model Design**
   - Define the core data models for users, learning paths, and content resources
   - Create a diagram showing the relationships between these entities
   - Use Roocode to generate Pydantic models based on your design

4. **User Story Development**
   - Write 5-7 user stories for the LearningPathAI application
   - Create acceptance criteria for each story
   - Use Roocode to help refine the stories and ensure they're comprehensive

### Lesson 3: Basic Code Generation and Editing

1. **React Component Generation**
   - Generate a learning goals input form component
   - Create a learning path display component
   - Generate a navigation bar component
   - Edit the generated components to fit the application's specific needs

2. **FastAPI Route Creation**
   - Generate basic FastAPI route handlers for user operations
   - Create routes for learning path management
   - Implement proper validation and response handling
   - Edit the generated code to ensure proper error handling

3. **Frontend-Backend Integration**
   - Create a frontend service to communicate with your backend API
   - Implement proper error handling and loading states
   - Use Roocode to generate efficient data fetching mechanisms

4. **Component Refactoring Practice**
   - Take a complex, monolithic component and use Roocode to help break it down
   - Refactor the component into smaller, more manageable pieces
   - Ensure the refactored components maintain the original functionality

## Intermediate Level Exercises

These exercises build upon the basics and focus on more complex development tasks with AI assistance.

### Lesson 4: Iterative Development and Workflow

1. **LLM Integration Implementation**
   - Create a service to interact with the OpenAI API
   - Implement prompt templates for learning path generation
   - Develop a knowledge assessment algorithm
   - Iteratively refine the implementation through multiple prompting cycles

2. **Pydantic Model Development**
   - Create Pydantic models for validating LLM inputs and outputs
   - Implement custom validators for complex data structures
   - Develop a schema for learning path representation
   - Use Roocode to optimize your models

3. **User Knowledge Modeling**
   - Design and implement a system to model user knowledge levels
   - Create algorithms for determining knowledge gaps
   - Implement prerequisite tracking for learning topics
   - Use Roocode to enhance your implementation

4. **Learning Path Visualization**
   - Develop a component to visualize a learning path as a graph/tree
   - Implement interactive features to explore the path
   - Use Roocode to generate complex visualization code
   - Iteratively improve the visualization with AI assistance

### Lesson 5: Debugging and Error Handling with AI

1. **LLM Response Validation**
   - Implement comprehensive validation for LLM responses
   - Create fallback mechanisms for API failures
   - Develop strategies for handling malformed responses
   - Use Roocode to identify potential edge cases

2. **Error Boundary Implementation**
   - Create React error boundaries for different sections of the application
   - Implement user-friendly error displays
   - Develop recovery mechanisms from common errors
   - Test the error boundaries with various failure scenarios

3. **Input Validation Enhancement**
   - Implement comprehensive validation for all user inputs
   - Create helpful error messages for validation failures
   - Use Roocode to generate validation logic
   - Test your validation with edge cases

4. **API Error Handling**
   - Implement global error handling for your FastAPI backend
   - Create consistent error response formats
   - Develop proper logging for API errors
   - Use Roocode to enhance your error handling approach

### Lesson 6: Refactoring and Optimization

1. **Frontend Performance Optimization**
   - Identify performance bottlenecks in React components
   - Implement code splitting and lazy loading
   - Optimize rendering performance
   - Use Roocode to suggest and implement optimizations

2. **API Endpoint Optimization**
   - Refactor API endpoints for better performance
   - Implement caching strategies
   - Optimize database queries
   - Use Roocode to analyze and improve your code

3. **State Management Refactoring**
   - Refactor state management for complex components
   - Implement context providers for shared state
   - Create custom hooks for state logic
   - Use Roocode to guide your refactoring process

4. **Code Quality Improvement**
   - Identify and fix code smells in your application
   - Implement consistent patterns across components
   - Create reusable utility functions
   - Use Roocode to analyze and improve code quality

## Advanced Level Exercises

These exercises challenge experienced developers to leverage AI for complex tasks and project integration.

### Lesson 7: Advanced Roocode Features

1. **Perplexity Search Integration**
   - Implement a service to interact with the Perplexity Search API
   - Create search functionality for finding learning resources
   - Develop content relevance ranking algorithms
   - Use specialized Roocode modes to implement complex search features

2. **Content Recommendation System**
   - Design and implement a recommendation algorithm for learning resources
   - Create personalized resource suggestions based on user progress
   - Implement content filtering mechanisms
   - Use Roocode to develop complex recommendation logic

3. **Metadata Extraction Service**
   - Create a service to extract metadata from learning resources
   - Implement classification of content by difficulty and relevance
   - Develop automatic tagging of resources
   - Use Roocode to generate parsing and classification code

4. **Custom Mode Development**
   - Create custom Roocode modes for different aspects of your project
   - Develop specialized prompts for educational content generation
   - Implement domain-specific guidance for the LLM
   - Test and refine your custom modes

### Lesson 8: Testing and Quality Assurance

1. **Test Suite Implementation**
   - Create comprehensive unit tests for React components
   - Implement API endpoint tests for FastAPI routes
   - Develop integration tests for LLM functionality
   - Use Roocode to generate test cases

2. **Test-Driven Development Practice**
   - Implement a new feature using TDD approach
   - Write tests first, then use Roocode to generate implementation
   - Iterate on the implementation until tests pass
   - Document your TDD process

3. **LLM Integration Testing**
   - Develop testing strategies for LLM-based features
   - Create mocks for API responses
   - Implement validation tests for learning path algorithms
   - Use Roocode to generate complex test scenarios

4. **Continuous Integration Setup**
   - Configure GitHub Actions for your project
   - Set up automated testing on pull requests
   - Implement code quality checks
   - Use Roocode to generate CI configuration

### Lesson 9: Project Deployment and Automation

1. **Database Integration**
   - Implement PostgreSQL integration with SQLAlchemy
   - Create database migration scripts
   - Develop data access patterns
   - Use Roocode to generate efficient database models

2. **Authentication Implementation**
   - Create a JWT-based authentication system
   - Implement user registration and login
   - Develop role-based access control
   - Use Roocode to generate secure authentication code

3. **Deployment Configuration**
   - Create Docker configurations for frontend and backend
   - Implement environment-specific settings
   - Develop deployment scripts
   - Use Roocode to generate deployment configurations

4. **Monitoring and Logging Setup**
   - Implement application monitoring
   - Create comprehensive logging
   - Develop error tracking mechanisms
   - Use Roocode to enhance your monitoring approach

### Lesson 10: Capstone Project & Best Practices

1. **Interactive Assessment Development**
   - Create an interactive assessment system
   - Implement various question types
   - Develop scoring and feedback mechanisms
   - Use Roocode to generate assessment functionality

2. **User Dashboard Implementation**
   - Create a comprehensive user dashboard
   - Implement progress tracking visualizations
   - Develop personalized recommendations display
   - Use Roocode to generate complex dashboard components

3. **Mobile Responsive Design**
   - Ensure responsive design across all components
   - Implement mobile-specific UI enhancements
   - Create adaptive layouts
   - Use Roocode to generate responsive styling

4. **Documentation Generation**
   - Create comprehensive user documentation
   - Implement API documentation
   - Develop developer guides
   - Use Roocode to generate and enhance documentation

## Challenge Exercises

These additional challenges provide opportunities to extend the LearningPathAI application with advanced features.

1. **Multi-Language Support**
   - Implement internationalization (i18n) support
   - Create translations for multiple languages
   - Develop language-specific content recommendations
   - Use Roocode to assist with translation management

2. **Collaborative Learning Paths**
   - Implement shared learning paths between users
   - Create collaborative editing features
   - Develop permission management
   - Use Roocode to generate complex collaboration features

3. **Learning Analytics Dashboard**
   - Create an advanced analytics dashboard
   - Implement data visualization components
   - Develop predictive learning algorithms
   - Use Roocode to generate complex analytics features

4. **Content Creation Platform**
   - Add features for users to create learning content
   - Implement a content review system
   - Develop content versioning
   - Use Roocode to generate content management features