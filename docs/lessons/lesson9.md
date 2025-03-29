# Lesson 9: Project Deployment and Automation

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Use Roocode to generate and automate deployment scripts
- Create Docker containers for applications
- Implement CI/CD workflows with AI assistance
- Automate repetitive deployment tasks
- Troubleshoot common deployment issues
- Apply best practices for secure and reliable deployments

## 📚 Lesson Content

### 1. Introduction to Deployment Automation via Roocode

Deployment is another area where AI can streamline development:

#### Benefits of AI-Assisted Deployment

1. **Consistent configurations**: Generating standardized deployment files
2. **Reduced human error**: Eliminating manual steps and typos
3. **Documentation generation**: Automatically creating deployment guides
4. **Best practice implementation**: Incorporating security and performance optimizations
5. **Cross-platform compatibility**: Handling multiple deployment targets

#### The Role of Roocode in Deployment

Roocode can help with:
- Generating configuration files (Docker, Kubernetes, cloud providers)
- Creating build and deployment scripts
- Setting up monitoring and logging
- Implementing security best practices
- Troubleshooting deployment issues

### 2. Example: Creating Dockerfiles via Roocode Prompts

Containerization is a key deployment strategy that Roocode can assist with:

#### Dockerfile Generation

```
I have a Node.js application with the following structure:
- src/: Contains the source code
- package.json: Dependencies and scripts
- tsconfig.json: TypeScript configuration
- .env.example: Environment variable template

The application uses:
- Node.js 18
- Express for the server
- MongoDB for the database
- TypeScript
- pm2 for process management

Please create a Dockerfile that:
1. Uses an appropriate base image
2. Installs dependencies
3. Builds the TypeScript code
4. Sets up proper environment variables
5. Exposes the necessary port (3000)
6. Implements security best practices
7. Optimizes for build time and image size
```

#### Example Generated Dockerfile

```dockerfile
# Stage 1: Build
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm ci

# Copy source files
COPY tsconfig.json ./
COPY src/ ./src/

# Build the application
RUN npm run build

# Remove development dependencies
RUN npm prune --production

# Stage 2: Runtime
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Set node environment to production
ENV NODE_ENV=production

# Create a non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Copy built application from builder stage
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package.json ./

# Copy environment variable example (will be overridden at runtime)
COPY .env.example ./.env

# Install pm2 globally
RUN npm install -g pm2

# Expose application port
EXPOSE 3000

# Change to non-root user
USER appuser

# Start the application with pm2
CMD ["pm2-runtime", "dist/index.js"]
```

### 3. Running Deployment Scripts with Roocode Terminal Commands

Roocode can help execute and automate deployment tasks:

#### Terminal Command Execution Workflow

1. **Generate the deployment script**: Have Roocode create the script
2. **Review for security and correctness**: Manually verify sensitive operations
3. **Execute via Roocode**: Let Roocode run the commands
4. **Monitor and capture output**: Use Roocode to analyze results
5. **Troubleshoot if needed**: Leverage AI for error interpretation

#### Example: Deployment Script Generation and Execution

```
Create a deployment script for our Docker container that:
1. Builds the image with proper tagging
2. Runs required tests before deployment
3. Logs in to our container registry
4. Pushes the image to the registry
5. Updates our staging environment
6. Performs a health check
```

**Generated Script:**
```bash
#!/bin/bash
set -e

# Configuration
IMAGE_NAME="myapp"
REGISTRY="registry.example.com"
TAG=$(git rev-parse --short HEAD)  # Use git commit hash as tag
FULL_IMAGE_NAME="$REGISTRY/$IMAGE_NAME:$TAG"
STAGING_SERVER="staging.example.com"

echo "🚀 Starting deployment process..."

# Build Docker image
echo "🔨 Building Docker image..."
docker build -t $FULL_IMAGE_NAME .

# Run tests
echo "🧪 Running tests..."
docker run --rm $FULL_IMAGE_NAME npm test

# Log in to registry
echo "🔑 Logging in to container registry..."
docker login $REGISTRY -u $REGISTRY_USER -p $REGISTRY_PASSWORD

# Push image to registry
echo "⬆️ Pushing image to registry..."
docker push $FULL_IMAGE_NAME

# Deploy to staging
echo "🚀 Deploying to staging environment..."
ssh deploy@$STAGING_SERVER "docker pull $FULL_IMAGE_NAME && \
  docker-compose down && \
  echo 'DOCKER_IMAGE=$FULL_IMAGE_NAME' > .env && \
  docker-compose up -d"

# Health check
echo "🔍 Performing health check..."
sleep 10  # Wait for service to start
HEALTH_STATUS=$(curl -s -o /dev/null -w "%{http_code}" https://$STAGING_SERVER/health)

if [ $HEALTH_STATUS -eq 200 ]; then
  echo "✅ Deployment successful! Health check passed."
else
  echo "❌ Health check failed with status $HEALTH_STATUS. Rolling back..."
  ssh deploy@$STAGING_SERVER "docker-compose down && docker-compose up -d --no-deps web-previous"
  exit 1
fi

echo "🎉 Deployment to staging complete!"
```

#### Executing the Script with Roocode

```
Let's run this deployment script, but first:
1. Let's add proper error handling
2. Make it safe to run (validate environment variables are set)
3. Add a prompt for confirmation before pushing to registry
```

### 4. Demo: Deploying a Project Locally and Remotely

Let's walk through a complete deployment for a web application:

#### Local Deployment with Docker Compose

**Step 1: Generate Docker Compose file**

```
Create a docker-compose.yml file for our MERN stack application with:
1. Node.js backend service
2. MongoDB database service
3. React frontend service
4. Nginx for serving the frontend and routing API requests
5. Proper networking between services
6. Volume mounts for persistence
7. Environment variable configuration
```

**Step 2: Set up local environment**

```
Generate a script that sets up our local development environment:
1. Create necessary .env files
2. Initialize the database with sample data
3. Build necessary Docker images
4. Start the services with docker-compose
```

**Step 3: Test the local deployment**

```
Create a test script that:
1. Checks if all services are running
2. Verifies connectivity between services
3. Runs basic API endpoint tests
4. Validates database connectivity
```

#### Remote Deployment to Cloud Provider

**Step 1: Generate cloud configuration**

```
Create an AWS CloudFormation template for deploying our application with:
1. EC2 instances for our application
2. Load balancer for traffic distribution
3. RDS for managed database
4. S3 bucket for static assets
5. IAM roles with least privilege
6. Security groups with proper access rules
```

**Step 2: Set up CI/CD pipeline**

```
Create a GitHub Actions workflow file that:
1. Builds and tests the application on each push
2. Deploys to staging on merges to develop branch
3. Deploys to production on merges to main branch
4. Includes approval steps for production deployment
5. Sends notifications on deployment events
```

**Step 3: Generate deployment documentation**

```
Create comprehensive deployment documentation that covers:
1. Architecture overview
2. Environment setup instructions
3. Deployment process step-by-step
4. Rollback procedures
5. Monitoring and logging
6. Troubleshooting common issues
```

### 5. Exercise: Deploy a Mini-Project (Web App/Service)

Practice by deploying a simple web application:

#### Project: URL Shortener Service

**Requirements:**
- Node.js Express backend with MongoDB
- Simple React frontend
- Redis for caching
- Dockerized for easy deployment
- CI/CD pipeline with GitHub Actions

**Step 1: Set up the project structure**

```
Help me create the basic structure for a URL shortener service with:
1. Express backend with MongoDB connection
2. React frontend with form for submitting URLs
3. API endpoints for creating and redirecting short URLs
4. Docker configuration for all components
```

**Step 2: Implement core functionality**

```
Help me implement the core functionality:
1. URL shortening algorithm
2. Database schema for storing mappings
3. Redis caching for popular URLs
4. API endpoints for creating and retrieving URLs
```

**Step 3: Create deployment configuration**

```
Create deployment files for:
1. Docker Compose for local development
2. Kubernetes manifests for production
3. GitHub Actions workflow for CI/CD
4. Environment configuration templates
```

**Step 4: Generate deployment script**

```
Create a deployment script that:
1. Builds the application images
2. Runs tests before deployment
3. Pushes images to a registry
4. Deploys to Kubernetes cluster
5. Performs health checks after deployment
```

### 6. Troubleshooting Deployment Errors Using Roocode

AI can be a valuable resource for diagnosing deployment issues:

#### Common Deployment Errors and Solutions

1. **Container startup failures**
   - Missing dependencies
   - Incorrect environment variables
   - Permission issues
   - Port conflicts

2. **Network connectivity issues**
   - Misconfigured networking
   - Incorrect DNS settings
   - Firewall rules blocking traffic
   - Service discovery problems

3. **Resource limitations**
   - Insufficient memory or CPU
   - Disk space exhaustion
   - Database connection limits
   - Rate limiting errors

#### Example: Troubleshooting Docker Deployment

```
I'm getting this error when trying to deploy my Docker container:

```
standard_init_linux.go:228: exec user process caused: exec format error
```

Here's my Dockerfile:
```dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["node", "dist/server.js"]
```

I'm building on a Mac with M1 chip and deploying to a Linux server. What could be causing this issue?
```

### 7. Automating Repetitive Tasks with AI Scripting

Identify and automate routine deployment tasks:

#### Tasks Suitable for Automation

1. **Environment setup**: Creating and configuring environments
2. **Dependency management**: Updating and auditing dependencies
3. **Build processes**: Compiling, transpiling, and bundling
4. **Testing**: Running test suites and reporting results
5. **Deployment**: Releasing to various environments
6. **Monitoring**: Checking service health and metrics

#### Example: Automation Script for Database Migration

```
Create a script that automates our database migration process:

Current steps (manual):
1. Take a database backup
2. Run migration scripts
3. Verify data integrity
4. Update application version
5. Roll back if issues are detected

The script should:
1. Handle error cases automatically
2. Log detailed information
3. Send notifications on completion or failure
4. Include a dry-run option
```

**Generated Script:**

```bash
#!/bin/bash
set -eo pipefail

# Configuration
DB_NAME="myapp"
DB_USER="dbuser"
DB_HOST="localhost"
MIGRATIONS_PATH="./migrations"
BACKUP_DIR="./backups"
APP_VERSION_FILE="./version.json"
SLACK_WEBHOOK="https://hooks.slack.com/services/TXXXX/BXXXX/XXXXXX"
DRY_RUN=false

# Parse arguments
while getopts "d" opt; do
  case $opt in
    d) DRY_RUN=true ;;
    \?) echo "Invalid option -$OPTARG" >&2; exit 1 ;;
  esac
done

# Functions
function log_info() {
    echo "ℹ️ [INFO] $1"
    if [ "$DRY_RUN" = false ]; then
        log_to_slack "INFO: $1"
    fi
}

function log_error() {
    echo "❌ [ERROR] $1" >&2
    if [ "$DRY_RUN" = false ]; then
        log_to_slack "ERROR: $1"
    fi
}

function log_success() {
    echo "✅ [SUCCESS] $1"
    if [ "$DRY_RUN" = false ]; then
        log_to_slack "SUCCESS: $1"
    fi
}

function log_to_slack() {
    curl -s -X POST -H 'Content-type: application/json' \
        --data "{\"text\":\"$1\"}" \
        $SLACK_WEBHOOK || true
}

function take_backup() {
    local timestamp=$(date +"%Y%m%d_%H%M%S")
    local backup_file="$BACKUP_DIR/${DB_NAME}_${timestamp}.sql"
    
    mkdir -p $BACKUP_DIR
    
    log_info "Taking database backup to $backup_file"
    if [ "$DRY_RUN" = false ]; then
        pg_dump -h $DB_HOST -U $DB_USER -d $DB_NAME -f $backup_file || return 1
    fi
    
    echo $backup_file
}

function run_migrations() {
    log_info "Running database migrations from $MIGRATIONS_PATH"
    if [ "$DRY_RUN" = false ]; then
        # Example using a hypothetical migration tool
        db-migrate up || return 1
    fi
}

function verify_data() {
    log_info "Verifying data integrity"
    if [ "$DRY_RUN" = false ]; then
        # Run verification queries or scripts
        psql -h $DB_HOST -U $DB_USER -d $DB_NAME -c "SELECT count(*) FROM users;" > /dev/null || return 1
        psql -h $DB_HOST -U $DB_USER -d $DB_NAME -c "SELECT count(*) FROM products;" > /dev/null || return 1
    fi
}

function update_version() {
    local new_version=$1
    log_info "Updating application version to $new_version"
    if [ "$DRY_RUN" = false ]; then
        echo "{\"version\": \"$new_version\", \"migratedAt\": \"$(date -u +"%Y-%m-%dT%H:%M:%SZ")\"}" > $APP_VERSION_FILE
    fi
}

function rollback() {
    local backup_file=$1
    log_error "Rolling back to backup: $backup_file"
    if [ "$DRY_RUN" = false ]; then
        psql -h $DB_HOST -U $DB_USER -d $DB_NAME < $backup_file
    fi
}

# Main execution
if [ "$DRY_RUN" = true ]; then
    log_info "Running in DRY RUN mode. No changes will be made."
fi

log_info "Starting database migration process"

# Read the current app version
if [ -f $APP_VERSION_FILE ]; then
    CURRENT_VERSION=$(cat $APP_VERSION_FILE | jq -r '.version')
else
    CURRENT_VERSION="0.0.0"
fi

# Calculate new version (example logic)
NEW_VERSION=$(echo $CURRENT_VERSION | awk -F. '{$NF = $NF + 1;} 1' | sed 's/ /./g')

# Take backup
BACKUP_FILE=$(take_backup)
if [ $? -ne 0 ]; then
    log_error "Backup failed. Aborting migration."
    exit 1
fi

# Run migrations with error handling
if ! run_migrations; then
    log_error "Migration failed. Rolling back."
    rollback $BACKUP_FILE
    exit 1
fi

# Verify data integrity
if ! verify_data; then
    log_error "Data verification failed. Rolling back."
    rollback $BACKUP_FILE
    exit 1
fi

# Update application version
update_version $NEW_VERSION

log_success "Migration completed successfully! New version: $NEW_VERSION"
exit 0
```

### 8. Advanced Example: CI/CD Pipeline Prompts via Roocode

Creating sophisticated CI/CD pipelines with AI assistance:

#### GitHub Actions Workflow for Full CI/CD

```
Create a GitHub Actions workflow for our Node.js application that:

1. Runs on pushes to develop and main branches, and pull requests
2. Sets up Node.js environment and caches dependencies
3. Installs dependencies with npm ci
4. Runs linting, type checking, and unit tests
5. Builds the application
6. Runs integration tests against the build
7. Builds and pushes Docker image on successful tests
8. Deploys to staging for develop branch changes
9. Requires manual approval for production deployment
10. Deploys to production for main branch with approval
11. Sends notifications on success/failure
```

**Generated Workflow:**

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [develop, main]
  pull_request:
    branches: [develop, main]

jobs:
  test:
    name: Test
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Lint code
        run: npm run lint
      
      - name: Type check
        run: npm run type-check
      
      - name: Run unit tests
        run: npm run test:unit
      
      - name: Build application
        run: npm run build
      
      - name: Run integration tests
        run: npm run test:integration
  
  build-and-push:
    name: Build and Push Docker image
    needs: test
    if: github.event_name == 'push' && (github.ref == 'refs/heads/develop' || github.ref == 'refs/heads/main')
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      
      - name: Login to GitHub Container Registry
        uses: docker/login-action@v2
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      
      - name: Extract metadata for Docker
        id: meta
        uses: docker/metadata-action@v4
        with:
          images: ghcr.io/${{ github.repository }}
          tags: |
            type=sha,format=short
            type=ref,event=branch
      
      - name: Build and push Docker image
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
          cache-from: type=gha
          cache-to: type=gha,mode=max
  
  deploy-staging:
    name: Deploy to Staging
    needs: build-and-push
    if: github.ref == 'refs/heads/develop'
    runs-on: ubuntu-latest
    environment: staging
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Setup kubectl
        uses: azure/setup-kubectl@v3
      
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-west-2
      
      - name: Update kubeconfig
        run: aws eks update-kubeconfig --name staging-cluster --region us-west-2
      
      - name: Deploy to staging
        run: |
          IMAGE_TAG=$(echo $GITHUB_SHA | cut -c1-7)
          sed -i "s|IMAGE_TAG|$IMAGE_TAG|g" k8s/staging/deployment.yaml
          kubectl apply -f k8s/staging/
      
      - name: Verify deployment
        run: |
          kubectl rollout status deployment/myapp -n staging
      
      - name: Send notification
        uses: rtCamp/action-slack-notify@v2
        env:
          SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
          SLACK_TITLE: "Staging Deployment"
          SLACK_MESSAGE: "Successfully deployed to staging environment"
  
  deploy-production:
    name: Deploy to Production
    needs: build-and-push
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment:
      name: production
      url: https://example.com
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Setup kubectl
        uses: azure/setup-kubectl@v3
      
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-west-2
      
      - name: Update kubeconfig
        run: aws eks update-kubeconfig --name production-cluster --region us-west-2
      
      - name: Deploy to production
        run: |
          IMAGE_TAG=$(echo $GITHUB_SHA | cut -c1-7)
          sed -i "s|IMAGE_TAG|$IMAGE_TAG|g" k8s/production/deployment.yaml
          kubectl apply -f k8s/production/
      
      - name: Verify deployment
        run: |
          kubectl rollout status deployment/myapp -n production
      
      - name: Send notification
        uses: rtCamp/action-slack-notify@v2
        env:
          SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
          SLACK_TITLE: "Production Deployment"
          SLACK_MESSAGE: "Successfully deployed to production environment"
```

### 9. Common Deployment Best Practices (Security/Performance)

Ensuring robust deployments with AI assistance:

#### Security Best Practices

1. **Least privilege principle**: Minimize permissions for services
2. **Secret management**: Use secure methods for handling credentials
3. **Container security**: Scan images for vulnerabilities
4. **Network segmentation**: Restrict communication between services
5. **Immutable infrastructure**: Deploy fresh instead of modifying

#### Performance Optimization

1. **Resource sizing**: Right-size container resources
2. **Caching strategies**: Implement appropriate caching
3. **Database optimization**: Tune database for workload
4. **Load balancing**: Distribute traffic effectively
5. **Auto-scaling**: Scale resources based on demand

#### Example: Generating Security Recommendations

```
Review our Kubernetes deployment configuration for security issues:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-web-app
  namespace: default
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-web-app
  template:
    metadata:
      labels:
        app: my-web-app
    spec:
      containers:
      - name: web-app
        image: myregistry/my-web-app:latest
        ports:
        - containerPort: 3000
        env:
        - name: DB_PASSWORD
          value: "password123"
        - name: API_KEY
          value: "1a2b3c4d5e"
        resources:
          limits:
            memory: "512Mi"
            cpu: "500m"
          requests:
            memory: "256Mi"
            cpu: "250m"
        securityContext: {}
```

### 10. Limitations and Considerations for Automated Deployments

Understand when to rely on AI and when to use human judgment:

#### AI Deployment Limitations

1. **Security-sensitive operations**: Requires human review
2. **Complex environment-specific issues**: Needs domain knowledge
3. **Custom integration points**: May need manual configuration
4. **Unpredictable failures**: Requires human troubleshooting
5. **Compliance requirements**: Human verification often needed

#### Balancing Automation and Control

1. **Plan for approval steps**: Integrate manual approvals for critical changes
2. **Implement progressive deployment**: Gradual rollout with monitoring
3. **Design for rollbacks**: Always have a way to revert changes
4. **Comprehensive testing**: Test automation itself thoroughly
5. **Visibility and logging**: Ensure all automated actions are well-documented

#### Example: Creating a Safe Deployment Strategy

```
Design a deployment strategy for our financial application that balances automation with necessary human oversight. Consider:
1. Security requirements for financial data
2. Compliance with regulations
3. Minimizing downtime for customers
4. Data integrity protection
5. Disaster recovery capabilities
```

## 🎯 Practice Exercises

1. **Containerization**
   - Take an existing application
   - Create a Dockerfile for it
   - Implement multi-stage builds
   - Optimize for security and size

2. **CI/CD Pipeline**
   - Create a GitHub Actions workflow
   - Include testing and deployment steps
   - Implement approval gates
   - Add notifications for key events

3. **Deployment Script**
   - Create a deployment script for a specific platform
   - Include error handling
   - Implement rollback capability
   - Add logging and monitoring hooks

## 📝 Lesson Summary

Key takeaways:

- Roocode can automate many aspects of deployment
- Containerization provides consistency across environments
- CI/CD pipelines ensure quality and reliability
- Automated scripts save time and reduce errors
- Security best practices should be built into deployment
- Balance automation with appropriate human oversight

## 🚀 Next Steps

1. Complete the practice exercises
2. Apply deployment automation to your own projects
3. Create a deployment checklist for your team
4. Prepare for Lesson 10: Capstone Project & Best Practices

## 📚 Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Patterns](https://www.oreilly.com/library/view/kubernetes-patterns/9781492050278/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Secure by Design](https://www.manning.com/books/secure-by-design) 