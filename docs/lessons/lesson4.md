# Lesson 4: Iterative Development and Workflow

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Implement an incremental development approach using Roocode
- Organize vibecoding tasks as mini "AI sprints"
- Build a web application iteratively using AI assistance
- Manage context and state effectively across multiple prompts
- Structure sequential prompts for complex projects
- Create and maintain TODOs to guide AI-assisted development

## 📚 Lesson Content

### 1. The Importance of Incremental Development

When working with AI, an incremental approach is crucial:

#### Benefits of Incremental Development

- **Manageable complexity**: Easier for AI to understand smaller, focused tasks
- **Error isolation**: Problems are localized to specific changes
- **Progressive validation**: Verify correctness at each step
- **Context management**: Stay within AI context windows
- **Mental model alignment**: Ensure AI understands your goals

#### Traditional vs. AI-Assisted Incremental Development

| Traditional Development | AI-Assisted (Vibecoding) |
|------------------------|--------------------------|
| Break tasks into user stories | Break tasks into clear prompts |
| Implement one feature at a time | Generate one component or function at a time |
| Manual testing after each addition | Test AI-generated code before continuing |
| Code reviews by humans | Human review of AI-generated code |
| Refactor as necessary | Prompt AI to refine and optimize |

### 2. Organizing Tasks as Mini "AI Sprints"

Think of each vibecoding session as a series of small sprints:

#### AI Sprint Structure

1. **Planning**: Define what to implement next
2. **Prompt crafting**: Write clear instructions for the AI
3. **Generation**: Let the AI create the code
4. **Review**: Assess the output for correctness
5. **Refinement**: Improve or fix as needed
6. **Integration**: Ensure it works with existing code
7. **Documentation**: Record what was done (for yourself and the AI)

#### Example: Task Organization

For a simple blog application:

**Sprint 1**: Core data models
- User model with authentication fields
- Blog post model with title, content, timestamps
- Category and tag models

**Sprint 2**: Authentication system
- User registration
- Login/logout functionality
- Password reset capability

**Sprint 3**: Basic blog post CRUD operations
- Create new posts
- Read/display posts
- Update existing posts
- Delete posts

### 3. Hands-on Example: Build a Simple Web App Incrementally

Let's build a web-based task management application using React and Express:

#### Project Overview

A task management application with:
- User authentication
- Task creation and management
- Categories and priorities
- Basic dashboard

#### Sprint 1: Project Setup and Frontend Scaffold

```
Create a new React application with the following structure:
1. Use create-react-app with TypeScript
2. Set up folder structure for components, pages, and services
3. Install necessary dependencies: React Router, Axios, and Material-UI
4. Create a basic App component with routing setup
```

#### Sprint 2: Backend API Structure

```
Create an Express.js backend with the following features:
1. Basic server setup with Express
2. MongoDB connection configuration
3. User model and authentication routes
4. Task model and CRUD routes
5. Basic error handling middleware
```

#### Sprint 3: Frontend Authentication Components

```
Create React components for authentication:
1. Login form with email and password fields
2. Registration form with validation
3. Auth context for managing user state throughout the app
4. Protected route component for secure routes
```

#### Sprint 4: Task Management UI

```
Implement task management components:
1. Task list component that displays all tasks
2. Task item component for individual tasks
3. Task form for creating and editing tasks
4. Task filtering and sorting capabilities
```

#### Sprint 5: Integration and Testing

```
Connect frontend to backend:
1. Create API service functions for all CRUD operations
2. Implement global state management for tasks
3. Add loading and error states
4. Ensure proper authentication flow and token management
```

### 4. Managing Context and State Effectively

AI models have limited context windows, making state management crucial:

#### Context Management Techniques

1. **Progressive disclosure**: Introduce complexity gradually
2. **Relevant code references**: Show only what's necessary
3. **State summarization**: Recap current project state concisely
4. **Focused scope**: Keep each prompt targeted to specific tasks
5. **Project overview maintenance**: Keep a high-level reference

#### Example: Effective Context Management

For our task management app:

**Initial context**:
```
I'm building a task management app with React frontend and Express backend.
Current progress:
- Basic project structure created
- Authentication system implemented
- Starting work on task management features

Current task: Create a component to display and edit task details
```

**Follow-up with specific details**:
```
Continuing from our task management app, here's the current Task model:
```typescript
interface Task {
  id: string;
  title: string;
  description: string;
  dueDate?: Date;
  priority: 'low' | 'medium' | 'high';
  completed: boolean;
  userId: string;
}
```

Please create a TaskDetails component that:
1. Displays all task information
2. Allows editing task fields
3. Handles task completion status toggling
4. Supports task deletion with confirmation
```

### 5. How to Structure Sequential Roocode Prompts

For complex projects, prompts should follow a logical sequence:

#### Prompt Sequencing Patterns

1. **Foundation first**: Start with core structures and models
2. **Dependencies before dependents**: Build prerequisite components first
3. **Outside-in**: Define interfaces before implementations
4. **Simple to complex**: Begin with basic features before advanced ones
5. **Independent before integrated**: Develop standalone components before connecting them

#### Example: Sequential Prompts for Our Web App

**Prompt 1 (Data Models)**:
```
Define TypeScript interfaces for our task management app:
1. User interface with authentication properties
2. Task interface with all necessary fields
3. Category interface for task categorization
```

**Prompt 2 (API Services)**:
```
Using the interfaces we defined earlier, create API service functions:
1. Authentication services (login, register, etc.)
2. Task CRUD operations
3. Category management
Include proper error handling and TypeScript typing.
```

**Prompt 3 (UI Components)**:
```
Based on our data models and services, create React components:
1. TaskList component that uses our TaskService to fetch tasks
2. TaskItem component that displays individual tasks
3. TaskForm component for creating/editing tasks
```

### 6. Benefits of Regular Testing Between Iterations

Testing between AI-assisted development cycles is crucial:

#### Testing Strategies

1. **Incremental verification**: Test each new feature as it's added
2. **Regression checks**: Ensure new changes don't break existing functionality
3. **Prompt-based testing**: Ask the AI to generate tests for its own code
4. **Manual review**: Always inspect AI-generated code before proceeding
5. **Integration testing**: Regularly check how components work together

#### Example: Testing in Our Web App Development

After implementing the authentication components:

```
1. Test user registration with valid credentials
2. Attempt login with the newly created account
3. Test form validation for invalid inputs
4. Verify protected routes redirect unauthenticated users
5. Check token storage and expiration handling
```

### 7. Using a Structured Plan (TODOs) to Guide Roocode

A clear plan helps both you and the AI stay organized:

#### Creating Effective TODOs

1. **Break down the project**: List major components and features
2. **Prioritize tasks**: Determine the logical implementation order
3. **Define dependencies**: Note which tasks depend on others
4. **Update progressively**: Mark completed items and add new ones
5. **Keep it visible**: Reference the TODO list in your prompts

#### Example: TODO List for Our Web App

```
# Task Management App TODOs

## Backend
- [x] Set up Express server with TypeScript
- [x] Configure MongoDB connection
- [x] Implement user model and authentication
- [ ] Create task model and routes
- [ ] Add category functionality
- [ ] Implement search and filtering

## Frontend
- [x] Project initialization with create-react-app
- [x] Set up routing and basic structure
- [x] Create authentication components
- [ ] Develop task list and task detail views
- [ ] Build task creation/editing forms
- [ ] Implement dashboard with statistics
- [ ] Add filtering and search UI

## Integration
- [ ] Connect authentication frontend to backend
- [ ] Implement task data fetching and state management
- [ ] Add error handling and loading states
- [ ] Deploy to testing environment
```

### 8. Exercises: Complete Multiple Small Development Cycles

Practice the iterative development approach:

#### Exercise 1: Weather Dashboard

Build a simple weather dashboard in small increments:
1. Create the basic UI structure
2. Implement weather API service
3. Add current weather display
4. Build forecast component
5. Implement location search
6. Add responsive design elements

#### Exercise 2: Extend Our Task Manager

Enhance the task management app with new features:
1. Add task sharing functionality
2. Implement recurring tasks
3. Create a calendar view
4. Add notifications for due dates
5. Implement data export/import

### 9. Common Mistakes in Iterative Prompting

Avoid these common pitfalls:

#### Common Issues

1. **Excessive scope**: Trying to implement too much in one prompt
2. **Inconsistent terminology**: Using different terms across prompts
3. **Insufficient context**: Not providing enough background
4. **Ignoring failures**: Not addressing issues before moving on
5. **Lack of structure**: Random feature development without a plan
6. **Overreliance on memory**: Expecting the AI to remember all details

#### How to Avoid These Mistakes

1. Keep prompts focused on specific tasks
2. Maintain consistent terminology and naming
3. Provide relevant context in each prompt
4. Fix issues as they arise
5. Follow a structured development plan
6. Remind the AI of important context when needed

### 10. Leveraging Roocode Memory & Context Management Tips

Maximize Roocode's effectiveness with these techniques:

#### Advanced Context Management

1. **File references**: Direct the AI to specific files for context
2. **Code snippets**: Include relevant code sections in your prompts
3. **Project summaries**: Maintain a brief project overview document
4. **Session focus**: Keep related tasks in the same session
5. **Context refreshing**: Periodically remind the AI of key information

#### Example: Memory Management in Roocode

**Creating a context file**:
```
// project-context.md

# Task Manager App Overview

## Architecture
- React frontend with TypeScript
- Express backend with MongoDB
- RESTful API design

## Current Status
- Authentication system complete
- Task CRUD operations implemented
- Working on UI components

## Key Components
- AuthContext: Manages user authentication state
- TaskService: Handles API requests for tasks
- TaskList/TaskItem: UI components for task display

## Next Goals
- Implement filtering and search
- Add category management
- Create dashboard with statistics
```

Then in your prompts:
```
Referring to our project-context.md file, I'd like to implement the category management feature next...
```

## 🎯 Practice Exercises

1. **Mini Project Planning**
   - Choose a small web application idea
   - Break it down into sequential development sprints
   - Identify dependencies between components
   - Create a structured TODO list

2. **Iterative Implementation**
   - Implement the first 3 sprints of your mini project
   - Document each prompt and its result
   - Test after each sprint
   - Refine your approach based on results

3. **Context Management Practice**
   - Create a project context document
   - Use it to guide development across multiple sessions
   - Update it as your project evolves

## 📝 Lesson Summary

Key takeaways:

- Incremental development is essential for effective vibecoding
- Organizing tasks as small "AI sprints" improves results
- Proper context management ensures AI understands your goals
- Sequential prompts should follow logical development patterns
- Regular testing between iterations prevents compounding errors
- A structured TODO list guides development efficiently
- Consistent terminology and context refreshing improve AI performance

## 🚀 Next Steps

1. Complete the practice exercises
2. Apply incremental development to your own projects
3. Experiment with different context management techniques
4. Prepare for Lesson 5: Debugging and Error Handling with AI

## 📚 Additional Resources

- [Agile Development Principles](https://agilemanifesto.org/principles.html)
- [React Official Documentation](https://reactjs.org/docs/getting-started.html)
- [Express.js Guide](https://expressjs.com/en/guide/routing.html)
- [Project Management for Developers](https://www.atlassian.com/software/jira/guides/getting-started/basics) 