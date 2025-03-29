# Sample Code

This page provides reference code samples that you can use throughout the course to understand key concepts and implement features in the LearningPathAI project.

## Frontend (React/Next.js)

### Basic Component Structure

```jsx
// components/learning/LearningGoalInput.jsx
import { useState } from 'react';

export default function LearningGoalInput({ onSubmit }) {
  const [goal, setGoal] = useState('');
  const [currentLevel, setCurrentLevel] = useState('beginner');
  const [targetLevel, setTargetLevel] = useState('intermediate');
  
  const handleSubmit = (e) => {
    e.preventDefault();
    onSubmit({ goal, currentLevel, targetLevel });
  };
  
  return (
    <div className="bg-white shadow-md rounded-lg p-6">
      <h2 className="text-xl font-bold mb-4">Define Your Learning Goal</h2>
      <form onSubmit={handleSubmit}>
        <div className="mb-4">
          <label className="block text-gray-700 mb-2" htmlFor="goal">
            What do you want to learn?
          </label>
          <input
            id="goal"
            type="text"
            className="w-full px-3 py-2 border border-gray-300 rounded-md"
            placeholder="E.g., React development, Machine learning basics"
            value={goal}
            onChange={(e) => setGoal(e.target.value)}
            required
          />
        </div>
        
        <div className="mb-4">
          <label className="block text-gray-700 mb-2">Your current knowledge level:</label>
          <select
            className="w-full px-3 py-2 border border-gray-300 rounded-md"
            value={currentLevel}
            onChange={(e) => setCurrentLevel(e.target.value)}
          >
            <option value="beginner">Beginner</option>
            <option value="intermediate">Intermediate</option>
            <option value="advanced">Advanced</option>
          </select>
        </div>
        
        <div className="mb-6">
          <label className="block text-gray-700 mb-2">Your target knowledge level:</label>
          <select
            className="w-full px-3 py-2 border border-gray-300 rounded-md"
            value={targetLevel}
            onChange={(e) => setTargetLevel(e.target.value)}
          >
            <option value="intermediate">Intermediate</option>
            <option value="advanced">Advanced</option>
            <option value="expert">Expert</option>
          </select>
        </div>
        
        <button
          type="submit"
          className="w-full bg-indigo-600 text-white py-2 px-4 rounded-md hover:bg-indigo-700 transition-colors"
        >
          Generate Learning Path
        </button>
      </form>
    </div>
  );
}
```

### Learning Path Visualization

```jsx
// components/learning/LearningPathDisplay.jsx
import { useState } from 'react';

export default function LearningPathDisplay({ learningPath }) {
  const [expandedNodes, setExpandedNodes] = useState({});
  
  if (!learningPath || !learningPath.topics) {
    return <div className="p-6 text-center">No learning path available yet.</div>;
  }
  
  const toggleNode = (id) => {
    setExpandedNodes(prev => ({
      ...prev,
      [id]: !prev[id]
    }));
  };
  
  return (
    <div className="bg-white shadow-md rounded-lg p-6">
      <h2 className="text-xl font-bold mb-4">{learningPath.title}</h2>
      <p className="text-gray-600 mb-6">{learningPath.description}</p>
      
      <div className="space-y-4">
        {learningPath.topics.map((topic, index) => (
          <div key={index} className="border border-gray-200 rounded-md p-4">
            <div 
              className="flex justify-between items-center cursor-pointer"
              onClick={() => toggleNode(`topic-${index}`)}
            >
              <h3 className="text-lg font-semibold">{topic.title}</h3>
              <span>{expandedNodes[`topic-${index}`] ? '−' : '+'}</span>
            </div>
            
            {expandedNodes[`topic-${index}`] && (
              <div className="mt-3 pl-4 border-l-2 border-indigo-200">
                <p className="text-gray-600 mb-2">{topic.description}</p>
                
                {topic.resources && topic.resources.length > 0 && (
                  <div className="mt-3">
                    <h4 className="font-medium mb-2">Recommended Resources:</h4>
                    <ul className="list-disc pl-5 space-y-1">
                      {topic.resources.map((resource, idx) => (
                        <li key={idx}>
                          <a 
                            href={resource.url} 
                            target="_blank" 
                            rel="noopener noreferrer"
                            className="text-indigo-600 hover:underline"
                          >
                            {resource.title}
                          </a>
                          {resource.type && (
                            <span className="ml-2 text-xs bg-gray-100 px-2 py-1 rounded-full">
                              {resource.type}
                            </span>
                          )}
                        </li>
                      ))}
                    </ul>
                  </div>
                )}
                
                {topic.subtopics && topic.subtopics.length > 0 && (
                  <div className="mt-3">
                    <h4 className="font-medium mb-2">Subtopics:</h4>
                    <ul className="list-disc pl-5 space-y-1">
                      {topic.subtopics.map((subtopic, idx) => (
                        <li key={idx}>{subtopic.title}</li>
                      ))}
                    </ul>
                  </div>
                )}
              </div>
            )}
          </div>
        ))}
      </div>
    </div>
  );
}
```

### API Client Integration

```javascript
// services/api.js
import axios from 'axios';

const API_BASE_URL = process.env.NEXT_PUBLIC_API_URL || 'http://localhost:8000';

const apiClient = axios.create({
  baseURL: API_BASE_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Add authentication interceptor
apiClient.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('auth_token');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);

// Learning path API calls
export const learningPathApi = {
  generatePath: async (goalData) => {
    const response = await apiClient.post('/api/learning-paths/generate', goalData);
    return response.data;
  },
  
  getPath: async (pathId) => {
    const response = await apiClient.get(`/api/learning-paths/${pathId}`);
    return response.data;
  },
  
  updateProgress: async (pathId, progressData) => {
    const response = await apiClient.patch(`/api/learning-paths/${pathId}/progress`, progressData);
    return response.data;
  },
  
  searchResources: async (query, filters = {}) => {
    const response = await apiClient.get('/api/resources/search', { 
      params: { 
        query,
        ...filters
      } 
    });
    return response.data;
  }
};

// User API calls
export const userApi = {
  register: async (userData) => {
    const response = await apiClient.post('/api/users/register', userData);
    return response.data;
  },
  
  login: async (credentials) => {
    const response = await apiClient.post('/api/users/login', credentials);
    localStorage.setItem('auth_token', response.data.token);
    return response.data;
  },
  
  logout: () => {
    localStorage.removeItem('auth_token');
  },
  
  getProfile: async () => {
    const response = await apiClient.get('/api/users/me');
    return response.data;
  },
  
  updateProfile: async (profileData) => {
    const response = await apiClient.patch('/api/users/me', profileData);
    return response.data;
  }
};

export default apiClient;
```

## Backend (FastAPI/Pydantic)

### FastAPI App Configuration

```python
# backend/main.py
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
from app.api.routes import router as api_router
from app.core.config import settings

app = FastAPI(
    title=settings.PROJECT_NAME,
    description="API for LearningPathAI application",
    version="1.0.0",
)

# Set up CORS
app.add_middleware(
    CORSMiddleware,
    allow_origins=settings.CORS_ORIGINS,
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# Include API routes
app.include_router(api_router, prefix="/api")

@app.get("/")
async def root():
    return {"message": "Welcome to LearningPathAI API"}

if __name__ == "__main__":
    import uvicorn
    uvicorn.run("main:app", host="0.0.0.0", port=8000, reload=True)
```

### Pydantic Models

```python
# backend/app/models/learning_path.py
from typing import List, Optional
from datetime import datetime
from pydantic import BaseModel, Field, HttpUrl


class ResourceBase(BaseModel):
    title: str
    url: HttpUrl
    type: Optional[str] = None
    description: Optional[str] = None


class SubtopicBase(BaseModel):
    title: str
    description: Optional[str] = None


class TopicBase(BaseModel):
    title: str
    description: str
    resources: List[ResourceBase] = []
    subtopics: List[SubtopicBase] = []
    estimated_hours: Optional[int] = None


class LearningPathBase(BaseModel):
    title: str
    description: str
    goal: str
    current_level: str
    target_level: str
    topics: List[TopicBase] = []
    estimated_completion_weeks: Optional[int] = None


class LearningPathCreate(LearningPathBase):
    user_id: str


class LearningPathInDB(LearningPathBase):
    id: str = Field(..., alias="_id")
    user_id: str
    created_at: datetime
    updated_at: datetime
    

class LearningPathUpdate(BaseModel):
    title: Optional[str] = None
    description: Optional[str] = None
    topics: Optional[List[TopicBase]] = None
    estimated_completion_weeks: Optional[int] = None


class LearningPathOut(LearningPathBase):
    id: str
    created_at: datetime
    updated_at: datetime
    
    class Config:
        orm_mode = True
```

### FastAPI Routes

```python
# backend/app/api/routes/learning_paths.py
from fastapi import APIRouter, Depends, HTTPException, status
from typing import List
from app.models.learning_path import (
    LearningPathCreate,
    LearningPathOut,
    LearningPathUpdate
)
from app.services.path import LearningPathService
from app.services.llm import LLMService
from app.api.deps import get_current_user, get_path_service, get_llm_service

router = APIRouter()

@router.post("/generate", response_model=LearningPathOut, status_code=status.HTTP_201_CREATED)
async def generate_learning_path(
    data: LearningPathCreate,
    current_user = Depends(get_current_user),
    path_service: LearningPathService = Depends(get_path_service),
    llm_service: LLMService = Depends(get_llm_service)
):
    """Generate a new learning path based on user goals and preferences."""
    # Add the current user's ID to the data
    data.user_id = current_user.id
    
    # Use the LLM service to generate the learning path content
    generated_path = await llm_service.generate_learning_path(
        goal=data.goal,
        current_level=data.current_level,
        target_level=data.target_level
    )
    
    # Combine the generated content with the user's data
    path_data = LearningPathCreate(
        user_id=current_user.id,
        title=generated_path["title"],
        description=generated_path["description"],
        goal=data.goal,
        current_level=data.current_level,
        target_level=data.target_level,
        topics=generated_path["topics"],
        estimated_completion_weeks=generated_path["estimated_completion_weeks"]
    )
    
    # Save the learning path to the database
    created_path = await path_service.create(path_data)
    return created_path


@router.get("/{path_id}", response_model=LearningPathOut)
async def get_learning_path(
    path_id: str,
    current_user = Depends(get_current_user),
    path_service: LearningPathService = Depends(get_path_service)
):
    """Get a specific learning path by ID."""
    path = await path_service.get(path_id)
    
    if not path:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail="Learning path not found"
        )
    
    # Ensure the path belongs to the current user
    if path.user_id != current_user.id:
        raise HTTPException(
            status_code=status.HTTP_403_FORBIDDEN,
            detail="Not authorized to access this learning path"
        )
    
    return path


@router.get("/", response_model=List[LearningPathOut])
async def list_learning_paths(
    current_user = Depends(get_current_user),
    path_service: LearningPathService = Depends(get_path_service)
):
    """List all learning paths for the current user."""
    paths = await path_service.list_by_user(current_user.id)
    return paths


@router.patch("/{path_id}", response_model=LearningPathOut)
async def update_learning_path(
    path_id: str,
    data: LearningPathUpdate,
    current_user = Depends(get_current_user),
    path_service: LearningPathService = Depends(get_path_service)
):
    """Update a learning path."""
    path = await path_service.get(path_id)
    
    if not path:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail="Learning path not found"
        )
    
    # Ensure the path belongs to the current user
    if path.user_id != current_user.id:
        raise HTTPException(
            status_code=status.HTTP_403_FORBIDDEN,
            detail="Not authorized to modify this learning path"
        )
    
    updated_path = await path_service.update(path_id, data)
    return updated_path


@router.delete("/{path_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_learning_path(
    path_id: str,
    current_user = Depends(get_current_user),
    path_service: LearningPathService = Depends(get_path_service)
):
    """Delete a learning path."""
    path = await path_service.get(path_id)
    
    if not path:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail="Learning path not found"
        )
    
    # Ensure the path belongs to the current user
    if path.user_id != current_user.id:
        raise HTTPException(
            status_code=status.HTTP_403_FORBIDDEN,
            detail="Not authorized to delete this learning path"
        )
    
    await path_service.delete(path_id)
    return None
```

### LLM Integration Service

```python
# backend/app/services/llm.py
import os
from typing import Dict, Any, List
import openai
from app.core.config import settings

class LLMService:
    def __init__(self):
        openai.api_key = settings.OPENAI_API_KEY
    
    async def generate_learning_path(
        self, 
        goal: str, 
        current_level: str, 
        target_level: str
    ) -> Dict[str, Any]:
        """
        Generate a learning path using the OpenAI API based on user inputs.
        
        Args:
            goal: The learning goal specified by the user
            current_level: User's current knowledge level (beginner, intermediate, advanced)
            target_level: User's target knowledge level
            
        Returns:
            Dictionary containing the generated learning path
        """
        prompt = self._create_learning_path_prompt(goal, current_level, target_level)
        
        try:
            response = await openai.ChatCompletion.acreate(
                model=settings.OPENAI_MODEL,
                messages=[
                    {"role": "system", "content": "You are an expert educational designer specializing in creating personalized learning paths."},
                    {"role": "user", "content": prompt}
                ],
                temperature=0.7,
                max_tokens=2000
            )
            
            # Extract and parse the response
            content = response.choices[0].message.content
            path_data = self._parse_learning_path_response(content)
            
            # Add a default title and description if not present
            if "title" not in path_data:
                path_data["title"] = f"Learning Path for {goal}"
            
            if "description" not in path_data:
                path_data["description"] = f"A personalized learning path to help you progress from {current_level} to {target_level} level in {goal}."
            
            return path_data
        
        except Exception as e:
            # In a real application, you would log this error
            print(f"Error generating learning path: {e}")
            # Return a fallback learning path
            return self._generate_fallback_path(goal, current_level, target_level)
    
    def _create_learning_path_prompt(self, goal: str, current_level: str, target_level: str) -> str:
        """Create a prompt for the learning path generation."""
        return f"""
        Please create a structured learning path to help someone learn {goal}.
        
        The person's current knowledge level is: {current_level}
        Their target knowledge level is: {target_level}
        
        Provide your response in the following JSON structure:
        {{
            "title": "Title of the learning path",
            "description": "Brief description of what this path will help the learner achieve",
            "topics": [
                {{
                    "title": "Topic 1",
                    "description": "Description of this topic and why it's important",
                    "resources": [
                        {{
                            "title": "Resource title",
                            "url": "https://example.com",
                            "type": "article/video/course/book/etc",
                            "description": "Brief description of the resource"
                        }}
                    ],
                    "subtopics": [
                        {{
                            "title": "Subtopic title",
                            "description": "Description of this subtopic"
                        }}
                    ],
                    "estimated_hours": 5
                }}
            ],
            "estimated_completion_weeks": 6
        }}
        
        Include 4-8 main topics, with appropriate resources and subtopics for each.
        Focus on providing a clear progression that matches the learner's current and target levels.
        Recommend high-quality, specific resources (with actual URLs) for each topic.
        """
    
    def _parse_learning_path_response(self, content: str) -> Dict[str, Any]:
        """Parse the LLM response into a structured dictionary."""
        import json
        
        # Find and extract the JSON part of the response
        # This is a simple implementation - in a real app, you'd use more robust parsing
        try:
            # Try to parse the entire response as JSON
            return json.loads(content)
        except json.JSONDecodeError:
            # If that fails, look for JSON within the response text
            import re
            json_match = re.search(r'```json\n(.*?)\n```', content, re.DOTALL)
            if json_match:
                try:
                    return json.loads(json_match.group(1))
                except json.JSONDecodeError:
                    pass
            
            # If all parsing fails, return an empty structure
            return {
                "title": "",
                "description": "",
                "topics": [],
                "estimated_completion_weeks": 0
            }
    
    def _generate_fallback_path(self, goal: str, current_level: str, target_level: str) -> Dict[str, Any]:
        """Generate a simple fallback learning path when the API call fails."""
        return {
            "title": f"Learning Path for {goal}",
            "description": f"A structured path to learn {goal}, from {current_level} to {target_level} level.",
            "topics": [
                {
                    "title": "Getting Started",
                    "description": "Introduction to the fundamentals",
                    "resources": [
                        {
                            "title": "Beginner Guide",
                            "url": "https://example.com/guide",
                            "type": "article"
                        }
                    ],
                    "subtopics": [
                        {
                            "title": "Basic Concepts",
                            "description": "Understanding the core concepts"
                        }
                    ],
                    "estimated_hours": 5
                }
            ],
            "estimated_completion_weeks": 4
        }
```

### Perplexity Search Integration

```python
# backend/app/services/search.py
import aiohttp
import asyncio
from typing import Dict, List, Any, Optional
from app.core.config import settings

class PerplexitySearchService:
    def __init__(self):
        self.api_key = settings.PERPLEXITY_API_KEY
        self.base_url = "https://api.perplexity.ai/search"
        self.headers = {
            "Authorization": f"Bearer {self.api_key}",
            "Content-Type": "application/json"
        }
    
    async def search_learning_resources(
        self, 
        query: str, 
        resource_types: Optional[List[str]] = None,
        difficulty: Optional[str] = None,
        max_results: int = 5
    ) -> List[Dict[str, Any]]:
        """
        Search for learning resources using the Perplexity API.
        
        Args:
            query: The search query
            resource_types: Optional list of resource types to filter by (e.g., ["article", "video", "course"])
            difficulty: Optional difficulty level to filter by
            max_results: Maximum number of results to return
            
        Returns:
            List of resources with their metadata
        """
        # Construct the search query with filters
        search_query = query
        if resource_types:
            type_filter = " OR ".join([f"type:{t}" for t in resource_types])
            search_query += f" ({type_filter})"
        
        if difficulty:
            search_query += f" difficulty:{difficulty}"
        
        # Add a specific modifier to focus on educational content
        search_query += " educational resources learning materials tutorial"
        
        try:
            async with aiohttp.ClientSession() as session:
                async with session.post(
                    self.base_url,
                    headers=self.headers,
                    json={
                        "query": search_query,
                        "max_results": max_results
                    }
                ) as response:
                    if response.status != 200:
                        # Log the error in a real application
                        print(f"Error searching resources: {response.status}")
                        return []
                    
                    data = await response.json()
                    return self._process_search_results(data, query)
        
        except Exception as e:
            # Log the error in a real application
            print(f"Error during search request: {e}")
            return []
    
    def _process_search_results(self, data: Dict[str, Any], original_query: str) -> List[Dict[str, Any]]:
        """Process and format the search results."""
        results = []
        
        if "results" not in data:
            return results
        
        for item in data["results"]:
            # Extract and infer resource type from the URL and title
            resource_type = self._infer_resource_type(item.get("url", ""), item.get("title", ""))
            
            # Extract and process the relevant information
            result = {
                "title": item.get("title", "Untitled Resource"),
                "url": item.get("url", ""),
                "description": item.get("snippet", ""),
                "type": resource_type,
                "relevance_score": self._calculate_relevance(item, original_query)
            }
            
            results.append(result)
        
        # Sort by relevance score
        results.sort(key=lambda x: x["relevance_score"], reverse=True)
        
        return results
    
    def _infer_resource_type(self, url: str, title: str) -> str:
        """Infer the type of resource based on the URL and title."""
        url = url.lower()
        title = title.lower()
        
        # Check for common video platforms
        if any(platform in url for platform in ["youtube.com", "vimeo.com", "coursera.org/lecture"]):
            return "video"
        
        # Check for course platforms
        if any(platform in url for platform in ["coursera.org", "udemy.com", "edx.org", "udacity.com"]):
            return "course"
        
        # Check for documentation
        if any(term in url for term in ["docs.", "documentation", "reference"]):
            return "documentation"
        
        # Check for GitHub repositories
        if "github.com" in url:
            return "repository"
        
        # Check for common blog platforms
        if any(platform in url for platform in ["medium.com", "dev.to", "blog."]):
            return "article"
        
        # Check title for clues
        if any(term in title for term in ["tutorial", "guide", "how to"]):
            return "tutorial"
        
        if any(term in title for term in ["course", "class", "lesson"]):
            return "course"
        
        if any(term in title for term in ["cheat sheet", "cheatsheet"]):
            return "cheat sheet"
        
        # Default to article as a fallback
        return "article"
    
    def _calculate_relevance(self, item: Dict[str, Any], query: str) -> float:
        """Calculate a relevance score for the search result."""
        # This is a simplified implementation - in a real app, you'd use more sophisticated relevance calculation
        relevance = 0.0
        
        # Title match is important
        if "title" in item and query.lower() in item["title"].lower():
            relevance += 0.5
        
        # Content snippet match
        if "snippet" in item and query.lower() in item["snippet"].lower():
            relevance += 0.3
        
        # Domain authority (simplified)
        domain_authority = 0.0
        if "url" in item:
            url = item["url"].lower()
            # Give higher scores to known educational domains
            if any(domain in url for domain in [".edu", "coursera", "udemy", "edx", "udacity", "freecodecamp", "mdn", "w3schools"]):
                domain_authority = 0.2
        
        relevance += domain_authority
        
        return min(relevance, 1.0)  # Cap at 1.0
```

## Testing

### Frontend Tests (Jest)

```javascript
// __tests__/components/LearningGoalInput.test.js
import { render, screen, fireEvent } from '@testing-library/react';
import LearningGoalInput from '../../components/learning/LearningGoalInput';

describe('LearningGoalInput component', () => {
  const mockOnSubmit = jest.fn();
  
  beforeEach(() => {
    mockOnSubmit.mockClear();
  });
  
  it('renders the component correctly', () => {
    render(<LearningGoalInput onSubmit={mockOnSubmit} />);
    
    // Check for essential elements
    expect(screen.getByText('Define Your Learning Goal')).toBeInTheDocument();
    expect(screen.getByLabelText(/What do you want to learn?/i)).toBeInTheDocument();
    expect(screen.getByLabelText(/Your current knowledge level:/i)).toBeInTheDocument();
    expect(screen.getByLabelText(/Your target knowledge level:/i)).toBeInTheDocument();
    expect(screen.getByRole('button', { name: /Generate Learning Path/i })).toBeInTheDocument();
  });
  
  it('updates input values on change', () => {
    render(<LearningGoalInput onSubmit={mockOnSubmit} />);
    
    // Get form elements
    const goalInput = screen.getByLabelText(/What do you want to learn?/i);
    const currentLevelSelect = screen.getByLabelText(/Your current knowledge level:/i);
    const targetLevelSelect = screen.getByLabelText(/Your target knowledge level:/i);
    
    // Change input values
    fireEvent.change(goalInput, { target: { value: 'React Development' } });
    fireEvent.change(currentLevelSelect, { target: { value: 'intermediate' } });
    fireEvent.change(targetLevelSelect, { target: { value: 'advanced' } });
    
    // Check if values were updated
    expect(goalInput.value).toBe('React Development');
    expect(currentLevelSelect.value).toBe('intermediate');
    expect(targetLevelSelect.value).toBe('advanced');
  });
  
  it('calls onSubmit with correct data when form is submitted', () => {
    render(<LearningGoalInput onSubmit={mockOnSubmit} />);
    
    // Get form elements
    const goalInput = screen.getByLabelText(/What do you want to learn?/i);
    const currentLevelSelect = screen.getByLabelText(/Your current knowledge level:/i);
    const targetLevelSelect = screen.getByLabelText(/Your target knowledge level:/i);
    const submitButton = screen.getByRole('button', { name: /Generate Learning Path/i });
    
    // Fill the form
    fireEvent.change(goalInput, { target: { value: 'Python Programming' } });
    fireEvent.change(currentLevelSelect, { target: { value: 'beginner' } });
    fireEvent.change(targetLevelSelect, { target: { value: 'intermediate' } });
    
    // Submit the form
    fireEvent.click(submitButton);
    
    // Check if onSubmit was called with correct data
    expect(mockOnSubmit).toHaveBeenCalledTimes(1);
    expect(mockOnSubmit).toHaveBeenCalledWith({
      goal: 'Python Programming',
      currentLevel: 'beginner',
      targetLevel: 'intermediate'
    });
  });
  
  it('requires a goal to be entered', () => {
    render(<LearningGoalInput onSubmit={mockOnSubmit} />);
    
    // Try to submit without entering a goal
    const submitButton = screen.getByRole('button', { name: /Generate Learning Path/i });
    fireEvent.click(submitButton);
    
    // Check that onSubmit was not called
    expect(mockOnSubmit).not.toHaveBeenCalled();
  });
});
```

### Backend Tests (Pytest)

```python
# backend/tests/services/test_llm.py
import pytest
from unittest.mock import patch, AsyncMock
from app.services.llm import LLMService

@pytest.fixture
def llm_service():
    return LLMService()

@pytest.mark.asyncio
async def test_generate_learning_path_success(llm_service):
    # Mock the OpenAI API response
    mock_response = AsyncMock()
    mock_response.choices = [
        AsyncMock(
            message=AsyncMock(
                content="""
                {
                    "title": "Python Programming for Beginners",
                    "description": "A comprehensive path to learn Python programming from scratch",
                    "topics": [
                        {
                            "title": "Python Basics",
                            "description": "Understanding fundamental Python concepts",
                            "resources": [
                                {
                                    "title": "Python Official Tutorial",
                                    "url": "https://docs.python.org/3/tutorial/",
                                    "type": "documentation"
                                }
                            ],
                            "subtopics": [
                                {
                                    "title": "Variables and Data Types",
                                    "description": "Learn about Python's variable system"
                                }
                            ],
                            "estimated_hours": 10
                        }
                    ],
                    "estimated_completion_weeks": 4
                }
                """
            )
        )
    ]
    
    with patch('openai.ChatCompletion.acreate', return_value=mock_response):
        result = await llm_service.generate_learning_path(
            goal="Python Programming",
            current_level="beginner",
            target_level="intermediate"
        )
    
    # Verify the result
    assert result["title"] == "Python Programming for Beginners"
    assert result["description"] == "A comprehensive path to learn Python programming from scratch"
    assert len(result["topics"]) == 1
    assert result["topics"][0]["title"] == "Python Basics"
    assert result["estimated_completion_weeks"] == 4

@pytest.mark.asyncio
async def test_generate_learning_path_api_error(llm_service):
    # Mock an API error
    with patch('openai.ChatCompletion.acreate', side_effect=Exception("API Error")):
        result = await llm_service.generate_learning_path(
            goal="Python Programming",
            current_level="beginner",
            target_level="intermediate"
        )
    
    # Verify fallback path is returned
    assert "title" in result
    assert "description" in result
    assert "topics" in result
    assert isinstance(result["topics"], list)
    assert len(result["topics"]) > 0
    assert "estimated_completion_weeks" in result

@pytest.mark.asyncio
async def test_parse_learning_path_response_valid_json(llm_service):
    valid_json = '{"title": "Test Path", "description": "Test Description", "topics": [], "estimated_completion_weeks": 2}'
    
    result = llm_service._parse_learning_path_response(valid_json)
    
    assert result["title"] == "Test Path"
    assert result["description"] == "Test Description"
    assert result["topics"] == []
    assert result["estimated_completion_weeks"] == 2

@pytest.mark.asyncio
async def test_parse_learning_path_response_json_in_markdown(llm_service):
    markdown_with_json = """
    Here's a learning path for you:
    
    ```json
    {
        "title": "Markdown Path",
        "description": "Path in markdown",
        "topics": [],
        "estimated_completion_weeks": 3
    }
    ```
    
    I hope this helps!
    """
    
    result = llm_service._parse_learning_path_response(markdown_with_json)
    
    assert result["title"] == "Markdown Path"
    assert result["description"] == "Path in markdown"
    assert result["topics"] == []
    assert result["estimated_completion_weeks"] == 3

@pytest.mark.asyncio
async def test_parse_learning_path_response_invalid_format(llm_service):
    invalid_format = "This is not JSON or markdown with JSON"
    
    result = llm_service._parse_learning_path_response(invalid_format)
    
    # Should return the default empty structure
    assert "title" in result
    assert "description" in result
    assert "topics" in result
    assert "estimated_completion_weeks" in result
```

## Database Integration

### SQLAlchemy Models

```python
# backend/app/db/models.py
from sqlalchemy import Column, String, Integer, ForeignKey, Text, DateTime, Table
from sqlalchemy.orm import relationship
from sqlalchemy.sql import func
from sqlalchemy.dialects.postgresql import JSONB
from app.db.session import Base

class User(Base):
    __tablename__ = "users"
    
    id = Column(String, primary_key=True, index=True)
    email = Column(String, unique=True, index=True)
    hashed_password = Column(String)
    full_name = Column(String)
    created_at = Column(DateTime, server_default=func.now())
    updated_at = Column(DateTime, server_default=func.now(), onupdate=func.now())
    
    # Relationships
    learning_paths = relationship("LearningPath", back_populates="user")
    progress_records = relationship("UserProgress", back_populates="user")


class LearningPath(Base):
    __tablename__ = "learning_paths"
    
    id = Column(String, primary_key=True, index=True)
    user_id = Column(String, ForeignKey("users.id"))
    title = Column(String)
    description = Column(Text)
    goal = Column(String)
    current_level = Column(String)
    target_level = Column(String)
    content = Column(JSONB)  # Stores the full path content as JSON
    estimated_completion_weeks = Column(Integer)
    created_at = Column(DateTime, server_default=func.now())
    updated_at = Column(DateTime, server_default=func.now(), onupdate=func.now())
    
    # Relationships
    user = relationship("User", back_populates="learning_paths")
    progress_records = relationship("TopicProgress", back_populates="learning_path")


class TopicProgress(Base):
    __tablename__ = "topic_progress"
    
    id = Column(String, primary_key=True, index=True)
    learning_path_id = Column(String, ForeignKey("learning_paths.id"))
    topic_id = Column(String)  # References the topic ID in the JSON content
    status = Column(String)  # "not_started", "in_progress", "completed"
    completion_percentage = Column(Integer)
    created_at = Column(DateTime, server_default=func.now())
    updated_at = Column(DateTime, server_default=func.now(), onupdate=func.now())
    
    # Relationships
    learning_path = relationship("LearningPath", back_populates="progress_records")


class UserProgress(Base):
    __tablename__ = "user_progress"
    
    id = Column(String, primary_key=True, index=True)
    user_id = Column(String, ForeignKey("users.id"))
    learning_path_id = Column(String, ForeignKey("learning_paths.id"))
    overall_progress = Column(Integer)  # Percentage of the entire path completed
    last_activity = Column(DateTime)
    created_at = Column(DateTime, server_default=func.now())
    updated_at = Column(DateTime, server_default=func.now(), onupdate=func.now())
    
    # Relationships
    user = relationship("User", back_populates="progress_records")


class Resource(Base):
    __tablename__ = "resources"
    
    id = Column(String, primary_key=True, index=True)
    title = Column(String)
    url = Column(String)
    type = Column(String)
    description = Column(Text)
    metadata = Column(JSONB)  # Additional metadata about the resource
    created_at = Column(DateTime, server_default=func.now())
    updated_at = Column(DateTime, server_default=func.now(), onupdate=func.now())
```

### Database Session Configuration

```python
# backend/app/db/session.py
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
from app.core.config import settings

# Create database engine
engine = create_engine(
    settings.SQLALCHEMY_DATABASE_URI,
    pool_pre_ping=True  # Check if connection is still valid before using it
)

# Create sessionmaker
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

# Create base class for models
Base = declarative_base()

# Dependency to get DB session
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

## Deployment Configuration

### Docker Configuration for Backend

```dockerfile
# backend/Dockerfile
FROM python:3.9-slim

WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Set environment variables
ENV PYTHONPATH=/app
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Expose port
EXPOSE 8000

# Command to run the application
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Docker Configuration for Frontend

```dockerfile
# frontend/Dockerfile
FROM node:16-alpine

WORKDIR /app

# Install dependencies
COPY package.json package-lock.json ./
RUN npm ci

# Copy application code
COPY . .

# Build the application
RUN npm run build

# Expose port
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]
```

### Docker Compose Configuration

```yaml
# docker-compose.yml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://postgres:postgres@db:5432/learningpath
      - OPENAI_API_KEY=${OPENAI_API_KEY}
      - PERPLEXITY_API_KEY=${PERPLEXITY_API_KEY}
    depends_on:
      - db
    volumes:
      - ./backend:/app
    restart: always

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_API_URL=http://localhost:8000
    volumes:
      - ./frontend:/app
    restart: always

  db:
    image: postgres:13
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_DB=learningpath
    ports:
      - "5432:5432"

volumes:
  postgres_data:
```

### GitHub Actions Workflow

```yaml
# .github/workflows/ci-cd.yml
name: CI/CD Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.9'
    
    - name: Install backend dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r backend/requirements.txt
        pip install pytest pytest-asyncio
    
    - name: Run backend tests
      run: |
        cd backend
        pytest
    
    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '16'
    
    - name: Install frontend dependencies
      run: |
        cd frontend
        npm ci
    
    - name: Run frontend tests
      run: |
        cd frontend
        npm test

  build:
    needs: test
    runs-on: ubuntu-latest
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Build and push backend Docker image
      uses: docker/build-push-action@v2
      with:
        context: ./backend
        push: false
        tags: learningpath-backend:latest
    
    - name: Build and push frontend Docker image
      uses: docker/build-push-action@v2
      with:
        context: ./frontend
        push: false
        tags: learningpath-frontend:latest