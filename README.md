
# Multi-Tier-App-containerization 

This repository contains the fully containerized version of the **VProfile** application using Docker and Docker Compose. The architecture follows microservices best practices with dedicated containers for the app, database, load balancer, message broker, and cache.

---

##  Project Overview

The application is a multi-tier Java web app, built and run using Docker containers.

###  Technologies Used

| Component     | Technology                                |
|---------------|--------------------------------------------|
| App Build     | Maven                                     |
| App Runtime   | Tomcat                |
| Database      | MySQL                                     |
| Load Balancer | Nginx                                     |
| Messaging     | RabbitMQ                                  |
| Cache         | Memcached                                 |
| Containerization | Docker (Multi-stage builds)            |

---

## Architecture

- **App Layer**
  - Built using Maven in a multi-stage Dockerfile.
  - Output `.war` file is copied to a Tomcat container as `ROOT.war`.

- **Database Layer**
  - Uses MySQL image.
  - Initialized with a backup file located at: `db/db_backup.sql`.

- **Load Balancer**
  - Nginx container configured via a custom config file located at: `web/nginx.conf`.
  - Routes traffic to the Tomcat app container.

- **RabbitMQ**
  - Used for message queuing and decoupling services.

- **Memcached**
  - Provides fast, in-memory caching.

---

## 📁 Project Structure

```
vprofile-containerization/
│
├── Dockerfile                     # Multi-stage Dockerfile for app
├── docker-compose.yml             # Orchestration of all services
├── db/
│   └── db_backup.sql              # MySQL database initialization script
├── web/
│   └── nginx.conf                 # Nginx configuration file
└── vprofile-project/              # Application source code
```

---

##  How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/Muhamed404/Multi-Tier-App-containerization
cd Multi-Tier-App-containerization
```

### 2. Build and Start Containers

```bash
docker compose up -d
```

> This command will:
> - Build the app using Maven
> - Start Tomcat with the compiled `.war` file
> - Launch MySQL with the backup data
> - Configure Nginx as the frontend load balancer
> - Start RabbitMQ and Memcached services

---

## Access the App

Once containers are up, visit:

```
http://localhost:80
```

Or access specific services:
- **Tomcat:** http://localhost:8080
- **RabbitMQ UI:** http://localhost:15672 (default user/pass: guest/guest)
- **MySQL:** accessible on port 3306
- **Memcached:** accessible on port 11211


