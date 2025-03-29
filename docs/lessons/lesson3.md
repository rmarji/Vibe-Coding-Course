# Lesson 3: Basic Code Generation and Editing

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Generate code from scratch using Roocode
- Add code snippets to existing files
- Edit and refine AI-generated code
- Build a simple working application using vibecoding
- Verify and improve the quality of AI-generated code

## 📚 Lesson Content

### 1. Generating Code from Scratch

Roocode excels at creating new code files based on your specifications:

#### Starting a New Project

To create a new file or project:

1. Open VS Code with the Roocode extension installed
2. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
3. Type "Roocode: Create New File"
4. Provide a detailed description of what you want to create

Alternatively, you can:
1. Create an empty file with the appropriate extension
2. Open Roocode panel
3. Describe what code you want to generate

#### Example: Simple CLI Calculator

Let's create a basic command-line calculator in Python:

1. Create a new file named `calculator.py`
2. Open the Roocode panel
3. Enter this prompt:

```
Create a Python command-line calculator that:
1. Prompts the user to enter an arithmetic expression
2. Supports addition, subtraction, multiplication, and division
3. Validates the input to prevent execution of malicious code
4. Calculates and displays the result
5. Asks if the user wants to perform another calculation
6. Provides a clean exit mechanism
```

4. Review and run the generated code

### 2. Adding Code Snippets to Existing Files

You can use Roocode to enhance existing code files:

#### Techniques for Adding Code

1. **Describe the addition**: Tell Roocode what functionality you want to add
2. **Specify location**: Indicate where in the file the code should be inserted
3. **Provide context**: Explain how the new code should interact with existing code

#### Example: Enhancing Our Calculator

Let's add a history feature to our calculator:

1. Open the existing `calculator.py` file
2. Place the cursor where you want to add the feature
3. Open Roocode and enter:

```
Add a history feature to this calculator that:
1. Stores the last 5 calculations and results
2. Allows users to view the history by typing "history"
3. Incorporates seamlessly with the existing calculator code
4. Uses a list to store the history entries
```

4. Review the suggested changes and apply them

### 3. Editing and Refining AI-Generated Code

Not all AI-generated code will be perfect on the first attempt:

#### Strategies for Refinement

1. **Analyze the generated code**: Understand what the AI has created
2. **Identify issues or improvements**: Look for bugs, inefficiencies, or missing features
3. **Direct the AI to make changes**: Provide specific feedback on what to modify
4. **Iteratively improve**: Continue the cycle until the code meets your requirements

#### Example: Refining Our Calculator

Let's improve our calculator code:

1. Review the generated calculator with history feature
2. Identify areas for improvement (error handling, user experience, etc.)
3. Ask Roocode to refine it:

```
Improve the calculator by:
1. Adding error handling for division by zero
2. Improving the user interface with clearer prompts
3. Adding support for parentheses in expressions
4. Implementing a help command that explains available features
```

4. Review and test the improved code

### 4. Practical Demo: Building a Simple To-Do App

Let's build a more complex application from scratch:

#### Project Requirements

A simple console-based to-do list application with the following features:
- Add, view, edit, and delete tasks
- Mark tasks as complete
- Save tasks to a file
- Load tasks when the program starts
- Clean command-line interface

#### Step-by-Step Implementation

1. **Create the base structure**:
   ```
   Create a Python to-do list application that manages tasks through a command-line interface.
   ```

2. **Add core functionality**:
   ```
   Enhance the to-do app with functions to:
   1. Add new tasks with descriptions
   2. List all tasks with their status
   3. Mark tasks as complete
   4. Delete tasks
   ```

3. **Implement data persistence**:
   ```
   Add functionality to save tasks to a JSON file and load them when the program starts.
   ```

4. **Improve user experience**:
   ```
   Enhance the UI with:
   1. Colored output for different task states
   2. Numbered task listings
   3. Confirmation messages for actions
   4. Help command explaining available commands
   ```

5. **Run and test the application**

### 5. Reviewing AI-Generated Code for Quality

Critical assessment of AI-generated code is essential:

#### What to Look For

1. **Functionality**: Does the code do what it's supposed to do?
2. **Correctness**: Is the implementation logically sound?
3. **Efficiency**: Does it use resources appropriately?
4. **Security**: Are there any security vulnerabilities?
5. **Readability**: Is the code easy to understand?
6. **Maintainability**: Will it be easy to modify in the future?

#### Example: Code Review

Review our to-do application focusing on these aspects:
- Check for proper error handling
- Verify file I/O operations are secure
- Examine how user input is processed
- Assess code organization and structure
- Look for documentation and clear naming

### 6. Tips on Verifying Logic and Correctness

AI-generated code isn't guaranteed to be correct:

#### Verification Techniques

1. **Manual code review**: Carefully examine the logic and implementation
2. **Unit testing**: Run tests to verify correct behavior
3. **Edge case testing**: Try inputs that might cause problems
4. **Incremental testing**: Test each feature as it's added
5. **Ask Roocode to explain**: Have the AI describe how the code works

#### Example: Verifying Our To-Do App

Verify the to-do app by:
1. Examining how tasks are stored and retrieved
2. Testing edge cases (empty list, long task names, etc.)
3. Checking file operations for potential issues
4. Verifying task completion and deletion logic

### 7. Combining Manual Edits with AI-Assisted Code

For optimal results, combine your expertise with AI capabilities:

#### Effective Collaboration

1. **Generate the foundation**: Let AI create the basic structure
2. **Manual refinement**: Adjust key sections that need human expertise
3. **Ask for enhancements**: Have AI build upon your manual changes
4. **Iterative development**: Alternate between manual and AI-assisted work

#### Example: Hybrid Development

Enhance the to-do app with:
1. Manually add a priority system for tasks
2. Ask Roocode to integrate this system with the existing code
3. Manually adjust the UI to your preferences
4. Have Roocode optimize the final implementation

### 8. Exercise: Adding a New Feature

Practice by adding a feature to our to-do application:

#### Feature Requirements

Add a "due date" functionality that:
- Allows users to set due dates for tasks
- Shows tasks sorted by due date
- Highlights overdue tasks
- Includes a command to show tasks due today

#### Implementation Steps

1. Plan the feature implementation
2. Write a clear prompt for Roocode
3. Review and refine the generated code
4. Test the feature thoroughly
5. Document your process and results

### 9. Efficient Prompt Iteration Cycles

Develop a workflow for efficient code generation:

#### Iterative Process

1. **Start small**: Begin with a clear, focused prompt
2. **Quick review**: Rapidly assess the generated code
3. **Targeted feedback**: Provide specific guidance for improvements
4. **Continuous refinement**: Iterate until satisfied
5. **Test frequently**: Verify functionality at each step

#### Tips for Efficiency

- Keep iterations focused on specific aspects
- Save successful prompts for future reference
- Learn from unsuccessful prompts
- Maintain a clear goal for each iteration

### 10. Troubleshooting When Roocode Output Isn't Accurate

When the AI doesn't generate what you expected:

#### Common Issues and Solutions

1. **Ambiguous prompts**: Clarify and provide more details
2. **Misunderstood context**: Explain the surrounding code or project structure
3. **Technical limitations**: Break complex requests into simpler ones
4. **Missing domain knowledge**: Provide relevant background information
5. **Conflicting instructions**: Resolve inconsistencies in your requirements

#### Troubleshooting Process

1. Identify the specific issue with the generated code
2. Formulate a clear explanation of what needs to change
3. Provide additional context if necessary
4. Request a targeted fix for the problem
5. Verify the correction meets your requirements

## 🎯 Practice Exercises

1. **Basic Code Generation**
   - Generate a simple file handling utility
   - Test its functionality
   - Add error handling capabilities

2. **Code Enhancement**
   - Take an existing code snippet
   - Use Roocode to improve its functionality
   - Compare before and after versions

3. **Complete Mini-Project**
   - Build a simple web scraper or API client
   - Implement it incrementally using Roocode
   - Test and refine the final product

## 📝 Lesson Summary

Key takeaways:

- Roocode can generate complete code files from descriptions
- Adding code to existing files requires context and specificity
- Generated code should always be reviewed and refined
- Iterative development produces the best results
- Combining manual edits with AI assistance creates optimal code
- Clear, specific prompts lead to more accurate code generation

## 🚀 Next Steps

1. Complete the practice exercises
2. Experiment with generating different types of applications
3. Practice refining AI-generated code
4. Prepare for Lesson 4: Iterative Development and Workflow

## 📚 Additional Resources

- [Roocode Documentation: Code Generation](https://docs.roocode.com)
- [VS Code Official Documentation](https://code.visualstudio.com/docs)
- [Python Official Documentation](https://docs.python.org/3/)
- [Clean Code Principles](https://github.com/ryanmcdermott/clean-code-javascript) 