# Docker Templates Repository

## Overview
This repository contains a collection of Dockerfile templates and related configurations for various development environments and projects. These templates are designed to provide robust, secure, and efficient containerization solutions.


## Key Features
  - Multi-stage build for optimal image size
  - Non-root user for enhanced security
  - Configurable environment settings

## Templates Available

### .NET Project Dockerfile Templates
- **Monolithic**

### Others
- **Jenkins**

## How to Use

1. **Select Appropriate Template**
   - Choose the template that matches your project's technology stack
   - Copy the Dockerfile to your project directory

2. **Customize the Template**
   - Replace placeholders like `ProjectName`
   - Adjust ports, environment variables, and health check endpoints
   - Update metadata labels

3. **Build Your Docker Image**
   ```bash
   docker build -t image-name .
   ```

## Best Practices

- Always test your Dockerfile locally before deployment
- Use `.dockerignore` to exclude unnecessary files
- Keep security considerations in mind
- Regularly update base images to get latest security patches

