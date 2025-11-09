#  Finance React + FastAPI Docker Application

This project is a **full-stack web application** that connects a **React frontend** with a **FastAPI backend**, both containerized using **Docker** and deployed via **AWS ECR** and **EC2**.

The application allows seamless interaction between the frontend and backend to manage and display financial transaction data.

---

## 🧩 Project Overview

This project contains two main services:

- **Backend (FastAPI):** Handles all API requests, data processing, and business logic. 
- **Frontend (React):** Displays the user interface and communicates with the backend API.

Both services are built, containerized, and deployed using **Docker** and **Docker Compose**, then hosted on **AWS** infrastructure.

---

## 🛠️ Technologies Used

- **React.js** — Frontend framework  
- **FastAPI** — Backend framework  
- **Docker & Docker Compose** — Containerization and orchestration  
- **AWS ECR (Elastic Container Registry)** — Image storage  
- **AWS EC2 (Elastic Compute Cloud)** — Hosting environment  
- **Nginx** — Serves the React build in production  
- **Ubuntu/Linux** — Server environment  

---

## ⚙️ Project Setup Steps

### 1️. Clone the Repository

```bash
git clone https://github.com/Derakings/react-fastapi-app.git
cd react-fastapi-app
```

### 2. Create an .env File

Create a .env file inside the React app directory to connect your frontend to the backend API:

REACT_APP_API_URL=http://<ip-address>:8000

⚠️ For public deployment, use your EC2 public IP.
Example: REACT_APP_API_URL=http://18.201.153.8:8000


- Each service (React and FastAPI) should have its own Dockerfile to define how the application is built and run using the Docker daemon.


### 3️ AWS ECR Setup

- Create two public and private AWS ECR repositories each: 

One for the React app
One for the FastAPI app

- Follow AWS ECR push command for authentication, build docker image and push dockerized app to the AWS Elastic Container Registry


### Provision remote server
Provision a remote server on AWS EC2 for production.



4️⃣ Docker Compose Setup

Ensure your docker-compose.yml file looks like this:
```bash
version: '3.8'

services:
  backend:
    image: <Image URL from AWS ECR>
    container_name: FastAPI-backend
    ports:
      - "8000:8000"

  frontend:
    image: <Image URL from AWS ECR>
    container_name: React-frontend
    ports:
      - "3000:80"
    depends_on:
      - backend
    environment:
      - REACT_APP_API_URL=http://ip_address:8000
```

### 5️⃣ Run Containers

Run the following commands:
```bash
docker compose down
docker compose pull
docker compose up -d
```


Check if both containers are running and logs are error-free:
```bash
docker compose ps
docker compose logs
```

### 🌐 Access the Application

- Local Server

Frontend → http://localhost:3000

Backend → http://localhost:8000

- ☁️ Remote EC2 Server

Frontend → http://18.201.153.8:3000

Backend → http://18.201.153.8:8000

---



🚀The react-fastAPI app is live.
