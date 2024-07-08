# DevOps Stage 2 Project

## Table of Contents
1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Manual Deployment Steps](#manual-deployment-steps)
4. [Creating Dockerfiles and Docker Compose](#creating-dockerfiles-and-docker-compose)
5. [Deploying to EC2](#deploying-to-ec2)
6. [Configuring Nginx Proxy Manager](#configuring-nginx-proxy-manager)
7. [Domain Setup and SSL Configuration](#domain-setup-and-ssl-configuration)
8. [Testing the Setup](#testing-the-setup)
9. [Troubleshooting](#troubleshooting)
10. [Benefits and Learnings](#benefits-and-learnings)

## Project Overview

This project is part of the HNG DevOps Stage 2 task, where I deployed a Dockerized full stack web application with a React frontend and FastAPI + PostgreSQL backend. Nginx Proxy Manager was used for SSL and domain configurations.

## Prerequisites

- AWS Account
- EC2 Instance running Amazon Linux 2
- Docker and Docker Compose installed
- Route 53 for domain management
- Let's Encrypt for SSL certificates

## Manual Deployment Steps

1. *Install WSL and Set Up Environment:*
   - Enable WSL and install Ubuntu.
   - Update and upgrade packages: sudo apt update && sudo apt upgrade
   - Install Git: sudo apt install git
   - Clone the project repository: git clone https://github.com/JothamCloud/devops-stage-2.git

2. *Install Poetry and PostgreSQL:*
   - Install Poetry: curl -sSL https://install.python-poetry.org | python3 -
   - Add Poetry to PATH: nano ~/.bashrc and add export PATH="$HOME/.local/bin:$PATH"
   - Install PostgreSQL: sudo apt install postgresql
   - Create PostgreSQL user and database.

3. *Set Up Backend:*
   - Navigate to backend directory: cd backend
   - Install dependencies: poetry install
   - Set up database tables: poetry run bash ../prestart.sh
   - Run the backend server: poetry run uvicorn app.main:app --reload

4. *Set Up Frontend:*
   - Install Node.js and npm.
   - Navigate to frontend directory: cd ../frontend
   - Install dependencies: npm install
   - Run the frontend development server: npm run dev

## Creating Dockerfiles and Docker Compose

Created Dockerfiles and docker-compose.yml file to containerize the application. These files are included in the repository.

## Deploying to EC2

1. *Connect to EC2 Instance:*
   - Use EC2 Instance Connect to SSH into the instance.

2. *Install Docker and Docker Compose:*
   - Install Docker: sudo amazon-linux-extras install docker && sudo service docker start
   - Install Docker Compose: sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose

3. **Clone Repository and Update .env Files:**
   - Clone the repository on EC2.
   - Update VITE_API_URL in the frontend .env file.

4. *Build and Run Containers:*
   - Run: docker-compose up --build -d

## Configuring Nginx Proxy Manager

1. *Access and Login:*
   - Open http://<your-ec2-public-ip>:81 and use default credentials to log in.

2. *Add Proxy Hosts:*
   - Add configurations for frontend.ajotham.link, db.ajotham.link, and proxy.ajotham.link.

## Domain Setup and SSL Configuration

1. *Configure Route 53:*
   - Set up A records for frontend.ajotham.link, db.ajotham.link, and proxy.ajotham.link.

2. *Enable SSL in Nginx Proxy Manager:*
   - Request a new SSL Certificate using Let's Encrypt and enable Force SSL.

## Testing the Setup

1. *Access Application:*
   - Frontend: https://frontend.ajotham.link
   - Backend: https://api.ajotham.link
   - Adminer: https://db.ajotham.link

2. *Verify SSL and Redirects:*
   - Ensure connections are secure and redirects are working.

## Troubleshooting

- *502 Bad Gateway:*
  - Check Docker containers: docker ps
  - Verify Nginx Proxy Manager configuration and domain settings.

- *Database Connection Issues:*
  - Ensure the database container is running and accessible from the backend container.

## Benefits and Learnings

Completing this project as part of the HNG DevOps Stage 2 task has given me practical skills in Docker, AWS, and Nginx Proxy Manager. It’s been a fantastic learning experience that has laid a solid foundation for my future DevOps endeavors.


## Project Structure

The repository is organized into two main directories:

- **frontend**: Contains the ReactJS application.
- **backend**: Contains the FastAPI application and PostgreSQL database integration.

Each directory has its own README file with detailed instructions specific to that part of the application.

## Getting Started

To get started with this template, please follow the instructions in the respective directories:

- [Frontend README](./frontend/README.md)
- [Backend README](./backend/README.md)

