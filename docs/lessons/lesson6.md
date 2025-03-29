# Lesson 6: Refactoring and Optimization

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Use Roocode to refactor and optimize existing code
- Enhance code readability and maintainability
- Apply large-scale code changes efficiently
- Generate comprehensive documentation for your code
- Balance automation and manual oversight in refactoring
- Build sustainable codebases with AI assistance

## 📚 Lesson Content

### 1. Why Refactoring is Crucial in AI-Assisted Workflows

Refactoring plays a special role in vibecoding:

#### Importance of Refactoring AI-Generated Code

1. **Quality enhancement**: AI may generate functional but sub-optimal code
2. **Consistency maintenance**: Ensure AI output follows project standards
3. **Technical debt prevention**: Address issues before they accumulate
4. **Performance optimization**: Improve efficiency of AI-generated solutions
5. **Knowledge integration**: Merge AI capabilities with human expertise

#### The Refactoring Mindset for Vibecoding

When working with AI-generated code, approach refactoring as:
- An expected part of the workflow, not a fix for mistakes
- A collaborative process between human intelligence and AI
- An opportunity to teach the AI your preferences
- A way to incrementally improve code quality

### 2. Using Roocode to Enhance Readability & Efficiency

Roocode can transform messy code into clean, efficient code:

#### Code Readability Improvements

1. **Consistent naming**: Align variable and function names with conventions
2. **Logical structure**: Reorganize code for better flow and understanding
3. **Comments and documentation**: Add explanatory text
4. **Code formatting**: Improve indentation and spacing
5. **Modularization**: Break complex functions into smaller, focused ones

#### Efficiency Optimizations

1. **Algorithm improvements**: Replace inefficient algorithms with better ones
2. **Resource management**: Minimize memory usage and processing time
3. **Redundancy elimination**: Remove duplicate or unnecessary code
4. **Caching implementation**: Add caching for expensive operations
5. **Asynchronous processing**: Convert blocking operations to non-blocking

#### Example: Readability Enhancement

**Before refactoring**:
```javascript
function x(a, b) {
  let r = [];
  for (let i = 0; i < a.length; i++) {
    if (a[i].t === b) {
      r.push(a[i]);
    }
  }
  return r;
}
```

**Prompt for Roocode**:
```
Refactor this function to improve readability with:
1. Meaningful variable and function names
2. Modern JavaScript features like array methods
3. JSDoc comments explaining purpose and parameters
```

**After refactoring**:
```javascript
/**
 * Filters an array of items based on a specified type
 * @param {Array} items - The array of items to filter
 * @param {string} targetType - The type to filter by
 * @returns {Array} - A new array containing only items of the target type
 */
function filterItemsByType(items, targetType) {
  return items.filter(item => item.type === targetType);
}
```

### 3. Demo: Refactor Messy Codebase (Real-World Example)

Let's refactor a poorly structured utility library:

#### Original Code

```javascript
// utils.js - A messy utility library
const formatDate = (d) => {
  if (!d) return '';
  let day = d.getDate();
  let month = d.getMonth() + 1;
  let year = d.getFullYear();
  day = day < 10 ? '0' + day : day;
  month = month < 10 ? '0' + month : month;
  return `${day}/${month}/${year}`;
};

const formatCur = (n, c = 'USD') => {
  if (isNaN(n)) return '0.00';
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: c,
  }).format(n);
};

function validateEmail(e) {
  const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
  return re.test(String(e).toLowerCase());
}

const str_to_slug = (str) => {
  str = str.replace(/^\s+|\s+$/g, ''); // trim
  str = str.toLowerCase();
  
  // remove accents, swap ñ for n, etc
  var from = "àáäâèéëêìíïîòóöôùúüûñç·/_,:;";
  var to   = "aaaaeeeeiiiioooouuuunc------";
  for (var i=0, l=from.length ; i<l ; i++) {
    str = str.replace(new RegExp(from.charAt(i), 'g'), to.charAt(i));
  }

  str = str.replace(/[^a-z0-9 -]/g, '') // remove invalid chars
    .replace(/\s+/g, '-') // collapse whitespace and replace by -
    .replace(/-+/g, '-'); // collapse dashes

  return str;
};

function debounce(func, wait) {
  let timeout;
  return function() {
    const context = this, args = arguments;
    clearTimeout(timeout);
    timeout = setTimeout(function() {
      func.apply(context, args);
    }, wait);
  };
}

// Utility to check if an object is empty
const isEmpty = (obj) => {
  return Object.keys(obj).length === 0;
};

// Get local storage item with expiry
const getWithExpiry = (key) => {
  const itemStr = localStorage.getItem(key);
  if (!itemStr) return null;
  
  const item = JSON.parse(itemStr);
  const now = new Date();
  
  if (now.getTime() > item.expiry) {
    localStorage.removeItem(key);
    return null;
  }
  
  return item.value;
};

// Set local storage with expiry
const setWithExpiry = (key, value, ttl) => {
  const now = new Date();
  const item = {
    value: value,
    expiry: now.getTime() + ttl,
  };
  localStorage.setItem(key, JSON.stringify(item));
};

// Export everything as an object
module.exports = {
  formatDate,
  formatCur,
  validateEmail,
  str_to_slug,
  debounce,
  isEmpty,
  getWithExpiry,
  setWithExpiry
};
```

#### Refactoring Process

1. **Initial analysis**:
   ```
   Analyze this utility library and identify issues with:
   1. Naming consistency
   2. Code organization
   3. Error handling
   4. Documentation
   5. Modern JavaScript practices
   ```

2. **First refactoring round - structure and naming**:
   ```
   Refactor this utility library with:
   1. Consistent naming conventions (camelCase for all functions)
   2. Organized code by grouping related functions together
   3. Add JSDoc comments for each function
   4. Apply modern JavaScript features (arrow functions, template literals consistently)
   ```

3. **Second round - error handling and robustness**:
   ```
   Enhance the refactored utility library with:
   1. Proper parameter validation
   2. Defensive programming techniques
   3. Consistent error handling
   4. Type checking for inputs
   ```

4. **Final round - optimization and advanced features**:
   ```
   Optimize the utility library with:
   1. Performance improvements for the slug and debounce functions
   2. Add common use case examples in comments
   3. Export functions individually for better tree-shaking
   4. Add TypeScript type definitions
   ```

### 4. Roocode Refactoring Prompts and Techniques

Master these refactoring patterns with Roocode:

#### Effective Refactoring Prompts

1. **Targeted scope**: "Refactor this function to improve X without changing Y"
2. **Progressive improvement**: "First improve naming, then we'll address error handling"
3. **Constraint-based**: "Refactor this code following the airbnb style guide"
4. **Learning-oriented**: "Refactor this code and explain your reasoning"
5. **Pattern application**: "Apply the Strategy pattern to this code"

#### Common Refactoring Techniques

1. **Extract method/function**: Split large functions into smaller ones
2. **Rename variables/functions**: Use descriptive names
3. **Replace conditional with polymorphism**: Use object-oriented patterns
4. **Simplify complex expressions**: Break down complicated logic
5. **Consolidate duplicate code**: Remove repetition

#### Example: Extracting Functions

**Original code**:
```javascript
function processOrder(order) {
  // Validate order
  if (!order.items || order.items.length === 0) {
    throw new Error('Order must have items');
  }
  
  // Calculate totals
  let subtotal = 0;
  for (const item of order.items) {
    subtotal += item.price * item.quantity;
  }
  
  // Apply discounts
  let discount = 0;
  if (order.couponCode === 'SAVE10') {
    discount = subtotal * 0.1;
  } else if (order.couponCode === 'SAVE20') {
    discount = subtotal * 0.2;
  }
  
  // Calculate tax
  const taxRate = 0.08;
  const tax = (subtotal - discount) * taxRate;
  
  // Calculate final total
  const total = subtotal - discount + tax;
  
  return {
    subtotal,
    discount,
    tax,
    total
  };
}
```

**Prompt**:
```
Refactor this function by extracting smaller functions for each logical step:
1. Order validation
2. Subtotal calculation
3. Discount application
4. Tax calculation
Use modern JavaScript and maintain the same behavior.
```

### 5. Hands-on Exercise: Optimize Provided Code Snippet

Practice refactoring with this data processing function:

```javascript
// User data processor with performance issues
function processUserData(users) {
  // Filter active users
  const activeUsers = [];
  for (let i = 0; i < users.length; i++) {
    if (users[i].status === 'active') {
      activeUsers.push(users[i]);
    }
  }
  
  // Calculate total purchases
  let totalPurchases = 0;
  for (let i = 0; i < activeUsers.length; i++) {
    const user = activeUsers[i];
    for (let j = 0; j < user.purchases.length; j++) {
      totalPurchases += user.purchases[j].amount;
    }
  }
  
  // Find users with high value purchases
  const highValueUsers = [];
  for (let i = 0; i < activeUsers.length; i++) {
    const user = activeUsers[i];
    let userTotal = 0;
    
    for (let j = 0; j < user.purchases.length; j++) {
      userTotal += user.purchases[j].amount;
    }
    
    if (userTotal > 1000) {
      highValueUsers.push({
        id: user.id,
        name: user.name,
        email: user.email,
        totalSpent: userTotal
      });
    }
  }
  
  // Sort high value users by total spent
  for (let i = 0; i < highValueUsers.length; i++) {
    for (let j = i + 1; j < highValueUsers.length; j++) {
      if (highValueUsers[i].totalSpent < highValueUsers[j].totalSpent) {
        const temp = highValueUsers[i];
        highValueUsers[i] = highValueUsers[j];
        highValueUsers[j] = temp;
      }
    }
  }
  
  return {
    totalActiveUsers: activeUsers.length,
    totalPurchaseAmount: totalPurchases,
    highValueUsers: highValueUsers.slice(0, 10) // Top 10 high value users
  };
}
```

**Exercise Steps**:
1. Identify performance and readability issues
2. Refactor using modern JavaScript methods (map, filter, reduce)
3. Optimize algorithms for better performance
4. Add proper error handling and validation
5. Test with sample data to verify correctness

### 6. Using AI for Code Documentation and Comments

Leverage Roocode to create comprehensive documentation:

#### Types of Documentation to Generate

1. **Function/method documentation**: Parameter descriptions, return values
2. **Class/module overview**: Purpose, usage patterns, examples
3. **API documentation**: Endpoint descriptions, request/response formats
4. **Architecture documentation**: System components and interactions
5. **Code comments**: Explanations for complex sections or algorithms

#### Example: Generating Documentation

```
Add comprehensive JSDoc documentation to this React component:

```jsx
function DataTable({ data, columns, sortable, pagination }) {
  const [sortConfig, setSortConfig] = useState({ key: null, direction: 'asc' });
  const [currentPage, setCurrentPage] = useState(1);
  const pageSize = pagination?.pageSize || 10;
  
  const sortedData = useMemo(() => {
    if (!sortConfig.key || !sortable) return data;
    return [...data].sort((a, b) => {
      if (a[sortConfig.key] < b[sortConfig.key]) {
        return sortConfig.direction === 'asc' ? -1 : 1;
      }
      if (a[sortConfig.key] > b[sortConfig.key]) {
        return sortConfig.direction === 'asc' ? 1 : -1;
      }
      return 0;
    });
  }, [data, sortConfig, sortable]);
  
  const paginatedData = useMemo(() => {
    if (!pagination) return sortedData;
    const startIndex = (currentPage - 1) * pageSize;
    return sortedData.slice(startIndex, startIndex + pageSize);
  }, [sortedData, currentPage, pageSize, pagination]);
  
  const handleSort = (key) => {
    if (!sortable) return;
    setSortConfig(prevConfig => ({
      key,
      direction: prevConfig.key === key && prevConfig.direction === 'asc' ? 'desc' : 'asc',
    }));
  };
  
  const totalPages = pagination ? Math.ceil(data.length / pageSize) : 1;
  
  return (
    <div className="data-table-container">
      <table className="data-table">
        <thead>
          <tr>
            {columns.map(column => (
              <th 
                key={column.key} 
                onClick={() => handleSort(column.key)}
                className={sortable ? 'sortable' : ''}
              >
                {column.title}
                {sortConfig.key === column.key && (
                  <span className={`sort-${sortConfig.direction}`} />
                )}
              </th>
            ))}
          </tr>
        </thead>
        <tbody>
          {paginatedData.map((row, index) => (
            <tr key={row.id || index}>
              {columns.map(column => (
                <td key={column.key}>{row[column.key]}</td>
              ))}
            </tr>
          ))}
        </tbody>
      </table>
      
      {pagination && totalPages > 1 && (
        <div className="pagination">
          <button 
            disabled={currentPage === 1}
            onClick={() => setCurrentPage(page => Math.max(page - 1, 1))}
          >
            Previous
          </button>
          <span>Page {currentPage} of {totalPages}</span>
          <button
            disabled={currentPage === totalPages}
            onClick={() => setCurrentPage(page => Math.min(page + 1, totalPages))}
          >
            Next
          </button>
        </div>
      )}
    </div>
  );
}
```

### 7. Techniques for Validating Refactored Code

Ensure your refactored code maintains correctness:

#### Validation Approaches

1. **Unit testing**: Write tests to verify behavior before and after refactoring
2. **Snapshot comparison**: Compare outputs for the same inputs
3. **Code review**: Have AI review changes for potential issues
4. **Static analysis**: Use linters and type checking
5. **Incremental refactoring**: Make small changes and test frequently

#### Example: Verifying Refactored Code

```
I've refactored this sort function from using a bubble sort to a more efficient quicksort. Can you verify if the implementation is correct and will produce the same results?

Original function:
```javascript
function sortArray(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j+1]) {
        const temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;
      }
    }
  }
  return arr;
}
```

Refactored function:
```javascript
function sortArray(arr) {
  if (arr.length <= 1) {
    return arr;
  }
  
  const pivot = arr[Math.floor(arr.length / 2)];
  const left = [];
  const middle = [];
  const right = [];
  
  for (let element of arr) {
    if (element < pivot) {
      left.push(element);
    } else if (element > pivot) {
      right.push(element);
    } else {
      middle.push(element);
    }
  }
  
  return [...sortArray(left), ...middle, ...sortArray(right)];
}
```

Can you analyze if these two functions will always produce the same output for the same input? What are the tradeoffs?
```

### 8. Common Refactoring Scenarios

Master these frequent refactoring patterns:

#### Scenario 1: Extracting Reusable Logic

```
This component has duplicate logic for form validation. Refactor it to extract a custom hook for form validation that can be reused across components.

```jsx
function SignupForm() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [emailError, setEmailError] = useState('');
  const [passwordError, setPasswordError] = useState('');
  
  const validateEmail = () => {
    if (!email) {
      setEmailError('Email is required');
      return false;
    }
    if (!/\S+@\S+\.\S+/.test(email)) {
      setEmailError('Email is invalid');
      return false;
    }
    setEmailError('');
    return true;
  };
  
  const validatePassword = () => {
    if (!password) {
      setPasswordError('Password is required');
      return false;
    }
    if (password.length < 8) {
      setPasswordError('Password must be at least 8 characters');
      return false;
    }
    setPasswordError('');
    return true;
  };
  
  const handleSubmit = (e) => {
    e.preventDefault();
    const isEmailValid = validateEmail();
    const isPasswordValid = validatePassword();
    
    if (isEmailValid && isPasswordValid) {
      // Submit form
    }
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <div>
        <input
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          onBlur={validateEmail}
        />
        {emailError && <p className="error">{emailError}</p>}
      </div>
      <div>
        <input
          type="password"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
          onBlur={validatePassword}
        />
        {passwordError && <p className="error">{passwordError}</p>}
      </div>
      <button type="submit">Sign Up</button>
    </form>
  );
}
```

#### Scenario 2: Improving Data Processing

```
This component fetches and processes data inefficiently. Refactor it to optimize data fetching and processing, and handle loading/error states properly.

```jsx
function UserList() {
  const [users, setUsers] = useState([]);
  
  useEffect(() => {
    fetch('/api/users')
      .then(response => response.json())
      .then(data => {
        setUsers(data);
      });
  }, []);
  
  const activeUsers = [];
  for (let i = 0; i < users.length; i++) {
    if (users[i].status === 'active') {
      activeUsers.push(users[i]);
    }
  }
  
  const sortedUsers = [...activeUsers].sort((a, b) => {
    return a.name.localeCompare(b.name);
  });
  
  return (
    <div>
      <h2>User List</h2>
      <ul>
        {sortedUsers.map(user => (
          <li key={user.id}>{user.name} - {user.email}</li>
        ))}
      </ul>
    </div>
  );
}
```

### 9. Balancing Automation and Manual Oversight

Not everything should be automated in refactoring:

#### When to Use AI vs. Manual Refactoring

| Good for AI Refactoring | Better for Manual Refactoring |
|-------------------------|-------------------------------|
| Routine code formatting | Architectural changes |
| Documentation generation | Security-critical code |
| Variable/function renaming | Complex algorithm optimizations |
| Simple performance optimizations | Business logic changes |
| Applying consistent patterns | Critical system components |

#### Best Practices for Balancing Automation

1. **Review all AI changes**: Never blindly accept refactoring suggestions
2. **Start small**: Automate simple refactorings before complex ones
3. **Know your domain**: Keep domain-specific logic under manual control
4. **Use tests as safeguards**: Automated tests catch automated refactoring issues
5. **Combine approaches**: Use AI for initial refactoring, then manually refine

### 10. Building a Sustainable Codebase with Roocode

Create long-term codebase health with AI assistance:

#### Sustainable Codebase Practices

1. **Style guide enforcement**: Have Roocode apply consistent style rules
2. **Regular refactoring cycles**: Schedule periodic code improvement sessions
3. **Documentation maintenance**: Keep documentation in sync with code changes
4. **Technical debt tracking**: Use AI to identify and prioritize technical debt
5. **Knowledge transfer**: Use AI-generated explanations to onboard new developers

#### Example: Technical Debt Assessment

```
Review this codebase section and identify technical debt issues, prioritized by severity:

```javascript
// User authentication service
const users = {};

// Register a new user
function register(username, password) {
  if (users[username]) {
    return { success: false, message: 'User already exists' };
  }
  
  // Store password directly (not hashed)
  users[username] = { password, createdAt: new Date() };
  return { success: true };
}

// Login function
function login(username, password) {
  const user = users[username];
  if (!user) {
    return { success: false, message: 'User not found' };
  }
  
  if (user.password === password) {
    return { success: true, userData: user };
  } else {
    return { success: false, message: 'Incorrect password' };
  }
}

// Get all users (for admin panel)
function getAllUsers() {
  return users;
}

module.exports = { register, login, getAllUsers };
```

## 🎯 Practice Exercises

1. **Code Smell Detection**
   - Review a codebase for "code smells"
   - Use Roocode to identify refactoring opportunities
   - Document the issues and proposed solutions

2. **Progressive Refactoring**
   - Take a complex function
   - Refactor it in stages (naming, structure, algorithms)
   - Compare performance before and after

3. **Documentation Generation**
   - Select an undocumented module
   - Use Roocode to generate comprehensive documentation
   - Review and enhance the AI-generated documentation

## 📝 Lesson Summary

Key takeaways:

- Refactoring is a critical part of the vibecoding workflow
- AI excels at routine refactoring and documentation tasks
- Human oversight is essential for quality and security
- Effective refactoring requires clear prompts and validation
- Regular refactoring cycles maintain codebase health
- Combining AI and human expertise produces optimal results

## 🚀 Next Steps

1. Complete the practice exercises
2. Apply refactoring techniques to your own projects
3. Create a refactoring guide for your specific codebase
4. Prepare for Lesson 7: Advanced Roocode Features

## 📚 Additional Resources

- [Refactoring: Improving the Design of Existing Code](https://refactoring.com/)
- [Clean Code by Robert C. Martin](https://www.oreilly.com/library/view/clean-code-a/9780136083238/)
- [Performance Optimization Techniques](https://web.dev/fast/)
- [JavaScript Patterns by Stoyan Stefanov](https://www.oreilly.com/library/view/javascript-patterns/9781449399115/) 