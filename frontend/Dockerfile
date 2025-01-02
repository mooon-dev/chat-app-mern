# Use an official Node.js image as a base
FROM node:16

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
# COPY frontend/package*.json ./
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the app code
COPY frontend/ .

# Build the React app
RUN npm run build

# Install a lightweight web server to serve the app
RUN npm install -g serve

# Expose the frontend port
EXPOSE 3000

# Start the server
CMD ["serve", "-s", "build", "-l", "3000"]
