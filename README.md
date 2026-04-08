# 📦 Project Setup

---

# FastAPI Calculator with PostgreSQL

## Overview
This project is a simple calculator API built with **FastAPI** and **PostgreSQL**, logging calculations per user.  
Demonstrates **one-to-many relationships** with foreign keys and `ON DELETE CASCADE`. Runs in **Docker** with pgAdmin for database management.

---

## Technologies
- FastAPI (Python)  
- PostgreSQL  
- pgAdmin  
- Docker & Docker Compose  
- SQL (CRUD operations)

---

## Setup

1. **Clone repo**
```bash
git clone <YOUR_REPO_URL>
cd <REPO_FOLDER>
```

2. **Start services**
```bash
docker compose up --build
```
3. **Access pgAdmin: http://localhost:5050
Connect to PostgreSQL server (host: db, user: postgres, database: fastapi_db).

---

4. **Database Schema**

Users
```bash
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50) NOT NULL UNIQUE,
  email VARCHAR(100) NOT NULL UNIQUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
Calculations
```bash 
CREATE TABLE calculations (
  id SERIAL PRIMARY KEY,
  operation VARCHAR(20) NOT NULL,
  operand_a FLOAT NOT NULL,
  operand_b FLOAT NOT NULL,
  result FLOAT NOT NULL,
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  user_id INTEGER NOT NULL,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```
**SQL Operations**

Insert
```bash
INSERT INTO users (username, email) VALUES ('alice','alice@example.com'),('bob','bob@example.com');
INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES ('add',2,3,5,1),('divide',10,2,5,1),('multiply',4,5,20,2);
```
Query
```bash
SELECT * FROM users;
SELECT * FROM calculations;
SELECT u.username, c.operation, c.operand_a, c.operand_b, c.result
FROM calculations c JOIN users u ON c.user_id = u.id;
```
Update
```bash
UPDATE calculations SET result = 6 WHERE id = 1;
```
Delete
```bash 
DELETE FROM calculations WHERE id = 2;
```
---

5. **Docker**

Start: 
```bash 
docker compose up --build
```
Verify: 
```bash
docker ps
```

Services: FastAPI, PostgreSQL, pgAdmin

---

# 🔥 Useful Commands Cheat Sheet

| Action                         | Command                                          |
| ------------------------------- | ------------------------------------------------ |
| Clone Repository                | `git clone <repo-url>`                          |
| Create Virtual Environment     | `python3 -m venv venv`                           |
| Activate Virtual Environment   | `source venv/bin/activate` / `venv\Scripts\activate.bat` |
| Install Python Packages        | `pip install -r requirements.txt`               |
| Build Docker Image              | `docker build -t <image-name> .`                |
| Push Code to GitHub             | `git add . && git commit -m "message" && git push` |

---

