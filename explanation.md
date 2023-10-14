# Explanation of Docker Containerization Project

## Objective 1: Choice of Base Image

For the web application container, I chose the official Node.js image (node:14) as it's compatible with the application's stack.

Dockerfile for the web application container:
```Dockerfile
# Use the official Node.js image
FROM node:14

# Copy the application code to the container
COPY . /app

# Set the working directory
WORKDIR /app

# Install dependencies
RUN npm install

# Expose the application port
EXPOSE 3000

# Start the application
CMD ["npm", "start"]


For the DB application container, I chose the official MongoDB image as the application referenced  Database choice

Dockerfile for the DB application container:

# Use the official MongoDB image
FROM mongo:4.4

# Define a data directory
VOLUME /data/db

# Expose the MongoDB port
EXPOSE 27017

# Start MongoDB
CMD ["mongod"]


