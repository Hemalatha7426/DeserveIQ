# DeserveIQ

DeserveIQ is a full-stack student deservingness and dropout-risk prediction application. It combines a React dashboard, a Spring Boot backend, and a Flask-based ML service that serves predictions from trained model artifacts.

## Project Structure

```text
DeserveIQ-main/
├── DeserveIQ/          # Spring Boot backend
├── frontend/           # React frontend
├── ml-service/         # Flask ML prediction API
└── docker-compose.yml  # Container orchestration
```

## Features

- Admin login with JWT-based authentication
- Single student dropout-risk prediction
- Batch CSV upload for multiple predictions
- Student records API with create, list, view, and delete operations
- Human-readable ML explanations with risk tier and deservingness score
- Docker support for frontend, backend, and ML service

## Tech Stack

- Frontend: React, Bootstrap, Axios, Recharts
- Backend: Java, Spring Boot, Spring Security, Spring Data JPA
- Database: MySQL
- ML Service: Python, Flask, Pandas, NumPy, scikit-learn, Joblib
- Deployment: Docker, Docker Compose

## Prerequisites

- Node.js and npm
- Java 21 or compatible JDK
- Maven wrapper, included in `DeserveIQ/`
- Python 3.10+
- MySQL
- Docker Desktop, optional

## Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/Hemalatha7426/DeserveIQ.git
cd DeserveIQ
```

### 2. Configure MySQL

Create a MySQL database named `deserveiq`.

Update the database credentials in:

```text
DeserveIQ/src/main/resources/application.properties
```

The backend expects MySQL on `localhost:3306` by default.

### 3. Start the ML service

```bash
cd ml-service
python -m pip install flask numpy pandas scikit-learn joblib
python api_deserveiq.py
```

ML service URL:

```text
http://localhost:5000
```

### 4. Start the backend

Open a new terminal:

```bash
cd DeserveIQ
./mvnw spring-boot:run
```

On Windows PowerShell:

```powershell
.\mvnw.cmd spring-boot:run
```

Backend URL:

```text
http://localhost:8080
```

### 5. Start the frontend

Open a new terminal:

```bash
cd frontend
npm install
npm start
```

Frontend URL:

```text
http://localhost:3000
```

## Docker Setup

Start Docker Desktop, then run:

```bash
docker compose up --build
```

Container URLs:

- Frontend: `http://localhost:3000`
- Backend: `http://localhost:8080`
- ML service: `http://localhost:5000`

Note: if running the backend in Docker with MySQL, enable or add a MySQL service in `docker-compose.yml` and set the Spring datasource environment variables accordingly.

## API Endpoints

### Authentication

```text
POST /auth/login
```

Default admin credentials:

```text
email: admin@maatram.org
password: password
```

### Predictions

```text
POST /api/predict/single
POST /api/predict/batch
```

### Students

```text
GET    /api/students
GET    /api/students/{id}
POST   /api/students
DELETE /api/students/{id}
```

## ML Service Endpoint

```text
POST /predict
```

Returns:

- `dropout_probability`
- `deservingness_score`
- `risk_tier`
- `explanation`

## Notes

- The ML service loads model artifacts from `ml-service/deserveiq_artifacts`.
- `node_modules`, virtual environments, logs, and build outputs are intentionally ignored by Git.
- Keep production database passwords and secrets outside source control.
