# Run-spring-boot-by-Local-Docker

### ✅ **Step 1: Install Docker (with Buildx and Docker Compose)**
Now let's install Docker and the necessary components, including Buildx and Docker Compose.

#### Add Docker's official repository:
```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### Install Docker:
```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

This will install Docker along with the necessary components.

### ✅ **Step 2: Verify Docker and Buildx Installation**
Now that Docker is installed, check if Buildx is available:
```bash
docker buildx version
```

If this works, then **Docker and Buildx** are installed successfully.

### ✅ **Step 3: Restart Docker**
In case Docker isn't running, restart it:
```bash
sudo systemctl restart docker
```




### Run react project by docker:

1. **Rebuild your Spring boot**:

  Got to lifecycle and click on package.

   This will create a `target/` directory containing the production-ready version of your app.

2. **Update your Dockerfile**:

   Ensure your `Dockerfile` copies the `target/` directory into the correct location inside the container. Here's an example of what your Dockerfile might look like:

   ```Dockerfile
    # Use OpenJDK base image
    FROM openjdk:23-jdk-slim
    WORKDIR /app
    
    # Copy JAR file into container
    COPY target/*.jar userservice-0.0.1-SNAPSHOT.jar
    
    # Run the application
    ENTRYPOINT ["java", "-jar", "userservice-0.0.1-SNAPSHOT.jar", "--server.port=8080"]
    

   ```



3.### ✅ **Move project directory in Ubuntu cmd:**

```bash
 cd /mnt/c/reactjs/userservice
```

4. **Rebuild the Docker image**:

   After updating the Dockerfile, rebuild the Docker image by running the following command:
   ```bash
    docker buildx build -t userservice .
   ```

5. **Run the Docker container again**:

   Once the image is rebuilt, run the container again:
   ```bash
   docker run --name snvnv1 -d -p 8080:8080 userservice      // docker run --name attendance1 -d -p 8181:8181 attendance

   ```

6. **Access your app**:

   Your spring service should now be properly served by Nginx and accessible.
