# ADR 0001 - Use Azure Container Apps

## Status
Accepted

## Context
My project requires a cloud deployment solution for the Inventory API with container support, scalability, and CI/CD integration.

## Decision
I decided to use Azure Container Apps together with Azure Container Registry for deployment.

## Consequences
Benefits:
- Easy container deployment
- Good integration with Azure services
- Supports scaling and managed identities
- Works well with Docker and CI/CD pipelines

Tradeoffs:
- Azure student subscriptions may have regional limitations
- Requires Azure configuration and permissions
