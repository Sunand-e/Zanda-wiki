### Overview of the Docker Setup

This project uses **docker-compose** to containerise the application and its dependencies for development.

#### 1. [docker-compose.yml](https://github.com/eLearning-Plus/MemberHub/blob/main/docker-compose.yml)

The docker-compose.yml file defines the services required for the application, including Rails, PostgreSQL, Nginx, Redis, and Mailhog. It also specifies the environment variables, volumes, and network configuration used. A `.env` file is used to provide the environment variables (see [.env.example](https://github.com/eLearning-Plus/MemberHub/blob/main/.env.example))

#### 2. [Dockerfile](https://github.com/eLearning-Plus/MemberHub/blob/main/Dockerfile)

The [Dockerfile for the Rails application](https://github.com/eLearning-Plus/MemberHub/blob/main/Dockerfile) defines the base image, installs dependencies, and sets up the application directory.

#### 3. [Dockerfile](https://github.com/eLearning-Plus/MemberHub/blob/main/docker/nginx/Dockerfile) for Nginx

The [Dockerfile for Nginx](https://github.com/eLearning-Plus/MemberHub/blob/main/docker/nginx/Dockerfile) sets up the Nginx server, installs necessary packages, and configures the server to serve the Rails application.

### Detailed Overview of Each Service

#### Rails Service

*   **Container Name**: rails
    
*   **Build Context**: Current directory (.)
    
*   **Volumes**: Mounts the current directory to [app](vscode-file://vscode-app/c:/Users/Mark/AppData/Local/Programs/Microsoft VS Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) inside the container.
    
*   **Depends On**: [db](vscode-file://vscode-app/c:/Users/Mark/AppData/Local/Programs/Microsoft VS Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) service.
    
*   **Command**: Removes any existing server PID file, runs database migrations, and starts the Rails server.
    
*   **Environment Variables**: Includes various environment variables for database configuration, SMTP settings, AWS S3 settings, and Redis configuration.
    
*   **Networks**: Connected to the back network.
    

#### PostgreSQL Service

*   **Container Name**: postgres-db
    
*   **Image**: postgres:latest
    
*   **Environment Variables**: Includes PostgreSQL user, password, and database name.
    
*   **Volumes**: Mounts a Docker volume to persist PostgreSQL data.
    
*   **Ports**: Exposes port 5432.
    
*   **Networks**: Connected to the back network.
    

#### Nginx Service

*   **Container Name**: nginx
    
*   **Build Context**: [nginx](vscode-file://vscode-app/c:/Users/Mark/AppData/Local/Programs/Microsoft VS Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)
    
*   **Depends On**: rails service.
    
*   **Volumes**: Mounts the frontend directory to /app/public and logs directory to /app/log.
    
*   **Ports**: Exposes port 80.
    
*   **Networks**: Connected to the back and shared networks.
    

#### Mailhog Service

*   **Container Name**: mailhog
    
*   **Image**: mailhog/mailhog:latest
    
*   **Ports**: Exposes ports 1025 and 8025.
    
*   **Networks**: Connected to the back and shared networks.
    

#### Redis Service

*   **Container Name**: redis
    
*   **Image**: redis:latest
    
*   **Environment Variables**: Sets the timezone to UTC.
    
*   **Ports**: Exposes port 6379.
    
*   **Networks**: Connected to the back network.
    

### Networks

*   **back**: An internal network for communication between the Rails, PostgreSQL, Nginx, Mailhog, and Redis services.
    
*   **shared**: An external network for communication between services that need to be accessible from outside the Docker setup.
    

### Volumes

*   **db**: A Docker volume to persist PostgreSQL data.
    

### Summary

This Docker setup provides a robust environment for developing and running the Rails application. It includes services for the Rails application, PostgreSQL database, Nginx web server, Redis cache, and Mailhog for email testing. Each service is configured with the necessary environment variables, volumes, and network settings to ensure seamless communication and data persistence.