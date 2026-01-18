# MeetingBot CI/CD Deployment (Jenkins + AWS ECS)

## 📌 Project Overview
This project demonstrates a **CI/CD pipeline** to build, push, and deploy a containerized application on **AWS ECS (EC2 launch type)** using **Jenkins**, **Docker**, **Amazon ECR**, and **Application Load Balancer (ALB)**.

The goal is to showcase a **real-world DevOps workflow** with automated deployments and zero downtime.

---

## 🛠️ Tech Stack
- Jenkins (CI/CD)
- Docker
- Amazon ECR
- Amazon ECS (EC2)
- Application Load Balancer (ALB)
- AWS CLI

---

## 🧩 What This Pipeline Does
1. Jenkins pulls code from GitHub  
2. Builds Docker images:
   - `example-app` (frontend)
   - `server` (backend – build only)
3. Pushes images to Amazon ECR  
4. Triggers ECS service deployment  
5. ALB performs rolling update with health checks  
6. Application is served without downtime  

---


---

## 📋 Key Notes
- `example-app` is deployed as an ECS **service**
- `server` image is built and pushed but **not deployed yet**
- Deployment uses **force new deployment**
- ALB ensures traffic is routed only to healthy tasks

---

## 🖼️ Screenshots

### Jenkins Pipeline – Successful Build
<img width="1913" height="1093" alt="Screenshot 2026-01-17 235826" src="https://github.com/user-attachments/assets/90c9f14e-e4eb-45aa-85b3-25bb45a4ea34" />

<img width="1906" height="989" alt="Screenshot 2026-01-18 125650" src="https://github.com/user-attachments/assets/a3f1a048-e8cd-4d46-a7b8-232c25dd4e7f" />

---

### ECS Service – Running & Stable
<img width="1915" height="984" alt="Screenshot 2026-01-18 115429" src="https://github.com/user-attachments/assets/9c00d663-97e0-469d-a2c1-2269997250a7" />

---

### All Events Logs
<img width="1918" height="1045" alt="Screenshot 2026-01-17 235702" src="https://github.com/user-attachments/assets/31834dee-6850-43d4-8484-ea581e3bdbe4" />

---

### Application Accessed via Port and ALB
<img width="1918" height="1153" alt="Screenshot 2026-01-17 235726" src="https://github.com/user-attachments/assets/349ade9a-f9ef-4385-abbe-c424eec206a9" />

<img width="1915" height="1087" alt="Screenshot 2026-01-18 130314" src="https://github.com/user-attachments/assets/2e7766f4-dad7-43b6-8526-97359c335554" />

---

## ✅ Final Outcome
- CI/CD pipeline successfully implemented
- Docker images built and stored in ECR
- ECS service deployed behind ALB
- Zero-downtime deployments achieved

---

## 📌 Future Enhancements
- Deploy backend server service
- Use immutable image tags (commit SHA)
- Migrate to `awsvpc` network mode
- Add autoscaling and monitoring

---

### 👤 Author
**Himanshi Bobde**



## 🚀 Deployment Flow
