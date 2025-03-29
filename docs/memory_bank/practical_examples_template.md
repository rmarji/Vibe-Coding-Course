# Practical Examples Template

## Lesson 4: Iterative Development Example

### Example 1: API Endpoint Development

#### Initial Prompt
```
Create a Node.js Express API endpoint for user registration that:
- Validates email and password
- Hashes the password
- Stores user in MongoDB
- Returns JWT token
```

#### Initial Code Generated
```javascript
app.post('/register', async (req, res) => {
  const { email, password } = req.body;
  
  // Basic validation
  if (!email || !password) {
    return res.status(400).json({ error: 'Email and password required' });
  }
  
  try {
    // Store user
    const user = new User({ email, password });
    await user.save();
    
    // Generate token
    const token = jwt.sign({ userId: user._id }, 'secret');
    res.json({ token });
  } catch (error) {
    res.status(500).json({ error: 'Server error' });
  }
});
```

#### Improved Prompt
```
Create a Node.js Express API endpoint for user registration that:
- Validates email format using regex
- Requires password with min 8 chars, 1 uppercase, 1 number
- Hashes the password with bcrypt (10 rounds)
- Checks if email already exists in MongoDB
- Stores user with created date
- Returns JWT token that expires in 24h
- Includes proper error handling
```

#### Improved Code
```javascript
app.post('/register', async (req, res) => {
  try {
    const { email, password } = req.body;
    
    // Validation
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!email || !emailRegex.test(email)) {
      return res.status(400).json({ error: 'Valid email required' });
    }
    
    const passwordRegex = /^(?=.*[A-Z])(?=.*\d)[A-Za-z\d]{8,}$/;
    if (!password || !passwordRegex.test(password)) {
      return res.status(400).json({ 
        error: 'Password must have at least 8 characters, 1 uppercase letter and 1 number' 
      });
    }
    
    // Check if user exists
    const existingUser = await User.findOne({ email });
    if (existingUser) {
      return res.status(400).json({ error: 'Email already registered' });
    }
    
    // Hash password
    const salt = await bcrypt.genSalt(10);
    const hashedPassword = await bcrypt.hash(password, salt);
    
    // Create user
    const user = new User({
      email,
      password: hashedPassword,
      createdAt: new Date()
    });
    
    await user.save();
    
    // Generate token
    const token = jwt.sign(
      { userId: user._id }, 
      process.env.JWT_SECRET,
      { expiresIn: '24h' }
    );
    
    res.status(201).json({ 
      message: 'User registered successfully',
      token 
    });
  } catch (error) {
    console.error('Registration error:', error);
    res.status(500).json({ error: 'Server error occurred' });
  }
});
```

#### Key Improvements
- Added robust email/password validation
- Added duplicate user checking
- Implemented proper password hashing
- Added created date tracking
- Improved token security
- Enhanced error handling
- Better response format

## Lesson 7: Custom Modes Example

### Custom Mode: "Security Focused"

#### Configuration
```json
{
  "name": "Security Focused",
  "description": "Prioritizes security best practices in generated code",
  "parameters": {
    "temperature": 0.3,
    "systemPrompt": "You are an expert in secure coding practices. Prioritize security over simplicity. Always validate inputs, escape outputs, use parameterized queries, implement proper authentication and authorization, and follow the principle of least privilege. Explain potential security vulnerabilities in your comments."
  }
}
```

#### Example Prompt with Standard Mode
```
Create a function to retrieve user data from a database based on user ID
```

#### Standard Mode Output
```javascript
function getUserData(userId) {
  const query = `SELECT * FROM users WHERE id = ${userId}`;
  return database.execute(query);
}
```

#### Security Mode Output
```javascript
/**
 * Retrieves user data from the database
 * @param {string|number} userId - The user ID to look up
 * @returns {Promise<Object>} - User data object
 * 
 * Security considerations:
 * - Uses parameterized query to prevent SQL injection
 * - Validates user ID format
 * - Limits returned fields to prevent data exposure
 * - Throws specific errors for better error handling
 */
async function getUserData(userId) {
  // Input validation
  if (!userId || typeof userId !== 'number' && typeof userId !== 'string') {
    throw new Error('Invalid user ID format');
  }
  
  try {
    // Parameterized query to prevent SQL injection
    const query = 'SELECT id, name, email, created_at FROM users WHERE id = ?';
    const [rows] = await database.execute(query, [userId]);
    
    if (rows.length === 0) {
      throw new Error('User not found');
    }
    
    return rows[0];
  } catch (error) {
    // Log error but don't expose details to caller
    console.error('Database error:', error);
    throw new Error('Error retrieving user data');
  }
}
```

## Lesson 8: Testing Examples

### Test Generation Example

#### Prompt
```
Write unit tests for this user authentication function:

function authenticate(email, password) {
  if (!email || !password) {
    throw new Error('Email and password required');
  }
  
  const user = userDb.findByEmail(email);
  if (!user) {
    return { success: false, message: 'User not found' };
  }
  
  const isMatch = bcrypt.compareSync(password, user.passwordHash);
  if (!isMatch) {
    return { success: false, message: 'Invalid password' };
  }
  
  const token = jwt.sign({ id: user.id }, process.env.JWT_SECRET, { expiresIn: '1h' });
  return { success: true, token, userId: user.id };
}
```

#### Generated Tests
```javascript
const { authenticate } = require('./auth');
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');

// Mock dependencies
jest.mock('bcrypt');
jest.mock('jsonwebtoken');

describe('authenticate function', () => {
  let mockUserDb;
  
  beforeEach(() => {
    // Reset mocks
    jest.clearAllMocks();
    
    // Setup mock user database
    mockUserDb = {
      findByEmail: jest.fn()
    };
    
    // Restore the global object
    global.userDb = mockUserDb;
  });
  
  test('should throw error when email is missing', () => {
    expect(() => {
      authenticate(null, 'password123');
    }).toThrow('Email and password required');
  });
  
  test('should throw error when password is missing', () => {
    expect(() => {
      authenticate('user@example.com', null);
    }).toThrow('Email and password required');
  });
  
  test('should return failure when user not found', () => {
    mockUserDb.findByEmail.mockReturnValue(null);
    
    const result = authenticate('unknown@example.com', 'password123');
    
    expect(mockUserDb.findByEmail).toHaveBeenCalledWith('unknown@example.com');
    expect(result).toEqual({
      success: false,
      message: 'User not found'
    });
  });
  
  test('should return failure when password is incorrect', () => {
    const mockUser = {
      id: 'user123',
      email: 'user@example.com',
      passwordHash: 'hashedPassword'
    };
    
    mockUserDb.findByEmail.mockReturnValue(mockUser);
    bcrypt.compareSync.mockReturnValue(false);
    
    const result = authenticate('user@example.com', 'wrongPassword');
    
    expect(bcrypt.compareSync).toHaveBeenCalledWith('wrongPassword', 'hashedPassword');
    expect(result).toEqual({
      success: false,
      message: 'Invalid password'
    });
  });
  
  test('should return success with token when credentials are valid', () => {
    const mockUser = {
      id: 'user123',
      email: 'user@example.com',
      passwordHash: 'hashedPassword'
    };
    
    mockUserDb.findByEmail.mockReturnValue(mockUser);
    bcrypt.compareSync.mockReturnValue(true);
    jwt.sign.mockReturnValue('generated.jwt.token');
    
    // Mock environment variable
    process.env.JWT_SECRET = 'test-secret';
    
    const result = authenticate('user@example.com', 'correctPassword');
    
    expect(jwt.sign).toHaveBeenCalledWith(
      { id: 'user123' },
      'test-secret',
      { expiresIn: '1h' }
    );
    
    expect(result).toEqual({
      success: true,
      token: 'generated.jwt.token',
      userId: 'user123'
    });
  });
});
```

#### Testing Execution Results
```
 PASS  src/auth.test.js
  authenticate function
    ✓ should throw error when email is missing (3ms)
    ✓ should throw error when password is missing (1ms)
    ✓ should return failure when user not found (1ms)
    ✓ should return failure when password is incorrect (1ms)
    ✓ should return success with token when credentials are valid (2ms)

Test Suites: 1 passed, 1 total
Tests:       5 passed, 5 total
Snapshots:   0 total
Time:        1.5s
Ran all test suites matching /auth.test.js/i.
``` 