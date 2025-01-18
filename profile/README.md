# Automated Go Application Deployment Pipeline

## Overview
This diagram illustrates an automated deployment and release pipeline for a Go application using GitHub Actions, Terraform, Ansible, and DigitalOcean infrastructure, split across two repositories.

![arch drawio](https://github.com/user-attachments/assets/7315052b-9cce-4f54-8b96-e5ed0724fa34)

## Repository Structure

### server Repo
Contains:
- Go application source code
- GitHub Actions workflow for:
 - Building on new tags
 - Publishing to GitHub Container Registry (GHCR)

### infra Repo
Contains:
- Terraform configurations for DigitalOcean infrastructure
- Ansible playbooks for:
 - Initial server configuration
 - Application deployment and updates

## Workflow Components

### Development Flow
The process begins with the Go repository where:
- Source code is maintained
- Changes are committed to the master branch
- New tags trigger the automation pipeline

### CI/CD Pipeline
1. **GitHub Actions** (in Go repo)
  - Triggered on new tags
  - Builds the application
  - Publishes container images to GitHub Container Registry (GHCR)

### Infrastructure Management

#### Onboarding Phase (from Infrastructure repo)
1. **Terraform** creates a new DigitalOcean droplet
2. **Ansible**:
  - Configures the droplet
  - After configuration, Ansible pulls the application from GitHub Container Registry (GHCR)

#### Release Phase (from Infrastructure repo)
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
