# Lesson 7: Advanced Roocode Features (Custom Modes & Roles)

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Understand and use Roocode's advanced custom modes
- Create specialized AI personas for different development tasks
- Apply custom modes for security audits and code reviews
- Customize Roocode's behavior for specific project requirements
- Develop effective mode switching strategies
- Combine multiple modes for complex workflows

## 📚 Lesson Content

### 1. Introduction to Advanced Roocode Modes

Roocode offers powerful customization through specialized modes:

#### What Are Custom Modes?

Custom modes allow you to customize Roocode's behavior by providing specific instructions or "personalities" for the AI. Each mode shapes how the AI:

- Interprets your prompts
- Generates code
- Formats outputs
- Approaches specific tasks
- Applies domain-specific knowledge

#### Benefits of Using Custom Modes

1. **Task specialization**: Optimize the AI for specific coding tasks
2. **Consistent output**: Enforce particular coding styles or patterns
3. **Domain expertise**: Add specialized knowledge for specific frameworks
4. **Workflow integration**: Adapt the AI to your development process
5. **Team standardization**: Create modes aligned with team practices

### 2. Creating and Customizing Roocode Modes

Learn how to define custom modes for your specific needs:

#### How to Access Mode Settings

1. Open VS Code with Roocode extension installed
2. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
3. Type "Roocode: Manage Custom Modes"
4. Select "Create New Mode" or "Edit Existing Mode"

#### Custom Mode Components

A complete custom mode consists of:

1. **Name**: Identifier for the mode
2. **Description**: Purpose and usage information
3. **System Instructions**: Primary behavior guidance for the AI
4. **Example Interactions**: Sample prompts and responses (optional)
5. **Knowledge Base**: Specific information for the AI to reference (optional)

#### Example: Creating a React Developer Mode

```
Name: React Developer
Description: Specialized mode for React.js development following best practices

System Instructions:
You are a senior React developer with expertise in modern React patterns and best practices. When helping with code:

1. Always use functional components with hooks, not class components
2. Follow the official React style guide
3. Prioritize component composition over inheritance
4. Implement proper state management (Context API for simpler apps, Redux for complex ones)
5. Consider performance optimizations (memoization, lazy loading)
6. Write clean, self-documenting JSX with proper separation of concerns
7. Include PropTypes or TypeScript type definitions
8. Add helpful comments for complex logic
9. Handle errors gracefully
10. Implement accessibility best practices

Before implementing any feature, consider:
- Component reusability
- State management approach
- Side effect handling
- Performance implications
```

### 3. Demo: Security Auditor or QA Tester Custom Mode

Let's create and use specialized security and QA modes:

#### Creating a Security Auditor Mode

```
Name: Security Auditor
Description: Finds and fixes security vulnerabilities in code

System Instructions:
You are a security expert specialized in identifying and fixing code vulnerabilities. When analyzing code:

1. Scan for common vulnerabilities:
   - SQL injection
   - Cross-site scripting (XSS)
   - Cross-site request forgery (CSRF)
   - Authentication flaws
   - Authorization bypasses
   - Insecure direct object references
   - Security misconfiguration
   - Sensitive data exposure
   - Broken access control
   - Insufficient logging/monitoring

2. For each identified issue:
   - Explain the vulnerability in clear terms
   - Rate severity (Critical, High, Medium, Low)
   - Provide a secure implementation alternative
   - Include references to security best practices

3. Prioritize fixes based on:
   - Exploitability
   - Potential impact
   - Complexity of the fix

4. Always verify input validation, output encoding, and authentication mechanisms.
5. Check for hardcoded credentials or secrets.
6. Verify proper encryption for sensitive data.
7. Examine dependency security and version management.
```

#### Creating a QA Tester Mode

```
Name: QA Tester
Description: Focuses on testing, edge cases, and reliability

System Instructions:
You are a thorough QA engineer specializing in software testing. When reviewing code:

1. Identify all possible test scenarios:
   - Happy paths
   - Edge cases
   - Boundary conditions
   - Error handling paths
   - Performance considerations

2. For each function or component, suggest:
   - Unit tests with clear assertions
   - Integration test scenarios
   - Edge case tests
   - Performance tests (if applicable)

3. Apply testing best practices:
   - Use descriptive test names
   - Follow Arrange-Act-Assert pattern
   - Isolate tests properly
   - Mock external dependencies
   - Consider test data management

4. Check for common issues:
   - Undefined or null handling
   - Empty collections
   - Boundary values
   - Concurrency issues
   - Resource leaks
   - Error propagation

5. Generate test code using the appropriate testing framework for the project.
```

#### Using the Security Auditor Mode for Code Review

```
[Switching to Security Auditor mode]

Please review this authentication function for security vulnerabilities:

```javascript
function authenticateUser(username, password) {
  const query = `SELECT * FROM users WHERE username = '${username}' AND password = '${password}'`;
  
  return new Promise((resolve, reject) => {
    db.query(query, (err, results) => {
      if (err) {
        reject(err);
        return;
      }
      
      if (results.length > 0) {
        const user = results[0];
        const token = createToken({ id: user.id, role: user.role });
        resolve({ authenticated: true, token, user });
      } else {
        resolve({ authenticated: false });
      }
    });
  });
}

function createToken(payload) {
  const secret = "my-secret-key";
  return jwt.sign(payload, secret, { expiresIn: '24h' });
}
```

### 4. How Different Modes Affect Roocode Behavior

Modes fundamentally change how Roocode interprets and responds to prompts:

#### Impact of Mode Selection

| Aspect | Impact of Mode Selection |
|--------|--------------------------|
| Code generation | Different styles, patterns, and approaches |
| Problem-solving approach | Prioritization of different factors |
| Level of detail | Mode-specific verbosity or conciseness |
| Focus areas | Emphasis on performance, security, readability, etc. |
| Recommendations | Different suggestions based on mode expertise |
| Response format | Structured according to mode's purpose |

#### Example: Same Prompt, Different Modes

**Prompt:** "Create a function to fetch and display user data"

**Default Mode Response:**
```javascript
async function fetchAndDisplayUsers() {
  try {
    const response = await fetch('/api/users');
    const users = await response.json();
    
    const userList = document.getElementById('user-list');
    userList.innerHTML = '';
    
    users.forEach(user => {
      const userElement = document.createElement('div');
      userElement.textContent = `${user.name} (${user.email})`;
      userList.appendChild(userElement);
    });
  } catch (error) {
    console.error('Error fetching users:', error);
  }
}
```

**Security Auditor Mode Response:**
```javascript
/**
 * Fetches and displays user data with security considerations
 * @returns {Promise<void>}
 */
async function fetchAndDisplayUsers() {
  try {
    // Use credentials: 'same-origin' to prevent CSRF
    const response = await fetch('/api/users', {
      credentials: 'same-origin',
      headers: {
        'Content-Type': 'application/json'
      }
    });
    
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    
    const users = await response.json();
    
    const userList = document.getElementById('user-list');
    if (!userList) {
      console.error('User list element not found');
      return;
    }
    
    // Clear list using safer methods
    while (userList.firstChild) {
      userList.removeChild(userList.firstChild);
    }
    
    // Display user data with XSS protection
    users.forEach(user => {
      const userElement = document.createElement('div');
      
      // Sanitize user data to prevent XSS
      const sanitizedName = document.createTextNode(user.name || '');
      const sanitizedEmail = document.createTextNode(user.email || '');
      
      const nameSpan = document.createElement('span');
      nameSpan.appendChild(sanitizedName);
      
      const emailSpan = document.createElement('span');
      emailSpan.appendChild(document.createTextNode(' ('));
      emailSpan.appendChild(sanitizedEmail);
      emailSpan.appendChild(document.createTextNode(')'));
      
      userElement.appendChild(nameSpan);
      userElement.appendChild(emailSpan);
      
      userList.appendChild(userElement);
    });
  } catch (error) {
    console.error('Error fetching users:', error);
    // Don't expose error details to the user
    const errorElement = document.getElementById('error-message');
    if (errorElement) {
      errorElement.textContent = 'Unable to load users. Please try again later.';
    }
  }
}
```

### 5. Practical Example: Using a Security Auditor Mode

Let's see how to apply the Security Auditor mode to a real codebase:

#### Security Audit Workflow

1. **Enable Security Auditor mode**
2. **Identify critical code paths** (authentication, payment processing, etc.)
3. **Scan each component** for security issues
4. **Prioritize findings** based on severity
5. **Implement fixes** for identified vulnerabilities
6. **Verify fixes** to ensure vulnerabilities are properly remediated

#### Example: Security Audit of an Express API

```
[Security Auditor Mode enabled]

Please review this Express API endpoint for security vulnerabilities:

```javascript
// User registration endpoint
app.post('/api/users/register', (req, res) => {
  const { username, password, email } = req.body;
  
  // Check if user exists
  const existingUser = db.users.find(u => u.username === username);
  if (existingUser) {
    return res.status(400).json({ error: 'Username already taken' });
  }
  
  // Create new user
  const newUser = {
    id: db.users.length + 1,
    username,
    password,
    email,
    role: req.body.role || 'user',
    createdAt: new Date()
  };
  
  db.users.push(newUser);
  
  // Generate token
  const token = jwt.sign(
    { id: newUser.id, username: newUser.username, role: newUser.role },
    'secret-key',
    { expiresIn: '7d' }
  );
  
  res.status(201).json({
    message: 'User registered successfully',
    token,
    user: newUser
  });
});
```

#### Security Issues and Fixes

After analyzing this code with the Security Auditor mode, Roocode would identify issues like:

1. **Plain text password storage**
2. **No input validation**
3. **Role assignment vulnerability**
4. **Hardcoded JWT secret**
5. **Sensitive data exposure**
6. **Missing rate limiting**

And would suggest fixes for each issue.

### 6. Creating Custom Modes for Different Project Needs

Tailor custom modes for specific development scenarios:

#### Domain-Specific Modes

1. **Frontend Developer Mode**: Specialized in UI components, accessibility, and browser compatibility
2. **Backend Developer Mode**: Focused on API design, database optimization, and server-side performance
3. **DevOps Mode**: Expert in deployment scripts, CI/CD pipelines, and infrastructure
4. **Mobile Developer Mode**: Specialized in responsive design and mobile-specific concerns

#### Project-Specific Modes

1. **Project Standards Mode**: Enforces your team's coding standards and patterns
2. **Legacy Code Mode**: Specialized in understanding and modifying older codebases
3. **Microservices Mode**: Focused on service boundaries, API contracts, and distributed system patterns
4. **Monorepo Mode**: Understanding module relationships in large repositories

#### Example: Creating a Project Standards Mode

```
Name: Company Standards
Description: Enforces our company's specific coding standards and practices

System Instructions:
You are a senior developer fully versed in our company's coding standards and best practices. When generating or reviewing code:

1. Follow our naming conventions:
   - camelCase for variables and functions
   - PascalCase for classes and components
   - UPPER_SNAKE_CASE for constants
   
2. Apply our file organization patterns:
   - One component per file
   - Group related functionality in modules
   - Follow the prescribed directory structure
   
3. Use our standard libraries and tools:
   - Prefer lodash for utility functions
   - Use axios for HTTP requests
   - Implement error handling with our ErrorBoundary component
   
4. Apply our code quality standards:
   - Maximum function length: 30 lines
   - Maximum file length: 300 lines
   - Maximum nesting depth: 3 levels
   
5. Include required documentation:
   - JSDoc for all public functions
   - README for each module
   - CHANGELOG entries for significant changes
   
6. Testing requirements:
   - Unit tests for all utility functions
   - Component tests for UI elements
   - Integration tests for API endpoints
```

### 7. Working with Rules Files (.rules)

Enhance your custom modes with standardized, shareable rules files:

#### What Are Rules Files?

Rules files are structured configuration files with a `.rules` extension that allow you to:

- Define consistent system instructions for Roocode
- Share standardized rules across your team
- Version control your AI guidance alongside code
- Apply project-specific standards automatically
- Create reusable rule sets for different project types

#### Rules File Formats

Rules files can be created in two formats:

1. **YAML Format** (`.rules.yaml` or `.rules.yml`)
   - Structured, hierarchical data format
   - Easier to parse programmatically
   - Good for complex rule sets with nested structure

2. **Markdown Format** (`.rules.md`)
   - More human-readable
   - Supports rich formatting and examples
   - Better for documentation-heavy rule sets

#### Creating Your First Rules File

Follow these steps to create an effective rules file:

1. **Choose your format** (YAML or Markdown)
2. **Create a new file** with a descriptive name and the `.rules` extension
3. **Define metadata** (name, description, version)
4. **Organize rules by category** (code style, architecture, etc.)
5. **Add specific instructions** under each category
6. **Include examples** to clarify expectations
7. **Save the file** in your project repository
8. **Reference the file** in your custom mode settings

#### YAML Format Example: Web Development Rules

Create a file named `web-project.rules.yaml`:

```yaml
name: "Web Development Standards"
description: "Standard rules for frontend web projects"
version: "1.0.0"
maintainer: "Web Development Team"

rules:
  - category: "Code Style"
    instructions:
      - "Use camelCase for variable and function names"
      - "Use PascalCase for component names"
      - "Use descriptive variable names that explain purpose"
      - "Keep line length under 80 characters"
      - "Use 2 spaces for indentation"
      
  - category: "React Patterns"
    instructions:
      - "Use functional components with hooks instead of class components"
      - "Keep components focused on a single responsibility"
      - "Extract reusable logic into custom hooks"
      - "Use React.memo for expensive renders"
      - "Implement proper prop validation"
      
  - category: "Performance"
    instructions:
      - "Avoid unnecessary re-renders"
      - "Use lazy loading for large components"
      - "Optimize images and assets"
      - "Implement code splitting for route-based chunks"
      - "Use windowing for long lists (react-window)"

frameworks:
  react:
    version: "^18.0.0"
    rules:
      - "Prefer useState over useReducer for simple state"
      - "Use Context API for state that needs to be accessed by many components"
      - "Implement error boundaries for component error handling"

environments:
  development:
    rules:
      - "Enable React strict mode"
      - "Use detailed error messages"
      - "Include comprehensive component prop documentation"
  
  production:
    rules:
      - "Remove all console.log statements"
      - "Implement proper error tracking"
      - "Optimize bundle size"
```

#### Markdown Format Example: API Development Rules

Create a file named `api-project.rules.md`:

```markdown
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
```

#### Mobile App Development Rules

Create a file named `mobile-app.rules.yaml`:

```yaml
name: "Mobile App Development Standards"
description: "Rules for React Native mobile applications"
version: "1.0.0"
maintainer: "Mobile Team"

rules:
  - category: "Architecture"
    instructions:
      - "Follow atomic design principles for UI components"
      - "Separate business logic from UI components"
      - "Use a navigation library consistently throughout the app"
      - "Implement proper state management"
      - "Handle device orientation changes gracefully"
  
  - category: "Performance"
    instructions:
      - "Minimize bridge crossings in React Native"
      - "Optimize list rendering with FlatList"
      - "Use PureComponent or memo for list items"
      - "Implement proper image caching"
      - "Reduce app size by optimizing assets"
  
  - category: "User Experience"
    instructions:
      - "Follow platform-specific design guidelines"
      - "Implement loading states for all async operations"
      - "Support both light and dark modes"
      - "Make touch targets at least 44x44 pts"
      - "Provide haptic feedback for important actions"
  
  - category: "Offline Support"
    instructions:
      - "Cache critical data for offline use"
      - "Handle network status changes gracefully"
      - "Implement background sync when connection is restored"
      - "Provide clear offline mode indicators"
      - "Persist user input to prevent data loss"

frameworks:
  react-native:
    version: "^0.70.0"
    rules:
      - "Use Reanimated for complex animations"
      - "Implement proper navigation with React Navigation"
      - "Use Hermes engine for improved performance"
```

#### Step-by-Step: Creating Project-Specific Rules Files

To create a rules file tailored to your project:

1. **Identify key requirements:**
   - Coding standards specific to your project/team
   - Common patterns and practices
   - Framework-specific guidelines
   - Project-specific constraints

2. **Organize rules by category:**
   - Group related rules under clear categories
   - Prioritize most important rules first
   - Keep instructions clear and actionable

3. **Add examples and clarifications:**
   - Include code examples of correct implementation
   - Explain the reasoning behind important rules
   - Document exceptions or special cases

4. **Review with your team:**
   - Ensure consensus on standards
   - Get feedback on clarity and completeness
   - Update based on team input

5. **Implement version control:**
   - Store rules files in your repository
   - Update version number when rules change
   - Document major changes in comments or changelog

#### Impact of Rules Files on Code Generation

Rules files significantly improve your experience with Roocode by:

1. **Consistency**: Ensuring all generated code follows the same standards
2. **Efficiency**: Reducing the need to repeat the same instructions in prompts
3. **Collaboration**: Creating shared understanding across team members
4. **Maintainability**: Making it easier to update and evolve standards
5. **Onboarding**: Helping new team members understand project standards

**Before using rules files:**
```
[Using default mode]
Create a React component for a user profile that displays the user's name, email, and profile picture. Make it responsive and follow best practices.
```

**After using rules files:**
```
[Using custom mode with web-project.rules.yaml]
Create a user profile component.
```

The second prompt, despite being shorter, would generate code that automatically follows all the standards defined in your rules file, including code style, React patterns, performance considerations, and more.

#### Integrating Rules Files with Custom Modes

To apply your rules file to a custom mode:

1. **In VS Code:**
   - Open Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`)
   - Type "Roocode: Manage Custom Modes"
   - Select "Edit Existing Mode" or "Create New Mode"
   - In the mode configuration, add a reference to your rules file:
     ```
     Rules File: ./path/to/your-project.rules.yaml
     ```

2. **Using direct prompts:**
   ```
   [Switch to Custom Mode]
   Please load the rules from ./path/to/your-project.rules.yaml and apply them to all code generation for this project.
   ```

#### Troubleshooting Common Rules File Issues

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| Rules not being applied | Incorrect file path | Double-check the path to your rules file |
| Conflicting rules | Contradictory instructions | Review and resolve conflicting guidance |
| Too many rules | Overloaded with instructions | Prioritize and simplify your rule set |
| Rules too restrictive | Overly specific constraints | Balance guidance with flexibility |
| YAML parsing errors | Syntax issues in YAML | Validate YAML syntax with a linter |
| Formatting problems in Markdown | Markdown syntax issues | Review Markdown formatting |

**Tip:** Start with a minimal set of critical rules and gradually expand as needed. This prevents overwhelming the AI with too many instructions at once.

### 8. Real-World Use Cases for Custom Modes

Discover practical applications of custom modes in development:

#### Use Case 1: Security Review

**Scenario**: Preparing for a security audit of your application

**Custom Mode Solution**: Create a Security Auditor mode that specializes in:
- Identifying common vulnerabilities (XSS, CSRF, injection)
- Reviewing authentication and authorization
- Checking for secure data handling
- Finding hardcoded secrets or credentials
- Verifying proper input validation

**Workflow**:
1. Switch to Security Auditor mode
2. Review each major component of your application
3. Compile a list of security issues
4. Prioritize and fix vulnerabilities

#### Use Case 2: Code Migration

**Scenario**: Migrating from an older framework/library to a newer one

**Custom Mode Solution**: Create a Migration Assistant mode that:
- Understands both the source and target frameworks
- Knows mapping patterns between equivalent features
- Identifies deprecated APIs and their replacements
- Provides step-by-step migration guidance
- Handles edge cases specific to your codebase

**Workflow**:
1. Define migration requirements in the custom mode
2. Process each file that needs updating
3. Apply consistent migration patterns
4. Validate the migrated code functions correctly

#### Use Case 3: Documentation Generation

**Scenario**: Creating comprehensive documentation for an existing codebase

**Custom Mode Solution**: Create a Documentation Specialist mode that:
- Analyzes code functions and components
- Generates clear explanations of their purpose
- Creates usage examples
- Identifies edge cases and limitations
- Formats documentation in your preferred style

**Workflow**:
1. Switch to Documentation Specialist mode
2. Process each module or component
3. Review and refine the generated documentation
4. Compile into comprehensive documentation

### 9. Exercise: Create a New Custom Mode

Hands-on practice creating a specialized mode:

#### Exercise: Performance Optimizer Mode

Create a custom mode focused on code performance optimization:

1. **Define the mode's purpose**: Identify and fix performance bottlenecks
2. **Specify the system instructions**: Detail how the AI should approach performance issues
3. **List performance patterns**: Common optimizations for your language/framework
4. **Create example scenarios**: Sample performance issues and solutions
5. **Test your mode**: Apply it to existing code and evaluate results

#### Mode Template

```
Name: Performance Optimizer
Description: [Your description]

System Instructions:
[Your detailed instructions about how the AI should approach performance optimization]

Key Focus Areas:
1. [Focus area 1]
2. [Focus area 2]
3. [Focus area 3]
...

Common Optimization Patterns:
- [Pattern 1]
- [Pattern 2]
- [Pattern 3]
...

Examples:
[Provide examples of before/after optimizations]
```

### 10. Common Mistakes and Best Practices for Custom Modes

Avoid pitfalls and optimize your custom modes:

#### Common Mistakes

1. **Overly restrictive instructions**: Limiting AI creativity too much
2. **Contradictory guidance**: Providing conflicting directives
3. **Lack of specificity**: Instructions too vague to be useful
4. **Over-engineering**: Creating overly complex modes
5. **Ignoring context**: Not considering the specific project context
6. **Assuming perfect memory**: Overloading with too many rules

#### Best Practices

1. **Clear purpose**: Define a specific focus for each mode
2. **Prioritized instructions**: List most important guidance first
3. **Concrete examples**: Provide clear examples of desired output
4. **Regular updates**: Refine modes based on actual usage
5. **Shared knowledge**: Document and share useful modes with your team
6. **Balance flexibility and constraints**: Guide without over-restricting

#### Example: Improving a Custom Mode

**Original Mode Instruction (Too Vague):**
```
Create good React components.
```

**Improved Mode Instruction:**
```
When creating React components:
1. Use functional components with hooks
2. Implement proper prop validation
3. Apply the single responsibility principle
4. Extract complex logic into custom hooks
5. Optimize rendering with useCallback and useMemo when appropriate
6. Structure JSX for readability with consistent indentation
7. Follow this component file structure:
   - Imports
   - Component definition
   - Prop types
   - Default props
   - Export statement
```

### 11. Combining Multiple Modes for Complex Workflows

Advanced strategies for leveraging multiple custom modes:

#### Mode Switching Strategies

1. **Sequential processing**: Apply different modes in a specific order
2. **Divide and conquer**: Use specialized modes for different aspects of a project
3. **Mode layering**: Start with a general mode, then refine with specialized ones
4. **Expert consultation**: Switch to specialist modes for specific questions
5. **Validation pipeline**: Use different modes to check different aspects of code

#### Example: Full Development Workflow

For developing a new feature:

1. **Planning Mode**: Outline feature requirements and architecture
2. **Implementation Mode**: Generate initial code with project standards
3. **QA Tester Mode**: Create comprehensive tests
4. **Security Auditor Mode**: Check for vulnerabilities
5. **Performance Optimizer Mode**: Enhance efficiency
6. **Documentation Mode**: Generate clear documentation

#### Practical Example

```
// Step 1: Feature planning
[Switch to Planning Mode]
"Design a user authentication system with login, registration, password reset, and profile management."

// Step 2: Implementation
[Switch to Implementation Mode]
"Let's implement the user registration component and API endpoint."

// Step 3: Testing
[Switch to QA Tester Mode]
"Create unit and integration tests for the registration functionality."

// Step 4: Security review
[Switch to Security Auditor Mode]
"Review the registration implementation for security vulnerabilities."

// Step 5: Performance optimization
[Switch to Performance Optimizer Mode]
"Optimize the form validation and API request handling."

// Step 6: Documentation
[Switch to Documentation Mode]
"Create comprehensive documentation for the registration feature."
```

## 🎯 Practice Exercises

1. **Custom Mode Creation**
   - Create a custom mode for code review
   - Define clear system instructions
   - Test it on a sample codebase
   - Refine based on results

2. **Mode Comparison**
   - Generate code using 3 different modes
   - Compare and contrast the results
   - Identify strengths and weaknesses of each
   - Document which situations each is best suited for

3. **Complex Workflow**
   - Design a multi-mode workflow for a specific project
   - Create the necessary custom modes
   - Document a step-by-step process
   - Apply it to a simple task

## 📝 Lesson Summary

Key takeaways:

- Custom modes transform Roocode into specialized coding assistants
- Creating effective modes requires clear, focused instructions
- Different modes produce significantly different code for the same prompt
- Rules files (.rules) provide standardized, shareable configurations for consistent AI behavior
- YAML and Markdown formats offer flexible options for defining project-specific rules
- Specialized modes like Security Auditor can help identify critical issues
- Rules files significantly improve team collaboration and code consistency
- Combining multiple modes creates powerful development workflows
- Regular refinement improves mode effectiveness over time

## 🚀 Next Steps

1. Complete the practice exercises
2. Create custom modes for your specific projects
3. Document successful modes to share with your team
4. Prepare for Lesson 8: Testing and Quality Assurance via Vibecoding

## 📚 Additional Resources

- [Prompt Engineering Guide](https://www.promptingguide.ai/)
- [OWASP Top 10 Web Application Security Risks](https://owasp.org/www-project-top-ten/)
- [Testing Best Practices](https://github.com/goldbergyoni/javascript-testing-best-practices)
- [Clean Code Principles](https://github.com/ryanmcdermott/clean-code-javascript)
- [Rules Files Templates Repository](https://github.com/vibecoding/roocode-rules-templates)
- [YAML Syntax Guide](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html)
- [Markdown Guide for Rules Files](https://www.markdownguide.org/basic-syntax/)