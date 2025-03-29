# Cheatsheets

This page provides quick reference guides and cheatsheets for various aspects of the Vibecoding with Roocode course.

## Prompt Engineering Cheatsheet

### General Prompting Principles

1. **Be Specific and Clear**
   - Specify programming language, libraries, and frameworks
   - Include desired functionality and design patterns
   - Mention important constraints or requirements

2. **Provide Context**
   - Explain the purpose of the code you're requesting
   - Mention where it fits in your project
   - Include relevant background information

3. **Use Structured Format**
   - Number your requirements
   - Group related items
   - Use clear section headers

4. **Include Examples**
   - Show sample inputs and expected outputs
   - Reference existing code patterns you want to follow
   - Provide examples of edge cases to handle

5. **Iterate and Refine**
   - Start with a general prompt and refine based on results
   - Ask for specific improvements to generated code
   - Break complex tasks into smaller, sequential prompts

### LearningPathAI Project-Specific Prompts

#### React/Next.js Frontend Components

##### User Profile Component
```
Create a React component for a user profile in our LearningPathAI application with the following features:

1. Display user's name, profile picture, and bio
2. Show completed courses count and current learning paths
3. Include a progress visualization showing completion percentage
4. Use Tailwind CSS for styling with our indigo/purple color scheme
5. Implement responsive design for mobile and desktop
6. Handle loading and error states properly
7. Use TypeScript for type safety

The component should receive a user object with the following structure:
{
  id: string;
  name: string;
  profilePicture: string;
  bio: string;
  completedCoursesCount: number;
  learningPaths: Array<{id: string, title: string, progress: number}>;
}
```

##### Learning Path Card Component
```
Generate a React component for displaying a learning path card with the following requirements:

1. Show the learning path title, description, and estimated completion time
2. Display the current progress as a percentage with a progress bar
3. Show topic count and resource count
4. Include a "Continue Learning" button that links to the learning path detail page
5. Style with Tailwind CSS using a card layout with subtle shadows
6. Make the entire card clickable with appropriate hover effects
7. Support both light and dark mode

The component should accept a prop of type LearningPath with this structure:
{
  id: string;
  title: string;
  description: string;
  estimatedHours: number;
  progress: number;
  topicCount: number;
  resourceCount: number;
}
```

#### FastAPI Backend Routes

##### Learning Path Generation Endpoint
```
Create a FastAPI endpoint for generating personalized learning paths with the following specifications:

1. HTTP POST route at /api/learning-paths/generate
2. Accept a JSON request body with:
   - goal (string): The learning goal
   - currentLevel (string): User's current knowledge level
   - targetLevel (string): User's target knowledge level
   - preferences (object): Learning style preferences
3. Use Pydantic models for request and response validation
4. Call the LLM service to generate the learning path
5. Store the generated path in the database
6. Return the created learning path with a 201 status code
7. Include proper error handling for:
   - Invalid request data
   - LLM service failures
   - Database errors
8. Add appropriate type hints and docstrings
9. Implement dependency injection for services

Make sure to follow RESTful API design principles and include appropriate status codes.
```

##### Resource Search Endpoint
```
Create a FastAPI endpoint that searches for learning resources using the Perplexity API:

1. HTTP GET route at /api/resources/search
2. Accept query parameters:
   - query (string, required): The search term
   - type (string, optional): Resource type filter (video, article, course, etc.)
   - difficulty (string, optional): Difficulty level filter
   - limit (int, optional, default=10): Maximum number of results
3. Create Pydantic models for the response
4. Implement the search service integration with Perplexity API
5. Add caching to prevent duplicate API calls
6. Return results sorted by relevance
7. Include pagination support
8. Add proper error handling and logging
9. Document the endpoint with OpenAPI annotations

Ensure the endpoint is performant and handles API rate limits appropriately.
```

#### LLM Integration

##### Learning Path Generation Prompt
```
Implement a function that generates a prompt for the OpenAI API to create a learning path with these requirements:

1. The function should take parameters for:
   - learning goal
   - current knowledge level
   - target knowledge level
   - time constraints (if any)
   - preferred learning style
2. Structure the prompt to request a learning path with:
   - A title and description
   - 5-8 main topics organized in logical progression
   - Each topic should have:
     - A description
     - Estimated time commitment
     - 3-5 learning resources (with titles, URLs, and types)
     - Subtopics if appropriate
3. Specify that the response must be in a valid JSON format
4. Include system instructions to act as an educational expert
5. Request the model to consider prerequisites between topics
6. Have the model explain its reasoning in a separate field

Make sure the function properly escapes any special characters and stays within token limits.
```

##### Perplexity Search Integration
```
Create a service that integrates with the Perplexity API to search for learning resources:

1. Implement an asynchronous search function that:
   - Takes a search query string and optional filters
   - Constructs an appropriate API request to Perplexity
   - Processes and validates the response
   - Transforms results into a consistent format
2. Add functionality to:
   - Filter results by content type
   - Rank resources by relevance
   - Extract metadata from search results
   - Handle API errors and rate limiting
3. Implement caching to improve performance
4. Add detailed logging for debugging
5. Include type hints and comprehensive documentation

The service should be reusable across different parts of the application.
```

#### Database Models

##### SQLAlchemy Models Setup
```
Create SQLAlchemy models for the LearningPathAI application with the following requirements:

1. Define the following models:
   - User: For user account information
   - LearningPath: For storing generated learning paths
   - Topic: For individual topics within a learning path
   - Resource: For learning resources (articles, videos, etc.)
   - UserProgress: For tracking user progress through a learning path

2. For each model, include:
   - Primary key fields
   - Appropriate relationships (many-to-one, many-to-many, etc.)
   - Created and updated timestamps
   - Relevant metadata fields

3. Implement:
   - Foreign key constraints
   - Indexes for frequently queried fields
   - Cascading deletes where appropriate
   - Proper table naming conventions

4. Add SQLAlchemy type annotations and documentation comments.

Include a database initialization function and schema upgrade mechanism.
```

#### Testing Code

##### React Component Tests
```
Create Jest tests for the LearningPathCard React component with the following requirements:

1. Test basic rendering with all props provided
2. Test component behavior with minimum required props
3. Test the progress bar visualization with different progress values
4. Test the click handler for the "Continue Learning" button
5. Test responsive behavior for different screen sizes
6. Test accessibility features
7. Test proper rendering in both light and dark modes

Use React Testing Library for rendering and assertions. Mock any necessary dependencies.
```

##### API Endpoint Tests
```
Write Pytest tests for the learning path generation endpoint with these requirements:

1. Test successful learning path creation with valid input
2. Test validation errors for:
   - Missing required fields
   - Invalid data types
   - Out-of-range values
3. Test authentication and authorization behavior
4. Test error handling for:
   - LLM service failures
   - Database connection issues
5. Create appropriate mocks for:
   - The LLM service
   - Database operations
   - User authentication
6. Include both unit tests and integration tests
7. Test performance and timeout handling

Use pytest fixtures for test setup and dependency injection.
```

## Vibecoding Workflow Cheatsheet

### Project Initialization Workflow

1. **Create Project Structure**
   - Ask AI to suggest directory structure
   - Generate initial configuration files
   - Set up build system and dependencies

2. **Define Core Requirements**
   - Generate user stories with AI assistance
   - Create technical specifications
   - Design database schema

3. **Set Up Development Environment**
   - Configure tooling and linters
   - Establish testing framework
   - Set up version control

### Feature Development Workflow

1. **Feature Planning**
   - Define feature requirements
   - Create acceptance criteria
   - Design component structure

2. **Implementation**
   - Generate component boilerplate
   - Implement core functionality
   - Connect to services and APIs

3. **Refinement**
   - Add error handling
   - Optimize performance
   - Improve code quality

4. **Testing**
   - Create unit tests
   - Implement integration tests
   - Test edge cases

### Debugging Workflow

1. **Identify Issue**
   - Gather error information
   - Reproduce the problem
   - Isolate affected components

2. **Analyze with AI**
   - Share error details with Roocode
   - Request potential causes
   - Get suggestions for fixes

3. **Implement and Verify Fix**
   - Apply recommended solutions
   - Test to confirm resolution
   - Document the fix

## Technology Stack Reference

### Frontend (Next.js/React)

#### Component Structure
```
components/
├── common/          # Reusable UI elements
├── layout/          # Layout components
└── learning/        # Learning path specific components
```

#### Key Libraries
- React 18.x
- Next.js 14.x
- Tailwind CSS
- React Query
- Zustand (state management)

### Backend (FastAPI)

#### Project Structure
```
backend/
├── app/
│   ├── api/         # API routes
│   ├── core/        # Core application code
│   ├── db/          # Database models and session management
│   ├── models/      # Pydantic models
│   ├── services/    # Business logic services
│   └── utils/       # Utility functions
├── tests/           # Test directory
└── main.py          # Application entry point
```

#### Key Libraries
- FastAPI
- Pydantic
- SQLAlchemy
- OpenAI SDK
- Perplexity API Client

### Database (PostgreSQL)

#### Core Tables
- users
- learning_paths
- topics
- resources
- user_progress

#### ORM Setup
```python
# Example SQLAlchemy model
class LearningPath(Base):
    __tablename__ = "learning_paths"
    
    id = Column(UUID, primary_key=True, default=uuid.uuid4)
    user_id = Column(UUID, ForeignKey("users.id"))
    title = Column(String, nullable=False)
    description = Column(Text)
    created_at = Column(DateTime, default=func.now())
    updated_at = Column(DateTime, onupdate=func.now())
    
    # Relationships
    user = relationship("User", back_populates="learning_paths")
    topics = relationship("Topic", back_populates="learning_path")
```

## Common Error Solutions

### React/Next.js Issues

| Error | Potential Solution |
|-------|-------------------|
| "Cannot find module..." | Check import paths, ensure package is installed |
| "React Hook useEffect has a missing dependency..." | Add the missing dependency to the dependency array |
| "Cannot update a component while rendering a different component" | Move state updates to event handlers or useEffect |
| "Maximum update depth exceeded" | Check for infinite render loops in useEffect or state updates |

### FastAPI Issues

| Error | Potential Solution |
|-------|-------------------|
| Pydantic validation error | Check request payload against the expected model schema |
| CORS error | Verify CORS settings in the FastAPI app configuration |
| 422 Unprocessable Entity | Check that request body matches expected types |
| Database connection error | Verify connection string and database availability |

### LLM Integration Issues

| Error | Potential Solution |
|-------|-------------------|
| API key errors | Verify API key is correctly set in environment variables |
| Rate limit exceeded | Implement retry logic with exponential backoff |
| Response parsing errors | Use more robust JSON parsing with error handling |
| Context length exceeded | Reduce input prompt size or use chunking strategies |