# Lesson 5: Debugging and Error Handling with AI

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Understand common errors in AI-generated code
- Use Roocode to interpret and fix errors effectively
- Ask clarifying questions about code behavior
- Apply systematic debugging workflows with AI assistance
- Identify when manual debugging is necessary
- Overcome limitations in AI-assisted debugging

## 📚 Lesson Content

### 1. Common Errors and Debugging Principles in Roocode

Even AI-generated code isn't immune to bugs:

#### Types of Errors in AI-Generated Code

1. **Syntax errors**: Incorrect code structure or typos
2. **Logic errors**: Code runs but produces incorrect results
3. **Integration errors**: Components don't work together properly
4. **Incompatibility issues**: Dependencies or versions conflicts
5. **Missing implementation**: Incomplete code generation
6. **Hallucination errors**: References to non-existent functions or libraries

#### Debugging Principles with AI

1. **Isolate the issue**: Pinpoint exactly where the problem occurs
2. **Read error messages carefully**: Understand what the error indicates
3. **Think incrementally**: Fix one problem at a time
4. **Test after each change**: Verify fixes work before moving on
5. **Document the solutions**: Record what worked for future reference

### 2. Interpreting and Feeding Errors Back to Roocode

AI models can help interpret and fix errors if given the right information:

#### Effective Error Reporting to Roocode

1. **Include the full error message**: Provide complete error text
2. **Show code context**: Include the relevant code sections
3. **Explain what you expected**: Contrast with the actual behavior
4. **Describe any prior fixes**: Mention what you've already attempted
5. **Be specific about the desired outcome**: Clarify what "fixed" means

#### Example: Feeding Errors Back to Roocode

**Ineffective feedback**:
```
The code has an error. Can you fix it?
```

**Effective feedback**:
```
The authentication function is throwing this error:
"TypeError: Cannot read properties of undefined (reading 'token')"

Here's the relevant code:
```javascript
const authenticateUser = async (credentials) => {
  const response = await api.post('/auth/login', credentials);
  localStorage.setItem('token', response.data.user.token);
  return response.data.user;
};
```

I expected the function to store the token and return the user object, but it seems the response structure might be different than expected. Can you help fix this issue?
```

### 3. Using Roocode to Ask Clarifying Questions About Code

AI can help you understand code behavior:

#### Questions to Ask About Code

1. **Functionality questions**: "What does this function do?"
2. **Implementation details**: "How does this algorithm work?"
3. **Design rationale**: "Why was it implemented this way?"
4. **Alternative approaches**: "Is there a more efficient way to do this?"
5. **Potential issues**: "What edge cases might this code not handle?"

#### Example: Asking Clarifying Questions

```
Here's a piece of code I'm trying to understand:

```javascript
const debounce = (func, wait) => {
  let timeout;
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
};
```

Can you explain:
1. What this function does and when it would be useful
2. How the closure is working here
3. Why clearing the timeout before setting a new one is important
```

### 4. Step-by-Step Demo: Intentionally Breaking & Fixing Code

Let's work through a real debugging scenario:

#### Demo: Debugging a React Component

**Original Component with Bugs**:

```jsx
import React, { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState({});
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    const fetchUser = async () => {
      setLoading(true);
      try {
        const response = await fetch(`/api/users/${userId}`);
        const data = await response.json();
        setUser(data);
      } catch (error) {
        console.error('Error fetching user:', error);
      } finally {
        setLoading(false);
      }
    };
    
    fetchUser();
  });
  
  const handleUpdateProfile = async (updatedData) => {
    const response = await fetch(`/api/users/${userId}`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(updatedData),
    });
    
    if (response.ok) {
      const updatedUser = await response.json();
      setUser(updatedUser);
    }
  };
  
  if (loading) return <p>Loading...</p>;
  
  return (
    <div className="user-profile">
      <h2>{user.name}'s Profile</h2>
      <p>Email: {user.email}</p>
      <p>Role: {user.role}</p>
      <button onClick={() => handleUpdateProfile({ ...user, lastActive: new Date() })}>
        Update Last Active
      </button>
    </div>
  );
}

export default UserProfile;
```

**Debugging Process**:

1. **Identify the bugs**:
   - Missing dependency array in useEffect (causes infinite fetch loop)
   - No error handling in handleUpdateProfile
   - Potential error if user.name is undefined
   - Using POST instead of PUT for updates

2. **Ask Roocode to identify issues**:
   ```
   This UserProfile component has several bugs or issues. Can you identify them and explain the problems they might cause?
   ```

3. **Fix the issues one by one**:
   ```
   Let's fix the UserProfile component. Specifically:
   1. Add the proper dependency array to useEffect
   2. Add error handling to handleUpdateProfile
   3. Ensure the component handles the case where user data might be incomplete
   4. Fix the HTTP method for the update operation
   ```

4. **Test the fixes**:
   - Verify that fetching only happens when userId changes
   - Test error scenarios in both data fetching and updating
   - Check rendering with incomplete data

### 5. Understanding Roocode's Debugging Capabilities

Roocode offers several features to help with debugging:

#### Debugging Features

1. **Code analysis**: Identifying potential issues in existing code
2. **Error explanation**: Breaking down what an error message means
3. **Fix suggestions**: Proposing potential solutions
4. **Reasoning**: Explaining why a certain approach would work
5. **Testing**: Generating test cases to verify fixes

#### Example: Using Roocode for Debugging

```
I'm getting this error with my Express.js route handler:

TypeError: Cannot read property 'map' of undefined

Here's my code:
```javascript
app.get('/api/products', async (req, res) => {
  try {
    const products = await Product.find({ category: req.query.category });
    const simplifiedProducts = products.items.map(product => ({
      id: product._id,
      name: product.name,
      price: product.price
    }));
    res.json(simplifiedProducts);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

Can you help me understand what's causing this error and how to fix it?
```

### 6. Best Practices in Handling Logical and Syntax Errors

Different types of errors require different approaches:

#### Handling Syntax Errors

1. **Read the error message**: Identify line number and error type
2. **Format the code**: Proper indentation can reveal syntax issues
3. **Check for typos**: Missing parentheses, semicolons, or brackets
4. **Verify variable names**: Check for consistent naming
5. **Use Roocode to format and fix**: Let AI clean up syntax issues

#### Handling Logical Errors

1. **Understand the expected behavior**: Define what should happen
2. **Add console logs or debugger statements**: Trace execution flow
3. **Break complex logic into steps**: Test each part individually
4. **Use rubber duck debugging**: Explain the code to Roocode to find flaws
5. **Write test cases**: Create examples of inputs and expected outputs

#### Example: Debugging Different Error Types

**Syntax Error Example**:
```
This code has syntax errors. Can you identify and fix them?

```javascript
function calculateTotal(items) {
  let total = 0
  for (let i = 0; i < items.length i++) {
    total += items[i].price * items[i].quantity;
  
  return total;
}
```

**Logical Error Example**:
```
This function should calculate the average of an array of numbers, but it's not working correctly. Can you identify the logical error?

```javascript
function calculateAverage(numbers) {
  let sum = 0;
  for (let i = 0; i < numbers.length; i++) {
    sum += numbers[i];
  }
  return sum / numbers.length - 1;
}
```

### 7. Exercise: Debug a Small Roocode-Generated Program

Practice by debugging a problematic program:

#### Exercise: Fix the Bug Tracker

The following bug tracking application has several issues:

```javascript
// Bug Tracker Application
class BugTracker {
  constructor() {
    this.bugs = [];
    this.currentId = 0;
  }
  
  addBug(title, description, priority) {
    const newBug = {
      id: this.currentId++,
      title,
      description,
      priority,
      status: 'open',
      createdAt: new Date(),
    };
    this.bugs.push(newBug);
    return newBug;
  }
  
  getBug(id) {
    return this.bugs.find(bug => bug.id === id);
  }
  
  updateBugStatus(id, newStatus) {
    const bug = this.getBug(id);
    if (bug) {
      bug.status = newStatus;
    }
    return bug;
  }
  
  deleteBug(id) {
    const index = this.bugs.findIndex(bug => bug.id = id);
    if (index !== -1) {
      this.bugs.splice(index, 1);
      return true;
    }
    return false;
  }
  
  getBugsByStatus(status) {
    return this.bugs.filter(bug => bug.status = status);
  }
  
  getPriorityBugs() {
    return this.bugs.filter(bug => bug.priority === 'high');
  }
}

// Usage example
const tracker = new BugTracker();
tracker.addBug('Login Issue', 'Users cannot login with correct credentials', 'high');
tracker.addBug('Styling Problem', 'Button alignment is off on mobile devices', 'low');
console.log(tracker.getBugsByStatus('open')); // Should only show open bugs
console.log(tracker.getPriorityBugs()); // Should only show high priority bugs
tracker.updateBugStatus(0, 'in-progress');
console.log(tracker.getBug(0)); // Should show the updated bug
tracker.deleteBug(1);
console.log(tracker.bugs); // Should only have one bug left
```

**Debug Tasks**:
1. Identify all bugs in the code
2. Use Roocode to help analyze and fix each issue
3. Test the fixed code to ensure correct behavior
4. Document the bugs found and fixes applied

### 8. Recognizing When Manual Debugging is Needed

AI has limits in debugging complex issues:

#### When to Switch to Manual Debugging

1. **Complex state management issues**: When the problem involves intricate state flows
2. **Environment-specific bugs**: When the issue only occurs in certain environments
3. **Performance problems**: When the issue is related to efficiency, not correctness
4. **Library or framework-specific issues**: When deep domain knowledge is required
5. **Inconsistent behavior**: When the bug happens intermittently
6. **Runtime or timing issues**: When the problem involves asynchronous execution

#### Hybrid Debugging Approach

1. Use AI to identify potential issues and suggest fixes
2. Manually test and verify solutions in the actual environment
3. Use debugging tools (Chrome DevTools, VS Code Debugger, etc.)
4. Generate hypotheses with AI, then test them manually
5. Document findings for future use with AI

### 9. Debugging Workflows (prompt → test → iterate)

Establish a systematic debugging process:

#### Effective Debugging Workflow

1. **Identify the issue**: Understand what's not working
2. **Formulate a clear prompt**: Describe the problem to Roocode
3. **Analyze the response**: Understand the suggested fixes
4. **Implement changes**: Apply the proposed solution
5. **Test thoroughly**: Verify the fix works
6. **Iterate if needed**: If not resolved, provide more context and try again

#### Example Debugging Workflow

For a data processing function that returns incorrect results:

1. **Initial prompt**:
   ```
   This function should convert an array of user objects into a summary of active users per role, but it's returning incorrect results:

   ```javascript
   function summarizeUsersByRole(users) {
     const summary = {};
     users.forEach(user => {
       if (user.active) {
         if (summary[user.role]) {
           summary[user.role] += 1;
         } else {
           summary[user.role] = 1;
         }
       }
     });
   }
   ```

   Sample input:
   ```javascript
   const users = [
     { id: 1, name: 'Alice', role: 'admin', active: true },
     { id: 2, name: 'Bob', role: 'user', active: true },
     { id: 3, name: 'Charlie', role: 'user', active: false },
     { id: 4, name: 'Dana', role: 'admin', active: true }
   ];
   ```

   Expected output:
   ```javascript
   { admin: 2, user: 1 }
   ```

   But the function doesn't return anything. What's wrong?
   ```

2. **Apply fix and test**:
   Add the missing return statement and test with the sample data

3. **Iterate if needed**:
   If other issues appear during testing, refine the prompt with more details

### 10. Limitations and How to Overcome Them Effectively

Understand the boundaries of AI-assisted debugging:

#### Common Limitations

1. **Context limitations**: AI may not see the full codebase
2. **Lack of runtime information**: AI can't observe execution directly
3. **Environment-specific issues**: AI can't access your specific setup
4. **Complex interactions**: AI may struggle with intricate dependencies
5. **Specialized knowledge**: AI might lack deep framework-specific insights

#### Strategies to Overcome Limitations

1. **Provide more context**: Include related code and dependencies
2. **Share runtime information**: Provide logs, stack traces, and error messages
3. **Use specific examples**: Show inputs, expected outputs, and actual results
4. **Break down complex problems**: Focus on one aspect at a time
5. **Combine AI and human expertise**: Use AI for ideas, but apply your domain knowledge

#### Example: Overcoming Limitations

```
I'm debugging an issue with React's useEffect hook. Here's the component:

```jsx
function DataFetcher({ endpoint, onDataFetched }) {
  const [data, setData] = useState(null);
  
  useEffect(() => {
    let isMounted = true;
    
    const fetchData = async () => {
      try {
        const response = await fetch(endpoint);
        const result = await response.json();
        if (isMounted) {
          setData(result);
          onDataFetched(result);
        }
      } catch (error) {
        console.error('Fetch error:', error);
      }
    };
    
    fetchData();
    
    return () => {
      isMounted = false;
    };
  }, [endpoint]);
  
  return data ? <div>Data loaded</div> : <div>Loading...</div>;
}
```

I'm seeing this warning in the console:
"React Hook useEffect has a missing dependency: 'onDataFetched'. Either include it or remove the dependency array."

But when I add onDataFetched to the dependency array, it causes an infinite loop. Here's how I'm using the component:

```jsx
function ParentComponent() {
  const [results, setResults] = useState([]);
  
  const handleDataFetched = (data) => {
    setResults(prev => [...prev, ...data]);
  };
  
  return <DataFetcher endpoint="/api/data" onDataFetched={handleDataFetched} />;
}
```

How can I fix this issue without causing an infinite rerender loop?
```

## 🎯 Practice Exercises

1. **Error Analysis**
   - Take a piece of code with multiple bugs
   - Use Roocode to identify and explain each issue
   - Fix the problems and test the solution

2. **Debugging Workflow Practice**
   - Debug a more complex application
   - Document your debugging process
   - Note which problems AI could help with and which required manual intervention

3. **Create a Debugging Cheat Sheet**
   - Compile common errors and their solutions
   - Organize by error type or programming language
   - Include effective prompts for each scenario

## 📝 Lesson Summary

Key takeaways:

- AI can assist in debugging, but critical thinking is still essential
- Effective error reporting improves AI debugging suggestions
- Different error types require different debugging approaches
- A systematic debugging workflow produces better results
- Manual debugging complements AI assistance for complex issues
- Understanding AI limitations helps create effective debugging strategies

## 🚀 Next Steps

1. Complete the practice exercises
2. Apply the debugging workflows to your own projects
3. Build a personal library of effective debugging prompts
4. Prepare for Lesson 6: Refactoring and Optimization

## 📚 Additional Resources

- [Debugging Techniques](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/JavaScript#Debugging_problems)
- [Chrome DevTools Documentation](https://developer.chrome.com/docs/devtools/)
- [VS Code Debugging Guide](https://code.visualstudio.com/docs/editor/debugging)
- [Common JavaScript Errors and Solutions](https://blog.bitsrc.io/types-of-native-errors-in-javascript-you-must-know-b8238d40e492) 