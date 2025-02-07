# 🌐 Deployment Process – Backend & Frontend (Staging & Production)

## Backend Deployment Process

### Staging Environment
- Code is pushed to the `staging` branch.
- CI/CD pipeline is automatically triggered via GitHub Actions.
- The code is deployed to the staging server without manual intervention.

### Production Environment
- Code is pushed to the `main` branch.
- CI/CD pipeline automatically triggers GitHub Actions for deployment.
- The deployment to the production server happens without manual steps.

---

## Frontend Deployment Process

### Staging Environment
- Code is pushed to the `staging` branch.
- The CI/CD pipeline triggers GitHub Actions for automatic deployment to the staging server.

### Production Environment
- Code is pushed to the `deploy` branch.
- The CI/CD pipeline triggers GitHub Actions for deployment to the production environment.
