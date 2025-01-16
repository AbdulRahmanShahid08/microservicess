Project Structure

This project is a microservices-based hotel registration system built with Node.js, Express, MySQL, and Docker. It consists of three primary services:

Web1: Handles user account creation and registration.

Web2: Displays a list of all registered users.

Web3: Displays the latest registered user and serves the main page for the e-commerce application.

The services communicate with a shared MySQL database and are managed using Docker Compose.

File Structure

project-root/
├── database/                          # SQL initialization scripts
│   └── init.sql
├── web1/                              # Web1 service files
│   ├── app.js
│   ├── register.html
│   ├── package.json
│   ├── Dockerfile
│   └── public/                        # Static assets
├── web2/                              # Web2 service files
│   ├── app.js
│   ├── users.html
│   ├── package.json
│   ├── Dockerfile
│   └── public/                        # Static assets
├── web3/                              # Web3 service files
│   ├── app.js
│   ├── index.html
│   ├── package.json
│   ├── Dockerfile
│   └── public/                        # Static assets
├── docker-compose.yml                 # Docker Compose configuration
└── README.md                          # Project documentation

Service Details

Web1

Purpose: User account creation and registration.

Port: 8081

Key Routes:

GET /: Serves the registration page.

POST /add-user: Handles user registration and stores data in the MySQL database.

Dependencies:

express

mysql2

body-parser

Web2

Purpose: Displays a list of all registered users.

Port: 8082

Key Routes:

GET /: Serves the user list page.

GET /fetch-users: Fetches all users from the database.

Dependencies:

express

mysql2

Web3

Purpose: Displays the latest registered user and provides the main e-commerce interface.

Port: 8083

Key Routes:

GET /: Serves the main page.

GET /latest-user: Fetches the latest user from the database.

Dependencies:

express

mysql2

Database Details

The project uses a MySQL database initialized with the following schema:

CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL,
    password VARCHAR(255) NOT NULL
);

INSERT INTO users (username, password) VALUES ('admin', 'admin123');

Environment Variables for Database Configuration:

DB_HOST: Hostname of the database service.

DB_USER: MySQL username.

DB_PASSWORD: MySQL password.

DB_NAME: Name of the database.

Docker Configuration

The project is containerized using Docker. The docker-compose.yml file orchestrates the following services:

Services

Database:

Image: mysql:8.0

Ports: 3306:3306

Environment Variables:

MYSQL_ROOT_PASSWORD: Root password for MySQL.

MYSQL_DATABASE: Database name (userdb).

MYSQL_USER: Username (user).

MYSQL_PASSWORD: Password (userpassword).

Volumes:

./database:/docker-entrypoint-initdb.d: SQL initialization scripts.

Web1:

Build Context: ./web1

Ports: 8081:8080

Environment Variables:

DB_HOST: database

DB_USER: user

DB_PASSWORD: userpassword

DB_NAME: userdb

Web2:

Build Context: ./web2

Ports: 8082:8080

Environment Variables:

DB_HOST: database

DB_USER: user

DB_PASSWORD: userpassword

DB_NAME: userdb

Web3:

Build Context: ./web3

Ports: 8083:8080

Environment Variables:

DB_HOST: database

DB_USER: user

DB_PASSWORD: userpassword

DB_NAME: userdb

How to Run

Clone the Repository:

git clone <repository-url>
cd project-root

Start the Services:

docker-compose up --build

Access the Services:

Web1: http://localhost:8081

Web2: http://localhost:8082

Web3: http://localhost:8083

Stop the Services:

docker-compose down

Notes

Ensure Docker and Docker Compose are installed before running the project.

Use .env files to securely manage sensitive environment variables if needed.

Modify the docker-compose.yml file to adjust configurations as per your requirements.

Future Enhancements

Add authentication and authorization for improved security.

Implement password hashing.

Add additional features like user profile management.

Integrate a frontend framework like React or Angular for a more dynamic interface.