---
title: Docker Three Tier Architecture
---

# Hello World

## Three-Tier Application Deployment using Dockerfile

### Prerequisites

Before you begin, ensure that you have the following installed:

- Docker

### Project Structure

- backend: Node.js application serving as the backend.
- frontend: React.js application for the frontend.
- mysql: Dockerfile and configurations for the MySQL database.

#### Dockerfile(Database)
![Database Dockerfile](INSERT_DATABASE_DOCKERFILE_IMAGE_URL_HERE)

#### Dockerfile(Backend)
![Backend Dockerfile](INSERT_BACKEND_DOCKERFILE_IMAGE_URL_HERE)

#### Dockerfile(Frontend)
![Frontend Dockerfile](INSERT_FRONTEND_DOCKERFILE_IMAGE_URL_HERE)

### Deployment Steps

1. **Create Network**
   ```bash
   docker network create three-tier-network


2. **MySQL Database:**

- Navigate to the mysql directory.
- Build the MySQL Docker image:
  ```
  docker build -t mysql-image .
  ```

- Run the MySQL container:
  ```
  docker run --name mysql-container --network=three-tier-network -p 3306:3306 -v mysql-data:/var/lib/mysql -d mysql-image
  ```

- Access the MySQL container:
  ```
  docker exec -it mysql-container /bin/bash
  ```

3. **Backend Application:**

- Navigate to the backend directory.
- Build the backend Docker image:
  ```
  docker build -t backend .
  ```

- Run the backend container:
  ```
  docker run -d -p 3500:3500 --name backend-container --network=three-tier-network backend
  ```

4. **Frontend Application:**

- Navigate to the frontend directory.
- Build the frontend Docker image:
  ```
  docker build -t frontend .
  ```

- Run the frontend container:
  ```
  docker run -d --name frontend-container --network=three-tier-network -p 80:80 frontend
  ```

### Access the Application:

Open your favorite browser and visit http://localhost:80. Enjoy exploring the MERN stack application!

### Data Persistence

Data persistence is ensured by using Docker volumes. If the MySQL container is deleted, data remains available and is automatically added to a new Docker container by providing the same Docker volume.

Feel free to explore and modify the Dockerfiles to enhance your understanding of containerization and deployment! Happy coding! 🚀

Written on March 3, 2014
