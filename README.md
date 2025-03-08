# 📽️ BookMyShow Node.js Application

## 📝 Overview

The **BookMyShow Node.js App** is a web application for booking movie tickets. This repository includes the source code and a **Jenkins pipeline (Jenkinsfile)** for continuous integration and deployment.

## ✅ Prerequisites

Before running the pipeline or the app locally, ensure you have the following installed:

- **Node.js** (v18+ recommended)  
- **npm** (Node Package Manager)  
- **Docker**  
- **Jenkins**  
- **SonarQube** (for code quality analysis)  
- **Trivy** (for security scanning)  
- **Prometheus** (for monitoring, running on a separate instance)  
- **Grafana** (for visualization and dashboards, running on a separate instance)  

---

## 🔄 Jenkins CI/CD Pipeline

This project includes a **Jenkins pipeline** defined in `Jenkinsfile`. Below is a breakdown of each stage:

### 📌 Pipeline Stages

1️⃣ **Clean Workspace**  
   - Deletes previous builds and cleans up the workspace.  

2️⃣ **SonarQube Analysis**  
   - Runs SonarQube static code analysis to ensure code quality.  

3️⃣ **Quality Gate**  
   - Waits for the SonarQube quality gate result. If it fails, the pipeline stops.  

4️⃣ **Install Dependencies**  
   - Navigates to the application directory (`bookmyshow-app`).  
   - Removes existing `node_modules` and installs dependencies using `npm install`.  

5️⃣ **Trivy FS Scan**  
   - Runs a security scan on the file system to detect vulnerabilities.  

6️⃣ **Docker Build & Push**  
   - Builds a Docker image for the application.  
   - Pushes the image to **Docker Hub**.  

7️⃣ **Deploy to Container**  
   - Stops and removes any existing container.  
   - Runs the new container on **port 3000**.  
   - Logs container output.

## 📌 Load Balancing & Autoscaling in AWS**  
   - Uses **AWS Application Load Balancer (ALB)** to distribute incoming traffic across multiple EC2 instances.  
   - Implements **AWS Auto Scaling Group (ASG)** to dynamically add or remove instances based on CPU usage or traffic.  
   - Ensures **high availability and zero downtime** by gradually deploying new instances while keeping the old ones running until fully replaced.

##  Monitoring with Prometheus & Grafana**  
   - **Prometheus** collects metrics from the application and infrastructure.  
   - **Grafana** visualizes these metrics with dashboards.  
   - Ensure the application exposes metrics for Prometheus scraping (e.g., `/metrics` endpoint).  
   - Configure Prometheus (running on a separate instance) to scrape application metrics.  
   - Configure Grafana (running on a separate instance) to use Prometheus as a data source and create dashboards for real-time monitoring.  

## 👨‍💻 Author
   - Ragesh VK
