--------------------- MEDIUM POST ----------------------------

# Secure GitHub Pages Deployment from a Private Repository using GitHub Apps and GitHub Actions

Most developers host their portfolio websites directly from a public GitHub repository. While this approach is simple, it also means that the entire source code is publicly accessible.

I wanted a different solution:

* Keep my source code private
* Deploy automatically to GitHub Pages
* Avoid storing long-lived Personal Access Tokens (PATs)
* Follow a more secure and maintainable deployment approach

This article explains the architecture I implemented using a private source repository, a public deployment repository, GitHub Apps, and GitHub Actions.

## The Problem

GitHub Pages requires a public repository when using the standard GitHub Pages workflow.

For personal portfolio websites, this creates a challenge:

* Source code becomes publicly accessible
* Proprietary components can be copied
* Development branches and internal project structure become visible

I wanted to maintain the following workflow:

1. Keep all source code private
2. Deploy only the generated static website
3. Automate the deployment process
4. Use short-lived credentials instead of PATs

## Solution Architecture

The solution uses two repositories:

### Private Repository

Repository:

shevanfernando.github.io-source

Responsibilities:

* React/Vite application source code
* Components
* Assets
* Configuration
* Development workflow

### Public Repository

Repository:

shevanfernando.github.io

Responsibilities:

* GitHub Actions workflow
* GitHub Pages deployment
* Public website hosting

### GitHub App

A GitHub App is installed only on the private repository.

The GitHub Action generates a temporary access token at runtime and uses it to clone the private repository securely.

## Architecture Flow

1. Developer pushes code to the private repository
2. Workflow is triggered in the public repository
3. GitHub App generates a temporary access token
4. Action checks out the private repository
5. Node.js dependencies are installed
6. Production build is generated
7. Build artifacts are uploaded
8. GitHub Pages deploys the static site

Result:

The source code remains private while the generated website is publicly accessible.

## Why GitHub Apps Instead of Personal Access Tokens?

Many tutorials use Personal Access Tokens.

However, GitHub Apps provide several advantages:

### Short-Lived Credentials

Tokens are generated dynamically and expire automatically.

### Granular Permissions

Access can be limited to specific repositories.

### Better Security

No need to store high-privilege PATs.

### Enterprise Friendly

GitHub Apps align more closely with enterprise security practices.

## GitHub Actions Workflow

The workflow performs the following tasks:

### Step 1: Generate GitHub App Token

A temporary authentication token is generated using the GitHub App credentials.

### Step 2: Checkout Private Repository

The workflow clones the private source repository using the generated token.

### Step 3: Setup Node.js

Node.js runtime and dependency caching are configured.

### Step 4: Build Application

Dependencies are installed and the production build is generated.

### Step 5: Configure GitHub Pages

GitHub Pages deployment environment is prepared.

### Step 6: Upload Artifacts

The generated static files are uploaded as deployment artifacts.

### Step 7: Deploy

GitHub Pages publishes the build output.

## Benefits of This Approach

### Source Code Privacy

The website source code remains private.

### Automated Deployments

Every update can be deployed automatically.

### Security

No long-lived Personal Access Tokens are required.

### Cost Effective

Uses GitHub Free features.

### Professional Workflow

Demonstrates CI/CD and DevOps practices suitable for production environments.

## Potential Improvements

Future enhancements could include:

* Pull Request preview environments
* Lighthouse performance testing
* Automated security scanning
* Dependabot updates
* Infrastructure as Code for repository configuration
* Multi-environment deployments (Dev, Stage, Production)

## Final Thoughts

Although this project was created for a personal portfolio website, the same architecture can be used for many static websites where source code privacy is important.

The combination of GitHub Apps, GitHub Actions, and GitHub Pages provides a secure, automated, and maintainable deployment pipeline while keeping implementation details private.

For engineers looking to improve their CI/CD, DevOps, and GitHub automation skills, this is an excellent real-world project to implement and showcase.

--------------------- MEDIUM POST ----------------------------

--------------------- ARCHITECTURE ---------------------------

┌──────────────────────────────┐
│ Developer                    │
│ Push Code                    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Private Repository           │
│ shevanfernando.github.io-    │
│ source                       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ GitHub App                   │
│ Generates Temporary Token    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Public Repository            │
│ GitHub Actions Workflow      │
└──────────────┬───────────────┘
               │
     Build & Deploy
               │
               ▼
┌──────────────────────────────┐
│ GitHub Pages                 │
│ Portfolio Website            │
└──────────────────────────────┘

--------------------- ARCHITECTURE ---------------------------

--------------------- README ---------------------------------

# Portfolio Deployment Repository

This repository hosts the deployment pipeline for my personal portfolio website.

The actual website source code is maintained in a private repository. This public repository contains only the GitHub Actions workflow responsible for building and deploying the website to GitHub Pages.

## Architecture

```text
Private Source Repository
        │
        ▼
GitHub App Authentication
        │
        ▼
GitHub Actions Build Pipeline
        │
        ▼
GitHub Pages Deployment
```

## Repositories

### Private Repository

Contains:

* Application source code
* Components
* Assets
* Build configuration

### Public Repository

Contains:

* Deployment workflow
* GitHub Pages configuration
* Public hosting configuration

## Security Approach

Instead of using Personal Access Tokens (PATs), this solution uses GitHub Apps.

Benefits include:

* Temporary access tokens
* Repository-level permissions
* Improved security
* Reduced credential management overhead

## Deployment Workflow

1. Generate GitHub App token
2. Checkout private source repository
3. Install dependencies
4. Build production artifacts
5. Upload build output
6. Deploy to GitHub Pages

## Technology Stack

* GitHub Actions
* GitHub Pages
* GitHub Apps
* Node.js
* Vite
* React

## Motivation

The goal of this architecture is to:

* Keep source code private
* Automate deployments
* Improve security
* Maintain a clean public-facing repository

## Related Article

A detailed walkthrough of this implementation is available on Medium.

(Article link)

--------------------- README ---------------------------------