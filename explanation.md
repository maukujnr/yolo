# Explanation of a Docker Containerization Project -IP2

## Objective 1: Choice of Base Image

For the web application container, I chose the official Node.js image (node:14) as it's compatible with the application's stack.
I use smaller base images (node:14-slim and node:14-alpine) to reduce the image sizes.

Dockerfile for the web/client application container:
For the client, we copy only the build/ directory to the production image, which contains the compiled output. We will create a separate production build in the first stage and then copy the resulting build files to the second stage

```Dockerfile
# Use an official Node.js runtime as a build environment
FROM node:14-slim as build

# Set the working directory for the build stage
WORKDIR /app

# Copy package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the client application code to the working directory
COPY . .

# Build the client application
RUN npm run build

# Use a smaller base image for the production stage
FROM nginx:alpine

# Copy the build output from the build stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80


For the backend application container, we install only production dependencies and copy only necessary files.
We expose the required ports (80 for the client, 5000 for the backend).
# Use a smaller base image with Node.js
FROM node:14-slim as build

# Set the working directory for the build stage
WORKDIR /app

# Copy package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy the rest of the backend application code
COPY . .

# Use a smaller base image for the production stage
FROM node:14-alpine

# Set the working directory for the production stage
WORKDIR /app

# Copy only the necessary files from the build stage
COPY --from=build /app ./

# Expose the port (adjust to your application's port)
EXPOSE 5000

