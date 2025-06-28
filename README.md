# 🐍 Flask App with MySQL (Dockerized)

This is a simple Flask application that interacts with a MySQL database. Users can submit messages via the frontend, which are then stored in the database and displayed back.

## 🚀 Features

- Submit and view messages through a web UI
- Backend communication with MySQL database
- Fully Dockerized setup (Compose or manual)

---

## 📁 Project Setup

### 1. Clone the repository

git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
2. Create a .env file
bash
Copy
Edit
touch .env
Add your MySQL environment configuration:

env
Copy
Edit
MYSQL_HOST=mysql
MYSQL_USER=your_username
MYSQL_PASSWORD=your_password
MYSQL_DB=your_database
🐳 Docker Compose Usage
Start the app
bash
Copy
Edit
docker-compose up --build
Access the app
Frontend: http://localhost

Backend API: http://localhost:5000

🛠️ MySQL Table Setup
Once MySQL is running, create the messages table using a client (e.g., MySQL CLI or phpMyAdmin):

sql
Copy
Edit
CREATE TABLE messages (
  id INT AUTO_INCREMENT PRIMARY KEY,
  message TEXT
);
💬 Interact with the App
Submit messages at: http://localhost

Insert directly via SQL at: http://localhost:5000/insert_sql

🔄 Manual Docker Setup (Without Compose)
Step 1: Build the Flask image
bash
Copy
Edit
docker build -t flaskapp .
Step 2: Create a Docker network
bash
Copy
Edit
docker network create twotier
Step 3: Run the MySQL container
bash
Copy
Edit
docker run -d \
  --name mysql \
  -v mysql-data:/var/lib/mysql \
  --network=twotier \
  -e MYSQL_DATABASE=mydb \
  -e MYSQL_ROOT_PASSWORD=admin \
  -p 3306:3306 \
  mysql:5.7
Step 4: Run the Flask backend container
bash
Copy
Edit
docker run -d \
  --name flaskapp \
  --network=twotier \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=admin \
  -e MYSQL_DB=mydb \
  -p 5000:5000 \
  flaskapp:latest
🧹 Cleaning Up
Stop and remove containers:

bash
Copy
Edit
docker-compose down
Or, if using manual setup:

bash
Copy
Edit
docker stop flaskapp mysql
docker rm flaskapp mysql
⚠️ Notes
Replace placeholder values (e.g., your_username, your_password) with your actual configuration.

This project is intended for educational/demo use. Use security best practices in production.

Always sanitize user input to avoid SQL injection.

Check logs for debugging:

Flask app: docker logs flaskapp

MySQL: docker logs mysql
