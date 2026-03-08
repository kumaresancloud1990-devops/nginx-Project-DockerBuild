# Custom Nginx Docker Image Deployment using Docker Compose on AWS EC2

## Project Overview
This project demonstrates how to create a custom Nginx Docker image, deploy it using Docker Compose, mount a bind volume at `/var/opt/nginx`, and push the image to Docker Hub. The application is hosted on an AWS EC2 instance.

## Tech Stack
- AWS EC2
- Docker
- Docker Compose
- Nginx
- Git & GitHub
- Docker Hub

## Architecture
Developer → GitHub → AWS EC2 → Docker → Docker Compose → Nginx Container → Web Browser

## Project Structure

nginx-task3
│
├── Dockerfile
├── docker-compose.yml
├── html
│ └── index.html
└── nginx-data


## Step 1: Launch AWS EC2 Instance
1. Login to AWS Console
2. Launch Ubuntu 22.04 EC2 instance
3. Allow ports:
   - 22 (SSH)
   - 80 (HTTP)

Connect to instance:


ssh -i your-key.pem ubuntu@<EC2-PUBLIC-IP>


## Step 2: Install Docker


sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu


Verify installation:


docker --version


## Step 3: Install Docker Compose


sudo apt install docker-compose -y


Verify:


docker-compose --version


## Step 4: Create Project Directory


mkdir nginx-task3
cd nginx-task3
mkdir html
mkdir nginx-data


## Step 5: Create HTML File

Create `index.html` inside html folder.


nano html/index.html


Example:
<h1>🚀 Welcome to My Custom Nginx</h1>

<p>
This website is running inside a <b>Docker Container</b> and deployed using 
<b>Docker Compose</b> on <b>AWS EC2</b>.
</p>

<div class="badge">
DevOps Project
</div>

<div class="footer">
Created by Kumaresan | Docker + AWS
</div>

</div>

</body>
</html>

6: Create Dockerfile
FROM nginx:latest
COPY html /usr/share/nginx/html

This builds a custom Nginx image with a custom web page.

Step 7: Create docker-compose.yml
services:
  nginx:
    build: .
    container_name: custom-nginx
    ports:
      - "80:80"
    volumes:
      - ./nginx-data:/var/opt/nginx

This creates a bind mount at /var/opt/nginx.

Step 8: Build and Run Container
docker compose up -d --build

Check running containers:

docker ps
Step 9: Access Application

Open browser and enter:

http://<EC2-PUBLIC-IP>

You should see the custom Nginx page.

Step 10: Push Image to Docker Hub

Tag image:

docker tag nginx-task3-nginx <dockerhub-username>/custom-nginx:v1

Login to Docker Hub:

docker login

Push image:

docker push <dockerhub-username>/custom-nginx:v1
Step 11: Push Code to GitHub

Initialize Git:

git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <github-repo-url>
git push -u origin main
Outcome

Custom Nginx Docker image created

Container deployed using Docker Compose

Bind mount volume configured

Application hosted on AWS EC2

Docker image pushed to Docker Hub

Source code pushed to GitHub


After saving:

```bash
git add README.md
git commit -m "Added README file"
git push

