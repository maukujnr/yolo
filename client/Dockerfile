# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory to /app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install client-side dependencies
RUN npm install

# Copy the rest of the client application code to the working directory
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Define the command to run the client application
CMD ["npm", "start"]

