# hellodevops
Setting up a demo project for DevOps involving a sample application, Jenkins for CI/CD, and Helm for Kubernetes deployment involves several steps.

## Create Simple "Hello World" web application written in Node.js and Dockerize it.
1. Create a Node.js Application:
Create a directory for your project and navigate into it:
```
mkdir helloapp
cd helloapp
```
2. Create a file named app.js with the following content:
```
const http = require('http');

const hostname = '0.0.0.0';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World!\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```
2. Create package.json
```npm init -y```
3.  Create a Dockerfile:
Create a file named Dockerfile in the same directory as your app.js file with the following content:
```
# Use the official Node.js image
FROM node:14

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
ls


# Install application dependencies
RUN npm install

# Copy application code to the working directory
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Command to run the application
CMD [ "node", "app.js" ]
```
4. Build the Docker Image
```docker build -t nodejs-hello-world .```
Note: Check your Docker Desktop is running
5. Run the Docker Container
```docker run -p 3000:3000 -d nodejs-hello-world```
6. Test the Application.
```http://localhost:3000```

## Jenkins Configuration:
### Install Jenkins (ubuntu)
1. Update Package Index
```
sudo apt update
```
2. Install Java
```sudo apt install openjdk-11-jdk
```
3. Add Jenkins Repository Key
```wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```
4. Add Jenkins Repository
```sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```
5. Install Jenkins
```
sudo apt update
sudo apt install jenkins
```
6. Start Jenkins Service
```
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
7. Access Jenkins
```http://localhost:8080```
8. Unlock Jenkins.
During the first visit, Jenkins will ask you to unlock it using an initial admin password. You can find this password in the Jenkins log file:
```sudo cat /var/log/jenkins/jenkins.log | grep "initialAdminPassword"
```
if not present
```sudo cat /var/lib/jenkins/secrets/initialAdminPassword```