# Art Gallery Platform

## Project Concept

This project focuses on developing a scalable online platform for an art gallery. The application integrates a reliable backend and a dynamic frontend. The backend manages user authentication, artwork inventory, and order processing for prints or original art, while the frontend provides a seamless and engaging user experience for exploring and purchasing artworks. Additionally, caching mechanisms are employed to enhance performance, ensuring a robust and efficient user experience.

## Project Overview

This project is structured into three primary components: backend services (RDS and Redis), and the frontend. Each component plays a critical role in delivering a comprehensive solution. Below is a summary of the key elements:

- **Backend (RDS)**: Built with a focus on scalability and reliability, managing relational database operations for artworks, artists, and user data.
- **Backend (Redis)**: Optimized for session caching and quick access to frequently viewed artwork or user data.
- **Frontend**: Designed to provide a dynamic and interactive user interface for users to browse art collections and make purchases.

The platform utilizes PostgreSQL for database management and Redis for caching, ensuring optimal performance.


## File Structure

### 1. **Backend (RDS)**
- **Purpose**: Manages application logic and integrates with a relational database service.
- **Files**:
  - `manage.py`: Entry point for the backend application.
  - `requirements.txt`: Lists dependencies for the project.
  - `backend_rds/`: Contains the core backend logic, configuration files, and routes for the application.

### 2. **Backend (Redis)**
- **Purpose**: Handles backend logic with Redis for caching.
- **Files**:
  - `manage.py`: Entry point for the backend application.
  - `requirements.txt`: Lists dependencies for the project.
  - `backend_redis/`: Contains the core backend logic, configuration files, and routes for the application.

### 3. **Frontend**
- **Purpose**: Provides the user interface.
- **Files**:
  - `manage.py`: Entry point for the frontend application.
  - `requirements.txt`: Lists frontend dependencies.
  - `frontend/`: Contains configuration files, routing, views, and templates for the frontend interface.

## Deployment Flow

### Local Testing

- Follow the steps in **Local Testing** to set up and validate the application locally using Docker Compose.

### Step 1: Deploying the Basic Architecture

- Deploy the backend services on ECS instances in a private subnet as described in **Step 1: Deploying the Basic Architecture**.

### Step 2: Introducing Load Balancing

- Set up an Application Load Balancer (ALB) as outlined in **Step 2: Introducing Load Balancing** to distribute traffic across multiple backend instances.

### Step 3: Incorporating Databases and Caching

- Implement secure database and caching services using RDS and ElastiCache in a private subnet as described in **Step 3: Incorporating Databases and Caching**.

### CI/CD Process

- Implement separate CI/CD pipelines for backend and frontend deployment to automate the process effectively.

## Local Testing

### Step 1: Cloning the Repository
Clone the repository to your local machine and navigate to the project directory:
```bash
git clone https://github.com/NazarPry/Art-gallery.git
cd art-gallery
```

### Step 2: Writing Dockerfiles for Services
Write a `Dockerfile` for each service, including:
- Backend RDS
- Backend Redis
- Frontend

Ensure each `Dockerfile` is properly configured to build and run its respective service.

### Step 3: Creating `docker-compose.yml` and Environment Variables
Write a `docker-compose.yml` file to define all the services, including Redis, PostgreSQL, and backend services. Include the following:
- **Redis**: Use the official Redis image ([Redis Docker Hub](https://hub.docker.com/_/redis)).
- **PostgreSQL**: Use the official PostgreSQL image ([PostgreSQL Docker Hub](https://hub.docker.com/_/postgres)).
- **backend-rds**: This service should depend on PostgreSQL.
- **backend-redis**: This service should depend on Redis.
- **Frontend**: Use the frontend Dockerfile built.

***Make sure to place the corresponding `Dockerfile` for each backend service in the correct directory.***

### Step 4: Building and Running Services
Build and start all services using Docker Compose with the `--build` option to rebuild images:
```bash
docker-compose up -d --build
```

### Step 5: Monitoring Logs
To troubleshoot issues and monitor logs for each service:
- View logs for all services:
  ```bash
  docker-compose logs -f
  ```
- View logs for a specific service (e.g., backend-rds):
  ```bash
  docker-compose logs -f backend-rds
  ```
- Stop monitoring logs by pressing `Ctrl+C`.

### Step 6: Testing the Frontend
After starting all services, verify that the frontend served by Nginx is accessible.

### Step 7: Stopping Services
To stop all running services:
```bash
docker-compose down
```

## AWS Deployment

### Step 1: Deploying the Frontend

![Architecture Diagram Step 1](docs/assets/diagram-step1.png)

In the first step, deploy the frontend application with a simple setup:

- Launch an ECS cluster in a **private subnet** for hosting the frontend service.
- Use **Amazon ECR** for managing container images.
- Run the ECS task with the proper image.

### Step 2: Introducing Load Balancing

![Architecture Diagram Step 2](docs/assets/diagram-step2.png)

In the second step, enhance scalability and availability:

- Add an **Application Load Balancer (ALB)** in the **public subnet** to distribute traffic to the frontend service.

### Step 3: Incorporating Backend Services

![Architecture Diagram Step 3](docs/assets/diagram-step3.png)

In the final step, integrate data storage and backend functionality:

- Deploy **RDS** and **ElastiCache (Redis)** in **private subnets** for secure database and caching operations.
- Configure the backend services to work seamlessly with the frontend.


## CI/CD Process

Setting up a CI/CD pipeline is essential for automating the build, test, and deployment processes. You can choose to use either **GitHub Actions** or **GitLab CI/CD** based on your preference. Here are the general steps:

1. **Pipeline Configuration**:
   - Define a pipeline in GitHub Actions or in GitLab CI/CD.
   - Include stages for building Docker images, running tests, and deploying to AWS.

2. **Docker Integration**:
   - Configure the pipeline to build and push Docker images to Amazon ECR.

3. **Environment Variables**:
   - Store sensitive data, such as AWS credentials, database connection strings, and API keys, securely within the CI/CD platform.

4. **Testing**:
   - Add automated tests to validate the backend and frontend components.

5. **Deployment**:
   - Deploy the backend and frontend to AWS ECS instances.


## Final Thoughts

Congratulations on successfully setting up and integrating your art gallery application with Amazon ECS! This achievement highlights your understanding of scalable and efficient containerized application deployment, as well as your ability to manage real-world systems on AWS. Keep experimenting, refining, and advancing your skills as you continue your DevOps journey.

<p align="center">
  <img src="https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExYTd0MXc2bXE3cnB4ZGxpeW1mZHN0OHI1anhqdTl1bzRscGd0a3BjbiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/QPcJjFPzZXS4X61jwF/giphy.gif" width="50%">
</p>
