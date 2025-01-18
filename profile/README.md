# Automated Go Application Deployment Pipeline

## Overview
This diagram illustrates an automated deployment and release pipeline for a Go application using GitHub Actions, Terraform, Ansible, and DigitalOcean infrastructure.

![arch drawio](https://github.com/user-attachments/assets/783a98df-98c9-4dc1-95ff-0b5704226bf4)

## Workflow Components

### Development Flow
The process begins with a Go repository where:
- Source code is maintained
- Changes are committed to the master branch
- New tags trigger the automation pipeline

### CI/CD Pipeline
1. **GitHub Actions**
  - Triggered on new tags
  - Builds the application
  - Publishes container images to GitHub Container Registry (GHCR)

### Infrastructure Management

#### Onboarding Phase
1. **Terraform** creates a new DigitalOcean droplet
2. **Ansible**:
  - Configures the droplet
  - After configuration, Ansible pulls the application from GitHub Container Registry (GHCR)

#### Release Phase
1. **Ansible** manages the release process by:
  - Pulling the latest container image from GHCR
  - Starting the container with the updated image on the DigitalOcean droplet

## Technology Stack
- Version Control: GitHub
- Container Registry: GitHub Container Registry
- Infrastructure: DigitalOcean
- IaC: Terraform
- Configuration Management: Ansible
- CI/CD: GitHub Actions
- Application: Go
