# Use a smaller base image with Node.js
FROM node:14-slim as build

# Set the working directory for the build stage
WORKDIR /app

# Copy package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy the build output
COPY build/ /app/build/

# Use a smaller base image for the production stage
FROM nginx:alpine

# Copy the build output from the build stage to the Nginx web root
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80
