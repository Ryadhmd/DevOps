# TME : Kubernetes 

### Part 1

#### Exercise 1: Understanding Kubernetes Architecture
- **Objective**: Learn about the components of Kubernetes architecture such as Nodes, Pods, Deployments, and Services.
- **Task**: Draw a simple diagram showing the relationship between Nodes, Pods, Deployments, and Services. Explain the role of each component in your own words.

#### Exercise 2: Setting Up Minikube
- **Objective**: Install Minikube and start a local Kubernetes cluster.
- **Task**: Follow the official Minikube installation guide to install Minikube on your machine. Start your Minikube cluster and verify its status using the command line. 
https://kubernetes.io/docs/tasks/tools/


### Part 2 

#### Exercise 1 : Containerize a Simple Web Application

1. Create a simple web application (e.g., a "Hello, World!" app using Node.js, Python Flask, or any other lightweight framework). cf Exersice 1
2. Write a Dockerfile to containerize this application.
3. Build the Docker image and push it to a container registry (e.g., Docker Hub, Google Container Registry).

**Node.js 'Hello, World!' Application:**

- Create a file named app.js:

```javascript
const express = require('express')
const app = express()
const PORT = process.env.PORT || 3000

app.get('/', (req, res) => {
  res.send('Hello, World!')
})

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`)
})
```

- Create a package.json file:

```
{
  "name": "hello-world-app",
  "version": "1.0.0",
  "description": "A simple Node.js app",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

- Dockerfile:

```
# Use an official Node runtime as a parent image
FROM node:18

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the current directory contents into the container at /usr/src/app
COPY . .

# Install any needed packages specified in package.json
RUN npm install

# Make port 3000 available to the world outside this container
EXPOSE 3000

# Define environment variable
ENV NAME World

# Run app.js when the container launches
CMD ["node", "app.js"]
```

#### Exercise 2: Deployment with Kubernetes

**Create a Deployment:**

4. Write a Kubernetes deployment YAML file to deploy your containerized application. Specify the Docker image you pushed to the registry.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world-node
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-world-node
  template:
    metadata:
      labels:
        app: hello-world-node
    spec:
      containers:
      - name: hello-world-node
        image: yourusername/hello-world-node
        ports:
        - containerPort: 3000
```

6. Use kubectl apply -f your_deployment_file.yaml to create the deployment in your cluster.

**Expose Your Application:** 

7. Expose your application to the Internet by creating a Kubernetes service. You can start with a ClusterIP service and then upgrade it to a LoadBalancer or use an Ingress for more advanced scenarios.

```
apiVersion: v1
kind: Service
metadata:
  name: hello-world-node-service
spec:
  selector:
    app: hello-world-node
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
  type: LoadBalancer
```

8. Use kubectl expose deployment your_deployment_name --type=LoadBalancer --name=your_service_name to expose your deployment.

#### Exercise 3: Scaling and Updating

**Scaling the Application:**

9. Scale your deployment to run multiple replicas of your application. Consider the load and how many instances you need to handle it.

10. Use kubectl scale deployment your_deployment_name --replicas=3 to scale your deployment to 3 replicas.

**Updating the Application:**

11. Make a small change to your web application (for example change the message or add a new feature).

12. Rebuild and push the updated Docker image to your container registry. Make sure to update the version tag.

13. Update your deployment to use the new version of your Docker image. This can be done by editing the deployment or using kubectl set image.

#### Exercise 4: Cleanup

**Delete the Deployment and Service:**

14. Ensure you know how to clean up by deleting the deployment and service you created to avoid incurring any costs, especially if you are using a cloud provider.
15. Use kubectl delete deployment your_deployment_name and kubectl delete service your_service_name.

### Part 3 

#### Exercise 1: Deploying Your First Pod
- **Objective**: Learn how to deploy a simple application using Pods.
- **Task**: Deploy a Pod running the `nginx` image and expose it on port 80. Verify the Pod is running and access the application.

#### Exercise 2: Scaling Applications with Deployments
- **Objective**: Understand how to manage application scaling and updates using Deployments.
- **Task**: Create a Deployment that manages a set of Pods running the `nginx` image. Scale the Deployment to run 3 replicas. Update the Deployment to use the `nginx:alpine` image and observe the rolling update process.

#### Exercise 3: Service Discovery and Load Balancing
- **Objective**: Learn how Services enable communication and load balancing between Pods.
- **Task**: Create a Service of type `NodePort` that targets your Nginx Deployment. Verify that you can access the Nginx application through the Service.

#### Exercise 4: Persistent Storage with PersistentVolumes and PersistentVolumeClaims
- **Objective**: Understand persistent storage in Kubernetes.
- **Task**: Create a PersistentVolume backed by local storage and a PersistentVolumeClaim that requests a portion of that volume. Deploy a Pod that uses this claim for storing data.