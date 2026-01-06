# 🚀 Microservice Project

A simple **Docker Compose–based microservice application** demonstrating how multiple services communicate with each other using **REST APIs**, **PostgreSQL**, and **Redis caching**.

This project is fully backend-based (no UI) and is tested using `curl` or any API testing tool.

---

## 🧩 Project Overview

The **Microservice Project** consists of **four main components**:

1. **User Service** – Handles user registration
2. **Data Service** – Fetches user information
3. **PostgreSQL** – Permanent database storage
4. **Redis** – Cache layer for faster data access

All services are deployed and managed using **Docker Compose**.

---

## 🛠️ Tech Stack

* **Python (Flask)** – Backend services
* **Docker & Docker Compose** – Containerization & orchestration
* **PostgreSQL** – Relational database
* **Redis** – In-memory caching
* **Linux** – Development & testing environment

---

## 🏗️ Architecture Flow

1. User sends data to **User Service** (`/register` API)
2. User Service stores data in **PostgreSQL**
3. When data is requested from **Data Service**:

   * First check happens in **Redis cache**
   * If data is **not cached** → fetched from PostgreSQL → stored in Redis
   * If data **exists in cache** → returned directly from Redis

---

## 📁 Project Structure

```
microservice_project/
│
├── docker-compose.yaml
│
├── user-service/
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│
├── data-service/
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│
├── init.sql   # Database initialization script
```

> Note: `user-service` and `data-service` have similar file structures but different internal logic.

---

## 🚀 How to Run the Project

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/Shikha-1811/microservice_project.git
cd microservice_project
```

### 2️⃣ Start Services Using Docker Compose

```bash
docker compose up --build
```

This will start:

* User Service (port **5000**)
* Data Service (port **5001**)
* PostgreSQL
* Redis

---

## 🔗 API Usage

### 🧑 User Registration (User Service)

**Endpoint:**

```
POST http://127.0.0.1:5000/register
```

**Request Body (JSON):**

```json
{
  "name": "vimal",
  "info": "i am from jaipur"
}
```

This stores user data in **PostgreSQL**.

---

### 📄 Fetch User Information (Data Service)

**Endpoint:**

```
GET http://127.0.0.1:5001/<username>
```

**Example:**

```
http://127.0.0.1:5001/vimal
```

#### Behavior:

* **First request:**

  * Cache status → `false`
  * Data fetched from PostgreSQL
  * Data stored in Redis

* **Second request:**

  * Cache status → `true`
  * Data returned directly from Redis

---

## ⚡ Caching Logic (Redis)

* Improves performance by avoiding repeated database queries
* Demonstrates **real-world microservice caching strategy**
* Shows difference between **cache miss** and **cache hit**

---

## 🧪 Testing the Application

You can test APIs using:

* `curl`
* Postman
* Any REST client

Example curl command:

```bash
curl -X POST http://127.0.0.1:5000/register \
-H "Content-Type: application/json" \
-d '{"name":"vimal","info":"i am from jaipur"}'
```

---

## 📌 Key Learnings

* Microservice architecture basics
* Service-to-service communication
* Docker Compose orchestration
* Redis caching mechanism
* PostgreSQL integration with Python services

---

## 🙌 Conclusion

This project is a **beginner-friendly microservice application** that demonstrates how real-world backend systems work using Docker, databases, and caching.

Feel free to fork, improve, and experiment 🚀

---

### ⭐ If you like this project, don’t forget to star the repository!
