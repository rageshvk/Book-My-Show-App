BookMyShow Node.js Application

Overview

The BookMyShow Node.js App is a web application that provides movie ticket booking services. This repository includes the source code and a Jenkins pipeline (Jenkinsfile) for continuous integration and deployment.

Prerequisites

Before running the pipeline or the app locally, ensure you have the following installed:

Node.js (v18+ recommended)

npm (Node Package Manager)

Docker

Jenkins

SonarQube (for code quality analysis)

Trivy (for security scanning)

Prometheus (for monitoring, running on a separate instance)

Grafana (for visualization and dashboards, running on a separate instance)

Jenkins CI/CD Pipeline

This project includes a Jenkins pipeline defined in Jenkinsfile. Below is a breakdown of each stage:

Clean Workspace

Deletes previous builds and cleans up the workspace.

SonarQube Analysis

Runs SonarQube static code analysis to ensure code quality.

Quality Gate

Waits for the SonarQube quality gate result. If it fails, the pipeline stops.

Install Dependencies

Navigates to the application directory (bookmyshow-app).

Removes existing node_modules and installs dependencies using npm install.

Trivy FS Scan

Runs a security scan on the file system to detect vulnerabilities.

Docker Build & Push

Builds a Docker image for the application.

Pushes the image to Docker Hub.

Deploy to Container

Stops and removes any existing container.

Runs the new container on port 3000.

Logs container output.

Monitoring with Prometheus and Grafana

Prometheus collects metrics from the application and infrastructure.

Grafana visualizes these metrics with dashboards.

Ensure the application exposes metrics for Prometheus scraping (e.g., /metrics endpoint).

Configure Prometheus (running on a separate instance) to scrape application metrics.

Configure Grafana (running on a separate instance) to use Prometheus as a data source and create dashboards for real-time monitoring.

Running the Application Locally

To test the application locally:

cd bookmyshow-app
npm install
npm start

The app should now be running on http://localhost:3000.

Running the Jenkins Pipeline

Ensure Jenkins is running and configured with the necessary tools (Node.js, SonarQube, Docker, Trivy).

Set up credentials for DockerHub and SonarQube.

Trigger the Jenkins build and monitor the pipeline.

Docker Commands

To manually build and run the app in Docker:

docker build -t bookmyshow-app .
docker run -p 3000:3000 bookmyshow-app

Monitoring Setup

Prometheus

Install Prometheus on a separate instance and configure it to scrape application metrics.

Grafana

Install and start Grafana on a separate instance.

Add Prometheus (running on a separate instance) as a data source in Grafana.

Create dashboards to monitor application metrics.

Author

Ragesh VK

