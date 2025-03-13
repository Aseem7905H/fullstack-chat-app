# Full Stack Chat Application - Docker Compose Setup

## Overview
This project contains a full-stack chat application deployed using Docker Compose. It consists of the following services:

- **MongoDB**: A NoSQL database for storing user data and messages.
- **Backend**: A Node.js Express server handling authentication, WebSocket communication, and API requests.
- **Frontend**: A React-based user interface for real-time chat functionality.

## Prerequisites
Ensure you have the following installed on your system:
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/your-repo/chatapp-docker.git
cd chatapp-docker
```

### 2. Start the Application
Run the following command to start all services:
```bash
docker-compose up -d
```
The `-d` flag runs the containers in detached mode.

### 3. Verify Running Containers
To check if all containers are running, use:
```bash
docker ps
```

### 4. Access the Application
- **Frontend**: Open `http://localhost` in your browser.
- **Backend API**: Available at `http://localhost:5001`.
- **MongoDB**: Accessible at `mongodb://mongoadmin:secret@localhost:27017/dbname?authSource=admin`.

## Configuration Details

### Docker Compose File Structure
```yaml
version: '3.8'
services:
  mongodb:
    image: mongo:latest
    volumes:
      - mongo-data:/data/db
    environment:
      - MONGO_INITDB_ROOT_USERNAME=mongoadmin
      - MONGO_INITDB_ROOT_PASSWORD=secret
    ports:
      - "27017:27017"
    networks:
      - fullstack-chatapp

  backend:
    image: aseem1069/chatapp-backend:latest
    container_name: full-stack_backend
    environment:
      - NODE_ENV=production
      - MONGODB_URI=mongodb://mongoadmin:secret@mongodb:27017/dbname?authSource=admin
      - JWT_SECRET=<your-secret-key>
      - PORT=5001
    depends_on:
      - mongodb
    networks:
      - fullstack-chatapp

  frontend:
    image: aseem1069/chatapp-frontend:latest
    container_name: full-stack_frontend
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - fullstack-chatapp

networks:
  fullstack-chatapp:
    driver: bridge

volumes:
  mongo-data:
```

## Managing the Application

### Stopping the Application
To stop all running services, use:
```bash
docker-compose down
```

### Restarting Services
To restart the services after making changes:
```bash
docker-compose restart
```

### Removing Containers and Volumes
To remove all containers and associated volumes:
```bash
docker-compose down -v
```

## Security Considerations
- Change the default `MONGO_INITDB_ROOT_PASSWORD` and `JWT_SECRET` before deploying in production.
- Use environment variables to store sensitive credentials instead of hardcoding them.
- Restrict database access to trusted sources.

## Conclusion
This setup allows for easy deployment and management of the full-stack chat application using Docker Compose.  
 

