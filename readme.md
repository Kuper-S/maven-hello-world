# Build and Publish Java Application Pipeline with GitHub Actions and DockerHub




# Descreption 
This repository contains the source code of a simple Java application, along with a GitHub Actions workflow that automates the process of building, testing
Organization. Ansible Roles provide a structured way to organize tasks, templates, files, and variables. This structure makes it easier to manage complex automation setups, as everything related to a specific role is contained within its directory, packaging, and Publishing this application image.
This is an overview of this CI/CD pipeline, including the technologies used, GitHub secrets configuration, and a breakdown of each step in the pipeline.


# Quick Start
 **Trigger the workflow**: Push a change to the `master` branch or manually trigger the workflow through GitHub's UI under the "Actions" tab.


# Prerequisites
- A Docker Hub account + Generate access tokens and add them.
- Git installed on your local machine.


# Technologies Used 
Java: We use Java 1.8 to compile the application.
Maven: For build and dependency management tool for this Project and Maven Plugins.
Docker: For containerizing the application, ensuring consistent environments across the runners, and for image creation.
GitHub Actions: Automates CI/CD pipeline, from code push to Publish the final image Version.
Bash: For automated processes like versioning and other configuration



# Secrets Configuration
Set your own GitHub secrets to securely handle sensitive data with GitHub Actions workflow:
DOCKERHUB_USERNAME: Enter Your Docker Hub username, used for pushing images.
DOCKERHUB_PASSWORD: Enter the Docker Hub password, used for Docker login.
    OR
DOCKERHUB_TOKEN: Enter Docker Hub Token for more secure connections.
GIT_USER: Your git username for committing version bumps.
EMAIL: Your email is associated with the git user for commit operations.

# Workflow Overview

Workflow File Location: .github/workflows/build_and_deploy.yml
Trigger: The pipeline is triggered on every push to the master branch, you can change your trigger if needed.

# Workflow Pipeline Steps Explained 
Environment: The job runs on the latest Ubuntu runner (ubuntu-latest) provided by GitHub Actions. This ensures that we have a consistent and up-to-date environment for this pipeline execution.

Steps:
- Clone Stage: Clones the repository code onto the runner.
- Compile Java Source Code Stage: Compiles the application source code.
- Tests Stage: Executes unit tests to ensure code reliability.
- Package Artifact Stage: Packages compiled code into a JAR file.
- Increment Patch Version Stage: Automatically increments the application's patch version by using a bash script.
- Commit and Push Version Stage: Commits the version increment back to the repository to make sure the remote repo is aligned with the latest POM version.
- Build Docker Image Stage: Build a Docker image of the application with 2 tags, the latest and the version we are working on.
- Login to Docker Hub Stage: Authenticates with Docker Hub to enable image pushing.
- Push Docker Image Stage: Pushes the built image to Docker Hub twice the latest + version number.
- Pull Docker Image Stage: Pulls the image for testing.
- Run Docker Container for Testing Stage: Tests the running container to ensure the app is running on the container.


