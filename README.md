#  Docker + Jenkins + Ansible CI/CD Pipeline

This is a demo DevOps project that implements a complete CI/CD pipeline using:

-  Docker – to containerize a Python Flask application  
-  Jenkins – to build, push, and automate the deployment process  
-  DockerHub – to store built images  
-  Ansible – to deploy the container to a remote host

##  Project Structure

.
├── Dockerfile  
├── app.py  
├── deploy-playbook.yml  
├── inventory.ini  
└── Jenkinsfile

##  How It Works

1. Jenkins Pipeline (defined in Jenkinsfile):  
   - Clones the repository  
   - Builds a Docker image  
   - Pushes the image to DockerHub  
   - Deploys the image using Ansible  

2. Ansible Playbook:  
   - Uses docker_container module to run the container remotely  
   - Exposes the app on port 80  

3. Dockerfile:  
   - Based on python:3.9-slim  
   - Copies and runs app.py, a simple Flask app  

##  Try It Yourself

git clone https://github.com/silverdeath366/docker-ansible-app.git

Make sure to update:
- DockerHub credentials in Jenkins  
- SSH keys and IP address in inventory.ini  

##  Security Notes

- No sensitive data is committed in this repo  
- Do NOT push private SSH keys or passwords  
- This repo is safe to share publicly and add to your resume  


##   Troubleshoot problems

1. Docker Permission Denied in Jenkins
Jenkins failed to run Docker commands with an error about permission to access the Docker socket.
Solution: The Jenkins user was added to the docker group, allowing it to run Docker commands without sudo.

2. SSH Authentication Failures During Ansible Deployment
Initial Ansible deployments failed with SSH permission errors or missing keys.
Solution: A dedicated SSH key pair was generated for Jenkins. The public key was added to the remote server’s authorized_keys, and permissions were correctly set to allow secure access.

3. Ansible Inventory Not Recognized
Errors were raised due to Jenkins not parsing the inventory.ini file properly.
Solution: The full path to the inventory file was used in the pipeline to ensure Ansible could locate it during execution.

4. Sudo Password Prompts in Ansible
Ansible failed during the playbook run due to missing sudo access.
Solution: The remote user was configured with passwordless sudo privileges, eliminating the need to provide a password interactively.

5. Jenkins Pipeline Syntax Errors
Early versions of the Jenkinsfile caused failures due to incorrect block nesting or missing braces.
Solution: The pipeline syntax was carefully validated, and fixed using proper indentation and structure for all stages and environment declarations.



