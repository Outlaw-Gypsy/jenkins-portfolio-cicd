## Challenges Encountered

During the implementation of this project, several technical challenges were encountered. Each issue provided valuable insight into troubleshooting CI/CD pipelines and cloud infrastructure.

⸻

### 1. GitHub Personal Access Token Permission Error

### Challenge

While pushing the repository to GitHub after creating the Jenkinsfile, Git rejected the push with an error indicating that the Personal Access Token (PAT) did not have permission to create or update workflow files.

### Cause

The existing Personal Access Token did not include the required workflow permission.

### Resolution

A new Personal Access Token was generated with the required permissions, including the workflow scope. The Git credentials were updated, after which the repository was pushed successfully.

⸻

### 2. Unable to Connect to the EC2 Instance Through SSH

### Challenge

The initial SSH connection to the EC2 instance timed out even though the instance was running.

### Cause

The subnet route table was not associated with an Internet Gateway, preventing internet traffic from reaching the EC2 instance.

### Resolution

The route table was updated with a default route (0.0.0.0/0) pointing to the Internet Gateway. After the update, SSH connectivity was restored.

⸻

### 3. Jenkins Installation Failure

### Challenge

During the Jenkins installation, Ubuntu reported that the Jenkins repository was not signed and the package could not be installed.

### Cause

The Jenkins repository signing key was not trusted by the operating system.

Resolution

The Jenkins signing key was imported correctly, the package repository was refreshed, and Jenkins was installed successfully.

⸻

### 4. Jenkins Pipeline Stuck Waiting for an Executor

### Challenge

The first pipeline execution remained in the Waiting for next available executor state.

### Cause

The Jenkins Built-in Node had been automatically marked offline because the available disk space on the /tmp filesystem was below Jenkins’ configured threshold.

### Resolution

The Disk Space Monitor threshold was reduced from 1 GiB to 100 MiB, allowing the Built-in Node to return online and execute the pipeline.

⸻

### 5. Deploying Files to the Nginx Directory

### Challenge

The portfolio website could not initially be deployed because Jenkins required permission to copy files into the Nginx web directory.

### Cause

The deployment directory (/var/www/html) is owned by the root user, while Jenkins executes the pipeline as the jenkins user.

### Resolution

The Jenkins user permissions were verified to ensure it could execute sudo commands without requiring a password. This allowed Jenkins to copy the website files and restart the Nginx service successfully.

⸻

### 6. Configuring Automatic Pipeline Execution

### Challenge

Initially, every deployment required manually clicking Build Now in Jenkins.

### Cause

No GitHub Webhook had been configured to notify Jenkins of new commits.

### Resolution

A GitHub Webhook was configured to send push events to Jenkins. The Jenkins Pipeline was also configured to listen for GitHub webhook events. After the configuration, every git push automatically triggered the pipeline.

