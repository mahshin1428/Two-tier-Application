
---

## 🚀 Features

- Submit and store messages in MySQL via Flask
- Dockerized backend and database
- Kubernetes support for:
  - **Auto-scaling**
  - **Self-healing**
  - **Cluster orchestration**
- Ready for deployment on **AWS EKS**
- Two Dockerfile versions: single-stage and multistage (for optimization)


## 🐳 Docker Setup

### 1️⃣ Using Docker Compose (Recommended for Local)

1. Clone the repo:
   
git clone https://github.com/mahshin1428/flask-mysql-k8s.git
cd flask-mysql-k8s


2.Add a .env file:

MYSQL_HOST=mysql
MYSQL_USER=root
MYSQL_PASSWORD=admin
MYSQL_DB=mydb

3.Start the services:
docker-compose up --build
Access the app:

Frontend: http://localhost

Backend: http://localhost:5000

Set up the database:


Use a MySQL client or UI tool to execute:
CREATE TABLE messages (
  id INT AUTO_INCREMENT PRIMARY KEY,
  message TEXT
);


⚙️ Manual Docker Run (Without Compose)
Create a Docker network:
docker network create twotier


Run MySQL container:

docker run -d \
  --name mysql \
  -v mysql-data:/var/lib/mysql \
  --network=twotier \
  -e MYSQL_DATABASE=mydb \
  -e MYSQL_ROOT_PASSWORD=admin \
  -p 3306:3306 \
  mysql:5.7

  
Run Flask app container:
docker build -t flaskapp .
docker run -d \
  --name flaskapp \
  --network=twotier \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=admin \
  -e MYSQL_DB=mydb \
  -p 5000:5000 \
  flaskapp:latest



