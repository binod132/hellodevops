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