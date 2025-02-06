# Deploying Apache2 Webserver

In this project, I created a custom HTML file. Then, I created a docker file which builds an Apache2 image, while copying the custom HTML file to replace the default HTML welcome page of the the Apache2 webserver.

The image in the docker file is built and run as a container on port 3035, mapping port 80 using docker compose.

The code is pushed to a github repository, and a Jenkins container is used to checkout the code, and start the Apache2 container. The server is the accessible via http://localhost:3035/ once the container is up and running

---

## Difficulties Encountered.

The main difficulty was to figure out how to run docker and docker compose inside the jenkins container. I had a choice to use either one of two options:

 **Docker-in-Docker (DinD)** or **Docker socket Binding of host machine** into the Jenkins container. Below are the steps to set up the latter:

---




### **Docker socket Binding**
This approach allows the Jenkins container to use the host's Docker daemon.

1. **Run the Jenkins container:**

   ```bash
   docker run -d \
     --name jenkins \
     -p 8085:8080 \
     -p 50000:50000 \
     -v jenkins_home:/var/jenkins_home \
     -v /var/run/docker.sock:/var/run/docker.sock \
     -u root \
     jenkins/jenkins:lts
   ```

2. **Access Jenkins:**
   - Open `http://localhost:8085` on browser.
   - Complete the Jenkins setup wizard.

3. **Install Docker-related plugins:**
   - Go to **Manage Jenkins > Manage Plugins**.
   - Install the **Docker Pipeline** plugin.

4. **Test Docker in Jenkins:**
   - Create a Jenkins pipeline job and test the script

     ```groovy
     pipeline {
       agent any
       stages {
         stage('Test Docker') {
           steps {
             script {
               docker.image('alpine:latest').inside {
                 sh 'echo "Hello from Docker!"'
               }
             }
           }
         }
       }
     }
     ```

---

### **In a Nutshell:**

- **Docker-in-Docker (DinD):** This approach is isolated but can be slower due to nested Docker layers.
- **Bind-mounting Docker Socket:** This approach is faster but less secure since the Jenkins container has full access to the host's Docker daemon.