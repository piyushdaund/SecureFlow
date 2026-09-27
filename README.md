# SecureFlow -- Todo Management System

A secure, containerized **Todo Management System** built with **PHP,
MySQL, Bootstrap, Docker, Jenkins, SonarQube, Trivy, OWASP ZAP, and
Kubernetes**.

SecureFlow provides user authentication and personal task management
while demonstrating practical **DevOps, CI/CD, containerization,
security scanning, and Kubernetes deployment** concepts.

------------------------------------------------------------------------

## 📌 Table of Contents

-   [About the Project](#-about-the-project)
-   [Project Objectives](#-project-objectives)
-   [Key Features](#-key-features)
-   [Technology Stack](#-technology-stack)
-   [Application Workflow](#-application-workflow)
-   [Project Structure](#-project-structure)
-   [Database Design](#-database-design)
-   [Security](#-security)
-   [Run Locally with PHP and MySQL](#-run-locally-with-php-and-mysql)
-   [Run with Docker Compose](#-run-with-docker-compose)
-   [Deploy with Kubernetes](#-deploy-with-kubernetes)
-   [CI/CD Pipeline](#-cicd-pipeline)
-   [Configuration](#-configuration)
-   [Important Security Notes](#-important-security-notes)
-   [Future Improvements](#-future-improvements)
-   [Learning Outcomes](#-learning-outcomes)
-   [Author](#-author)
-   [License](#-license)

------------------------------------------------------------------------

## 🚀 About the Project

**SecureFlow** is a web-based task management application designed to
demonstrate the development and deployment of a small full-stack
application using modern DevOps practices.

The application allows users to:

-   Create an account
-   Log in securely
-   Create personal tasks
-   Assign task priorities
-   Track pending and completed tasks
-   Edit tasks
-   Mark tasks as completed
-   Delete tasks
-   Filter tasks by status
-   Receive application notifications

The project goes beyond basic application development by integrating a
deployment workflow using **Docker and Kubernetes**, together with
automated code-quality and security checks.

------------------------------------------------------------------------

## 🎯 Project Objectives

The main objectives of SecureFlow are:

1.  Build a functional web-based task management application.
2.  Implement user authentication and session-based access control.
3.  Store application data in a relational MySQL database.
4.  Use prepared SQL statements to reduce SQL injection risks.
5.  Containerize the application using Docker.
6.  Run the application and database using Docker Compose.
7.  Automate build and deployment tasks using Jenkins.
8.  Perform static code analysis using SonarQube.
9.  Scan Docker images using Trivy.
10. Perform web application security testing using OWASP ZAP.
11. Deploy the application to Kubernetes.
12. Demonstrate persistent MySQL storage using Kubernetes Persistent
    Volumes and Persistent Volume Claims.

------------------------------------------------------------------------

## ✨ Key Features

### 👤 User Management

-   User registration
-   User login and logout
-   Session-based authentication
-   Unique username validation
-   Password hashing using PHP's `password_hash()`
-   Password verification using `password_verify()`
-   Password complexity validation

### ✅ Task Management

-   Add new tasks
-   Edit existing tasks
-   Delete tasks
-   Mark tasks as completed
-   Track task creation time
-   Track task completion time
-   User-specific task access

### 🎯 Task Priority

Each task can have one of three priorities:

-   **Low**
-   **Medium**
-   **High**

### 📊 Task Status

Tasks can be:

-   **Pending**
-   **Completed**

Users can filter the task list by status.

### 🔔 Notification System

The UI includes a notification system for events such as:

-   Successful registration
-   Login-related messages
-   Task creation
-   Task updates
-   Task completion
-   Task deletion
-   Error messages

### 📱 Responsive UI

The frontend uses **Bootstrap 5** and responsive CSS to provide a usable
interface across desktop and smaller screens.

------------------------------------------------------------------------

## 🛠 Technology Stack

  Category               Technology
  ---------------------- -----------------------------------------
  Backend                PHP 8.2
  Web Server             Apache
  Database               MySQL 8.0
  Frontend               HTML5, CSS3, Bootstrap 5
  Icons                  Bootstrap Icons
  Database Access        PHP MySQLi
  Authentication         PHP Sessions
  Password Security      `password_hash()` / `password_verify()`
  Containerization       Docker
  Local Orchestration    Docker Compose
  CI/CD                  Jenkins
  Code Quality           SonarQube
  Container Security     Trivy
  Web Security Testing   OWASP ZAP
  Orchestration          Kubernetes
  Persistent Storage     Kubernetes PV/PVC
  Source Control         Git / GitHub

------------------------------------------------------------------------

## 🔄 Application Workflow

``` text
                    ┌──────────────────────┐
                    │       User           │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   PHP Web Application│
                    │   + Bootstrap UI     │
                    └──────────┬───────────┘
                               │
                    ┌──────────┴───────────┐
                    │                      │
                    ▼                      ▼
             Authentication          Task Management
                    │                      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      MySQL 8.0       │
                    │ users + tasks tables │
                    └──────────────────────┘
```

### Deployment Workflow

``` text
Git Repository
      │
      ▼
   Jenkins
      │
      ├── PHP Syntax Check
      │
      ├── SonarQube Analysis
      │
      ├── Docker Image Build
      │
      ├── Trivy Image Scan
      │
      ├── Push Image to Registry
      │
      ├── Deploy to Kubernetes
      │
      ├── Verify Kubernetes Rollout
      │
      └── OWASP ZAP Security Scan
```

------------------------------------------------------------------------

## 📁 Project Structure

``` text
CDAC-Project-main/
│
├── database/
│   └── todo-db.sql
│
├── images/
│   └── sunbeam.jpg
│
├── k8s/
│   ├── configmap.yaml
│   ├── index.html
│   ├── mysql-deployment.yaml
│   ├── mysql-pv.yaml
│   ├── mysql-pvc.yaml
│   ├── mysql-service.yaml
│   ├── namespace.yaml
│   ├── secret.yaml
│   ├── todo-deployment.yaml
│   └── todo-service.yaml
│
├── base.html.php
├── complete_task.php
├── config.php
├── delete_task.php
├── Dockerfile
├── docker-compose.yml
├── edit_task.php
├── index.php
├── Jenkinsfile
├── login.php
├── logout.php
├── register.php
└── sonar-project.properties
```

------------------------------------------------------------------------

## 🗄 Database Design

The application uses a MySQL database named:

``` text
mytododb
```

### Users Table

Stores registered application users.

``` text
users
├── id
├── username
├── password_hash
├── created_at
└── updated_at
```

### Tasks Table

Stores tasks belonging to users.

``` text
tasks
├── id
├── name
├── status
├── priority
├── created_at
├── completed_at
└── user_id
```

### Relationship

``` text
users
  │
  │ 1
  │
  │
  │ N
  ▼
tasks
```

A user can have multiple tasks, while every task belongs to a specific
user.

The `user_id` foreign key uses `ON DELETE CASCADE`, so tasks associated
with a deleted user are removed automatically.

------------------------------------------------------------------------

## 🔐 Security

Security is an important part of the project.

### Authentication

The application uses PHP sessions to maintain authenticated user state.

Protected pages use a login requirement before allowing access to task
data.

### Password Hashing

Passwords are not stored as plain text. The application uses:

``` php
password_hash()
```

and:

``` php
password_verify()
```

### SQL Injection Protection

Database operations use prepared statements such as:

``` php
mysqli_prepare()
```

and parameter binding with:

``` php
mysqli_stmt_bind_param()
```

### User-Level Data Access

Task queries include the authenticated user's ID so that users access
their own tasks.

### Security Scanning

The CI/CD pipeline includes:

-   **SonarQube** for code-quality analysis
-   **Trivy** for container image vulnerability scanning
-   **OWASP ZAP** for web application security testing

------------------------------------------------------------------------

## 💻 Run Locally with PHP and MySQL

### Prerequisites

Install:

-   PHP 8.2+
-   Apache or another PHP-compatible web server
-   MySQL 8.0+
-   Git

### 1. Clone the repository

``` bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd CDAC-Project-main
```

### 2. Create the database

Import:

``` text
database/todo-db.sql
```

For example:

``` bash
mysql -u root -p < database/todo-db.sql
```

### 3. Configure the database

The application reads database configuration from environment variables.

Default local values are:

``` text
DB_HOST=localhost
DB_USER=todo_user
DB_PASS=password
DB_NAME=mytododb
```

### 4. Start the PHP application

If using Apache, place the project inside the Apache web root and open:

``` text
http://localhost/CDAC-Project-main/
```

------------------------------------------------------------------------

## 🐳 Run with Docker Compose

Docker Compose is the easiest way to run the complete application
locally.

### Prerequisites

Install:

-   Docker
-   Docker Compose

### Start the application

From the project root:

``` bash
docker compose up --build
```

The application container uses:

``` text
PHP 8.2 + Apache
```

and the database container uses:

``` text
MySQL 8.0
```

### Application URL

Open:

``` text
http://localhost:8081
```

### MySQL Port

The MySQL container is exposed locally on:

``` text
localhost:3307
```

### Stop the application

``` bash
docker compose down
```

### Rebuild the application

``` bash
docker compose up --build
```

------------------------------------------------------------------------

## ☸️ Deploy with Kubernetes

The project contains Kubernetes manifests under:

``` text
k8s/
```

The manifests define:

-   Namespace
-   ConfigMap
-   Secret
-   MySQL Deployment
-   MySQL Service
-   Persistent Volume
-   Persistent Volume Claim
-   Todo Application Deployment
-   Todo Application Service

### Create the namespace

``` bash
kubectl apply -f k8s/namespace.yaml
```

### Deploy configuration and secrets

``` bash
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/secret.yaml
```

### Deploy MySQL

``` bash
kubectl apply -f k8s/mysql-pv.yaml
kubectl apply -f k8s/mysql-pvc.yaml
kubectl apply -f k8s/mysql-deployment.yaml
kubectl apply -f k8s/mysql-service.yaml
```

### Deploy the application

``` bash
kubectl apply -f k8s/todo-deployment.yaml
kubectl apply -f k8s/todo-service.yaml
```

### Check resources

``` bash
kubectl get pods -n secureflow
kubectl get services -n secureflow
kubectl get deployments -n secureflow
```

The application service is configured as a Kubernetes `NodePort` using:

``` text
30080
```

The exact URL depends on your Kubernetes environment.

------------------------------------------------------------------------

## 🔁 CI/CD Pipeline

The `Jenkinsfile` defines an automated pipeline.

### Pipeline Stages

#### 1. Checkout

Retrieves the source code from the configured Git repository.

#### 2. PHP Syntax Check

Runs PHP syntax validation against PHP files.

``` bash
php -l
```

#### 3. SonarQube Scan

Analyzes source code using SonarQube.

#### 4. Docker Build

Builds the application container image.

#### 5. Trivy Scan

Scans the Docker image for known vulnerabilities.

#### 6. Docker Registry Push

Pushes the image to the configured Docker registry.

#### 7. Kubernetes Deployment

Applies the Kubernetes manifests:

``` bash
kubectl apply -f k8s/
```

#### 8. Deployment Verification

Checks Kubernetes rollout status.

#### 9. OWASP ZAP Scan

Runs an automated baseline security scan against the deployed
application.

#### 10. Report Collection

The ZAP report is copied back into the Jenkins workspace and archived as
a build artifact.

------------------------------------------------------------------------

## ⚙️ Configuration

Database configuration is controlled using environment variables.

  Variable    Description         Example
  ----------- ------------------- -------------
  `DB_HOST`   MySQL hostname      `mysql`
  `DB_USER`   Database username   `todo_user`
  `DB_PASS`   Database password   `password`
  `DB_NAME`   Database name       `mytododb`

For Docker Compose, the application receives these values automatically
from `docker-compose.yml`.

For Kubernetes, database configuration is supplied through:

-   `ConfigMap`
-   `Secret`

------------------------------------------------------------------------

## ⚠️ Important Security Notes

The repository currently contains example/default credentials in
configuration and Kubernetes manifests.

**Do not use these credentials in a production environment.**

Before production deployment:

-   Replace default database passwords.
-   Use Kubernetes Secrets or an external secrets manager.
-   Do not commit real credentials to Git.
-   Rotate any credentials that may already have been exposed.
-   Store Jenkins and Docker registry credentials in Jenkins Credentials
    Manager.
-   Avoid hard-coding infrastructure IP addresses.
-   Configure HTTPS/TLS.
-   Use a production-grade Kubernetes storage solution instead of local
    `hostPath` storage where appropriate.
-   Review OWASP findings before deployment.

The example values in this repository should be treated as
development/demo configuration.

------------------------------------------------------------------------

## 📈 Future Improvements

Possible improvements for future versions include:

-   Role-based access control
-   Admin dashboard
-   Task search
-   Pagination
-   Due dates and reminders
-   Task categories/tags
-   REST API
-   API authentication using JWT
-   Email notifications
-   Redis caching
-   Automated unit and integration tests
-   Centralized application logging
-   Prometheus and Grafana monitoring
-   HTTPS with TLS certificates
-   Helm charts
-   Horizontal Pod Autoscaling
-   Production-grade Kubernetes storage
-   External secrets management
-   Cloud deployment on AWS
-   GitHub Actions integration

------------------------------------------------------------------------

## 🎓 Learning Outcomes

This project demonstrates practical experience with:

### Application Development

-   PHP
-   MySQL
-   HTML
-   CSS
-   Bootstrap
-   Authentication
-   Session management
-   CRUD operations
-   Relational database design

### DevOps

-   Git
-   Docker
-   Docker Compose
-   Jenkins
-   CI/CD pipelines
-   Docker image management

### DevSecOps

-   SonarQube
-   Trivy
-   OWASP ZAP
-   Static code analysis
-   Container vulnerability scanning
-   Web application security testing

### Cloud & Container Orchestration

-   Kubernetes
-   Deployments
-   Services
-   ConfigMaps
-   Secrets
-   Persistent Volumes
-   Persistent Volume Claims
-   Kubernetes namespaces

------------------------------------------------------------------------

## 📸 Application Screens

Add your application screenshots here to make the GitHub repository more
attractive.

Example:

``` markdown
![Login Screen](screenshots/login.png)

![Task Dashboard](screenshots/dashboard.png)

![Task Management](screenshots/tasks.png)
```

Recommended screenshots:

1.  Login page
2.  Registration page
3.  Task dashboard
4.  Add task screen
5.  Completed task view
6.  Docker containers
7.  Jenkins pipeline
8.  Kubernetes deployment

------------------------------------------------------------------------

## 👨‍💻 Author

**Pranav Daund**

Software Developer \| Web Development \| DevOps

-   GitHub: `https://github.com/pranavdaund`
-   LinkedIn: Add your LinkedIn profile URL

------------------------------------------------------------------------

## 📄 License

This project was developed for educational and project demonstration
purposes.

If you intend to distribute or reuse the project, add an appropriate
open-source license such as MIT License and update this section
accordingly.

------------------------------------------------------------------------

## ⭐ Support

If you find this project useful for learning PHP, Docker, Jenkins,
Kubernetes, or DevSecOps concepts, consider giving the repository a ⭐
on GitHub.
