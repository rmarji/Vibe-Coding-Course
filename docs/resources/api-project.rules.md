# API Development Rules

**Version:** 1.0.0  
**Maintainer:** Backend Team  
**Description:** Standard rules for REST API development

## Code Style

- Use snake_case for endpoint URLs
- Use camelCase for function and variable names
- Use PascalCase for class names
- Limit function length to 25 lines
- Follow RESTful resource naming conventions

## API Design

- Use nouns, not verbs in endpoint paths
- Use plural resource names (e.g., /users not /user)
- Use HTTP methods appropriately:
  - GET for retrieval
  - POST for creation
  - PUT for complete updates
  - PATCH for partial updates
  - DELETE for removal
- Include API version in URL path (e.g., /v1/users)
- Return appropriate HTTP status codes

## Security

- Validate all input data
- Implement proper authentication
- Use rate limiting for all endpoints
- Never expose sensitive information in responses
- Apply principle of least privilege
- Implement proper CORS configuration

## Documentation

- Document all endpoints with:
  - URL, method, and description
  - Request parameters and body schema
  - Response format and status codes
  - Authentication requirements
  - Example requests and responses
- Use OpenAPI/Swagger for API documentation

## Frameworks: Express.js

- Organize routes into separate modules
- Use middleware for cross-cutting concerns
- Implement proper error handling middleware
- Use async/await with try/catch blocks
- Implement controller pattern for route handlers