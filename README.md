# Hello World CI/CD Pipeline 🚀

[![CI/CD Pipeline](https://github.com/rednexx/pd-frontend/actions/workflows/cicd.yml/badge.svg)](https://github.com/rednexx/pd-frontend/actions/workflows/cicd.yml)

Welcome to my CI/CD practical exercise! This repository contains a simple "Hello World" frontend application built with Vue 3 and Vite, fully automated through a GitHub Actions pipeline. 

Developed by **José Xavier**.

## 🛠️ Tech Stack
* **Frontend:** Vue 3 + Vite
* **Containerization:** Docker (Multi-stage build with Node 20 & Nginx)
* **CI/CD:** GitHub Actions
* **Registry:** GitHub Container Registry (GHCR)

---

## ⚙️ How the Pipeline Works

Whenever a new commit is pushed to the `main` branch, the GitHub Actions workflow (`.github/workflows/cicd.yml`) kicks in. It is divided into two main jobs:

### 1. The Gatekeeper (`validate-commit`)
To maintain a clean and readable project history, this pipeline strictly enforces the **Conventional Commits** standard. 
If a commit message doesn't start with a valid tag (like `feat:`, `fix:`, `docs:`, etc.), the pipeline will instantly **fail** and block the build process.

* ❌ **Fails:** `git commit -m "updated the text on the homepage"`
* ✅ **Passes:** `git commit -m "feat: updated the text on the homepage"`

### 2. The Builder (`build-and-publish`)
If the commit message passes the validation, this job takes over. It will:
1. Securely log into the GitHub Container Registry.
2. Build a fresh Docker image of the Vue application using a multi-stage process (compiling with Node and serving via Nginx for maximum performance).
3. Tag the image with the specific commit hash.
4. Publish the final image to the **Packages** section of this repository.