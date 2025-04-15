# Jenkins and Docker Pipeline Documentation

## Overview
This repository contains a Jenkins pipeline configuration for automating the build and deployment process using Docker. The pipeline clones the repository, builds a Docker image, and pushes it to Docker Hub.

## Prerequisites
- Jenkins server installed and configured with Docker: 
    docker run -d --name jenkins --restart=unless-stopped -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts
- Install Ngrok with Docker with port 8080 to map with Jenkins
- Docker installed on Jenkins server
- Docker Hub account
- GitHub repository access
- Jenkins plugins:
  - Git plugin
  - Docker Pipeline plugin
  - Docker plugin
  - Credentials plugin

## Pipeline Flow

### 1. Repository Setup
- Create a GitHub repository
- Add application source code
- Add Jenkinsfile for pipeline configuration
### 1. Repository Setup
- Create a GitHub repository
- Add application source code
- Add Jenkinsfile for pipeline configuration
- Configure GitHub webhook with Ngrok:
  1. Get Ngrok public URL (e.g., https://xxxx-xx-xxx-xxx-xx.ngrok.io)
  2. Go to GitHub repository > Settings > Webhooks
  3. Add webhook:
     - Payload URL: [Ngrok URL]/github-webhook/
     - Content type: application/json
     - Secret: (Optional) Set webhook secret
     - Events: Select "Just the push event"
  4. Verify webhook connection is active
### 1.1 GitHub Personal Access Token Setup
- Go to GitHub > Settings > Developer settings
- Select "Personal access tokens (classic)"
- Click "Generate new token (classic)"
- Set token name and expiration
- Select scopes:
  - repo (Full control of private repositories)
  - workflow (Update GitHub Action workflows)
- Copy and save the generated token securely
- Use this token as the password when setting up GitHub credentials in Jenkins

### 2. Jenkins Configuration
#### 2.1 Credentials Setup
- Add GitHub credentials in Jenkins
  - Go to Jenkins > Manage Jenkins > Credentials
  - Add GitHub credentials with ID: '1highbar45'
- Add Docker Hub credentials
  - Go to Jenkins > Manage Jenkins > Credentials
  - Add Docker Hub credentials with ID: 'cred-docker-hub'

#### 2.2 Pipeline Setup
- Create new Pipeline job in Jenkins
- Configure pipeline to use SCM
- Specify repository URL and credentials
- Set branch to 'main'

### 3. Pipeline Stages

#### Stage 1: Clone
- Pipeline clones the repository from GitHub
- Uses specified credentials
- Checks out the main branch

#### Stage 2: Docker
- Authenticates with Docker Hub
- Builds Docker image from Dockerfile
- Tags image as 'sigmaduck125/my-website'
- Pushes image to Docker Hub repository

## Usage

### Running the Pipeline
1. Access Jenkins dashboard
2. Navigate to your pipeline project
3. Click "Build Now"

### Monitoring
- View build progress in Jenkins console output
- Check build status and logs
- Verify Docker image in Docker Hub repository

## Troubleshooting

### Common Issues
1. Git clone fails
   - Verify GitHub credentials
   - Check repository URL and permissions

2. Docker build fails
   - Ensure Dockerfile exists in repository root
   - Check Docker daemon status
   - Verify Docker commands permissions

3. Docker push fails
   - Verify Docker Hub credentials
   - Check network connectivity
   - Ensure proper image tagging

## Additional Resources
- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)