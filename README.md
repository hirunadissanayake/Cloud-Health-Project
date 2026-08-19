# Cloud Health Project

A cloud-native healthcare management system built as independently deployable platform services, domain microservices, a clinical web application, and reproducible Google Cloud infrastructure.

## About

This project is the final project for **ITS 2130 - Enterprise Cloud Architecture**. It demonstrates service discovery, centralized configuration, API gateway routing, relational and document persistence, cloud object storage, managed infrastructure, and a browser-based healthcare workflow.

| Project detail | Value |
|---|---|
| Student | Hiruna Dissanayake |
| Student number | `TODO` |
| Slack handle | `TODO` |
| Google Cloud project | `cloud-health-506015-hiruna` |
| Default region | `asia-south1` |

## Tech Stack

| Technology | Purpose |
|---|---|
| Java 25 | Backend runtime |
| Spring Boot 4.1.0 | Application framework |
| Spring Cloud 2025.1.2 | Config, Eureka, Gateway, and load balancing |
| PostgreSQL 17 / Cloud SQL | Patient and appointment persistence |
| MongoDB Atlas | Diagnostic records and health metrics |
| Google Cloud Storage | Private medical-file storage |
| Firestore | Medical-file metadata |
| Node.js 22+ | Clinical web application |
| Terraform and Packer | Google Cloud infrastructure and VM images |
| Docker and Cloud Build | Container build and Cloud Run deployment |

## Repository Names

Use these names when creating the public GitHub repositories:

| Local component | GitHub repository name |
|---|---|
| Project root | `Cloud-Health-Project` |
| `backend-platform` parent | `Cloud-Health-Project-Platform` |
| Config Server | `Cloud-Health-Project-Platform-Config-Server` |
| Discovery Server | `Cloud-Health-Project-Platform-Discovery-Server` |
| API Gateway | `Cloud-Health-Project-Platform-Api-Gateway` |
| Configuration repository | `Cloud-Health-Project-Platform-Config-Repository` |
| `backend-services` parent | `Cloud-Health-Project-Services` |
| Patient Service | `Cloud-Health-Project-Service-Patient` |
| Diagnostics Service | `Cloud-Health-Project-Service-Diagnostics` |
| File Service | `Cloud-Health-Project-Service-File` |
| Clinical web application | `Cloud-Health-Project-Webapp` |
| Google Cloud infrastructure | `Cloud-Health-Project-Infrastructure` |

The Platform and Services repositories act as parent repositories. Their component repositories will be attached as Git submodules before submission.

## Architecture

```text
Cloud Run Webapp
       |
Global Load Balancer
       |
API Gateway :8080
       |
Eureka Discovery Server :8761
       |
+----------------+---------------------+----------------+
| Patient        | Diagnostics         | File           |
| Service :8081  | Service :8082       | Service :8083  |
| Cloud SQL      | MongoDB Atlas       | GCS/Firestore  |
+----------------+---------------------+----------------+
       |
Config Server :8888 -> Git configuration repository
```

## Project Structure

```text
backend-platform/
├── config-server/
├── discovery-server/
├── api-gateway/
└── config-repository/
backend-services/
├── patient-service/
├── diagnostics-service/
└── file-service/
frontend/
infrastructure/
└── images/
docs/
```

## Getting Started

Prerequisites are JDK 25, Docker, Git, Node.js 22+, Terraform 1.8+, and the Google Cloud CLI. Each Spring application includes Maven Wrapper, so a global Maven installation is unnecessary.

Start local applications in this order:

1. Config Server (`8888`)
2. Discovery Server (`8761`)
3. API Gateway (`8080`)
4. Patient Service (`8081`)
5. Diagnostics Service (`8082`)
6. File Service (`8083`)
7. Webapp (`3000`)

Each component README documents its environment variables, API, build, and test commands. See [the implementation plan](docs/IMPLEMENTATION_PLAN.md) for project status and [the infrastructure runbook](infrastructure/README.md) before creating billable cloud resources.

## Security

Never commit MongoDB connection strings, database passwords, Google credentials, service-account keys, Terraform state, real patient data, or generated `.tfvars` files. Runtime secrets are supplied through environment variables and Google Secret Manager.
