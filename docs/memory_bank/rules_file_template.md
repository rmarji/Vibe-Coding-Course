# Rules File Template

This template provides a structured format for creating rules files that guide Roocode's behavior for specific project types or tasks. Rules files establish consistent system instructions that can be shared across a team and versioned with your codebase.

## Basic Structure

```json
{
  "name": "Project Name Rules",
  "description": "System instructions for Roocode when working on [project type]",
  "version": "1.0.0",
  "maintainer": "Team or individual name",
  "rules": [
    {
      "category": "Code Style",
      "instructions": [
        "Use camelCase for variable names and function names",
        "Use PascalCase for class names and component names",
        "Use UPPER_SNAKE_CASE for constants",
        "Keep line length under 80 characters",
        "Use 2 spaces for indentation"
      ]
    },
    {
      "category": "Architecture",
      "instructions": [
        "Follow the Model-View-Controller pattern",
        "Keep components small and focused on a single responsibility",
        "Use dependency injection for service dependencies",
        "Separate business logic from presentation logic",
        "Store configuration in environment variables, not in code"
      ]
    },
    {
      "category": "Performance",
      "instructions": [
        "Optimize expensive operations",
        "Use memoization for complex calculations",
        "Implement lazy loading for resource-intensive components",
        "Minimize DOM manipulation",
        "Use efficient data structures for large collections"
      ]
    },
    {
      "category": "Security",
      "instructions": [
        "Validate all input data",
        "Sanitize data before displaying it to prevent XSS",
        "Use prepared statements for database queries",
        "Never store sensitive information in client-side code",
        "Implement proper authentication and authorization checks"
      ]
    },
    {
      "category": "Documentation",
      "instructions": [
        "Include JSDoc comments for all public functions and methods",
        "Document complex algorithms with clear explanations",
        "Maintain up-to-date README files",
        "Include usage examples for components and utilities",
        "Document known limitations and edge cases"
      ]
    }
  ],
  "frameworks": {
    "react": {
      "version": "^18.0.0",
      "rules": [
        "Use functional components with hooks instead of class components",
        "Use React.memo for expensive renders",
        "Manage global state with Context API for simple state, Redux for complex state",
        "Keep component state as local as possible",
        "Use proper key props in lists for optimal rendering"
      ]
    },
    "fastapi": {
      "version": "^0.95.0",
      "rules": [
        "Use Pydantic models for request/response validation",
        "Implement proper dependency injection",
        "Use async handlers for I/O-bound operations",
        "Organize routes in logical groups",
        "Include comprehensive OpenAPI documentation"
      ]
    }
  },
  "environments": {
    "development": {
      "rules": [
        "Include detailed error messages",
        "Enable debug logging",
        "Use hot reloading for faster iteration"
      ]
    },
    "production": {
      "rules": [
        "Hide implementation details in error responses",
        "Optimize for performance over development speed",
        "Implement proper error handling and recovery"
      ]
    }
  }
}
```

## How to Use This Template

1. **Create a new file** with a clear name (e.g., `your-project-rules.json` or `team-standards.json`)
2. **Customize the categories** to match your project needs
3. **Add specific instructions** under each category
4. **Define framework-specific rules** for any frameworks you're using
5. **Add environment-specific rules** for different deployment contexts
6. **Save the file** in your project repository
7. **Reference the file** in Roocode settings or in your prompts

## Integration with Roocode

### Loading Rules in Roocode

```
[Switch to Custom Mode]
Please load the rules from ./path/to/your-project-rules.json and apply them to all code generation for this project.
```

### Referencing Rules in Prompts

```
Following the rules specified in our project rules file, please implement a function that [task description].
```

## Best Practices for Rules Files

1. **Start simple**: Begin with a minimal set of critical rules and expand over time
2. **Be specific**: Write clear, actionable instructions
3. **Prioritize**: List more important rules earlier in each category
4. **Version control**: Maintain rules files alongside your code
5. **Review regularly**: Update rules as your project evolves
6. **Seek team consensus**: Ensure the team agrees on standards
7. **Include examples**: Where possible, include examples of correct implementations

## Example Categories

- **Code Style**: Formatting, naming conventions, file organization
- **Architecture**: Design patterns, component structure, file organization
- **Performance**: Optimization strategies, efficient algorithms
- **Security**: Vulnerability prevention, authentication, authorization
- **Documentation**: Comments, README files, usage examples
- **Testing**: Test coverage, test organization, assertion patterns
- **Accessibility**: A11y standards, keyboard navigation, screen reader support
- **Error Handling**: Exception management, user feedback, logging
- **State Management**: Data flow, state organization, side effect handling
- **API Design**: Endpoint naming, response formatting, error codes

## Framework-Specific Rules

Consider adding specialized rules for frameworks you're using:

- **Frontend**: React, Vue, Angular, Svelte
- **Backend**: FastAPI, Express, Django, Spring
- **Mobile**: React Native, Flutter, Swift UI
- **Data Science**: TensorFlow, PyTorch, scikit-learn
- **DevOps**: Docker, Kubernetes, Terraform

## Example: Minimal Rules File

```json
{
  "name": "Simple Web Project Rules",
  "description": "Basic rules for a web application",
  "version": "0.1.0",
  "rules": [
    {
      "category": "General",
      "instructions": [
        "Write clean, readable code with clear comments",
        "Follow the DRY (Don't Repeat Yourself) principle",
        "Implement proper error handling",
        "Write unit tests for critical functionality",
        "Document public APIs and functions"
      ]
    }
  ]
}