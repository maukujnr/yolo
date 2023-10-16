# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory to /app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install server-side dependencies
RUN npm install

# Copy the rest of the backend application code to the working directory
COPY . .

# Expose the port the server runs on
EXPOSE 3001

# Define the command to run the backend server
CMD ["npm", "start"]

