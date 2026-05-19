# 📦 K5U1 - Inventory API

## 📖 Project Overview

This project is a production-oriented Inventory API built with ASP.NET Core and .NET 9.

The goal of the assignment was to transform an existing API into a more secure and cloud-ready application using:

- Docker containerization
- CI/CD automation
- Azure cloud deployment
- Azure Key Vault integration
- Managed Identity authentication
- Secure configuration management

The project focuses on DevOps principles, cloud-native architecture, automation, and security best practices.

---

## 🛠️ Technologies

- .NET 9 / ASP.NET Core Web API
- Entity Framework Core
- InMemory Database
- Docker
- GitHub Actions
- Azure Container Apps
- Azure Container Registry (ACR)
- Azure Key Vault
- Managed Identity
- Scalar / OpenAPI

---

## 🧱 Project Structure

The project follows a clean and simple structure:

- `Controllers/` → Handles HTTP requests
- `Models/` → Domain entities
- `Data/` → Database context
- `CloudNativeInventory.Tests/` → Automated tests
- `.github/workflows/` → CI/CD pipeline configuration

---

## 🐳 Dockerization

The API was containerized using Docker with a multi-stage Dockerfile.

### Why multi-stage builds?

A multi-stage build reduces the final image size by separating:

- Build environment
- Runtime environment

This improves:

- Performance
- Security
- Deployment speed

The final image only contains the published application instead of the full SDK.

---

## 🔒 Rootless Container Security

The container runs using:

```dockerfile
USER app
```

### Why?

Running containers as root increases security risks.

Using a rootless container:

- Reduces attack surface
- Improves container security
- Follows cloud security best practices

---

## 🌐 Port Configuration & Health Checks

The application exposes port `8080`, which is the recommended default for .NET 9 rootless containers.

The API was verified locally through Docker before deployment.

---

## ⚙️ CI/CD Pipeline

GitHub Actions was used to automate the CI/CD workflow.

The pipeline automatically runs:

- `dotnet restore`
- `dotnet build`
- `dotnet test`

on every push and pull request.

### Why CI/CD?

CI/CD improves:

- Automation
- Reliability
- Faster deployments
- Code quality validation

Broken builds can be detected before deployment.

### 🔐 GitHub Secrets

Sensitive credentials were stored securely using GitHub Secrets.

Configured secrets:

- ACR_LOGIN_SERVER
- ACR_USERNAME
- ACR_PASSWORD

Used for:

- Azure Container Registry (ACR) authentication
- Docker image push
- Automated deployment

---

## 📦 Azure Container Registry (ACR)

Azure Container Registry was used to store Docker images.

The pipeline automatically:

- Builds Docker images
- Tags images
- Pushes images to ACR

### Why use a registry?

A registry centralizes container images and simplifies deployments.

---

## ☁️ Azure Deployment

The application was deployed using Azure Container Apps.

### Why Azure Container Apps?

Azure Container Apps provides:

- Easy container hosting
- Simple scaling
- Cloud-native deployment
- Lower infrastructure management

This made it suitable for the assignment requirements.

---

## 🔐 Azure Key Vault Integration

Azure Key Vault was implemented for secure secret management.

The application uses:

```csharp
DefaultAzureCredential
```

to securely retrieve secrets from Azure.

### Why Key Vault?

Key Vault prevents:

- Hardcoded secrets in source code
- Sensitive data inside repositories
- Unsafe secret handling during deployment

This follows secure cloud development practices.

---

## 👤 Managed Identity & RBAC

A Managed Identity was configured for the container application.

RBAC permissions were used to allow the application to:

- Read secrets from Azure Key Vault
- Follow the principle of least privilege

### Why?

The application only receives the permissions it actually needs, improving overall security.

---

## 🧪 Verification Endpoint

The API deployment was successfully verified through the public Azure Container App endpoint.

Example:

```http
GET /api/inventory
```

The endpoint successfully returns product data from the InMemory database:

```json
[
  {
    "id": 1,
    "name": "Laptop",
    "stockQuantity": 10,
    "price": 9999
  }
]
```

The `verify-integration` endpoint is intended to validate Azure Key Vault integration in production, but the Key Vault secret retrieval is currently not functioning correctly.

---

## 📊 Monitoring & Logging

Basic monitoring and logging were configured in Azure.

This allows:

- Error tracking
- Request monitoring
- Easier troubleshooting

---

## 🧠 ADR (Architecture Decision Record)

An ADR document was created to explain important technical decisions, including:

- Azure service selection
- Container strategy
- CI/CD workflow design
- Security decisions
- Key Vault integration

---

## ▶️ How To Run The Project

### Clone repository

```bash
git clone <repository-url>
```

---

### Run locally

```bash
dotnet restore
dotnet build
dotnet run
```

---

### Run with Docker

```bash
docker build -t inventory-api .
docker run -p 8080:8080 inventory-api
```

---

## 🧪 Automated Tests

Tests are located in:

```text
CloudNativeInventory.Tests
```

The tests are automatically executed in the CI pipeline using GitHub Actions.

---

## 📌 Key Features

- Docker containerization
- Multi-stage Docker builds
- Rootless container security
- GitHub Actions CI/CD
- Azure deployment
- Azure Container Registry integration
- Azure Key Vault integration
- Managed Identity authentication
- Automated testing
- Secure cloud configuration

---

## 👨‍💻 Author

- Abdalle Abdulkadir
