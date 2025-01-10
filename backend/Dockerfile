# # Use an official Node.js image as a base
# FROM node:16

# # Set the working directory
# WORKDIR /usr/src/app

# # Copy package.json and package-lock.json
# COPY backend/package*.json ./

# # Install dependencies
# RUN npm install

# # Copy the rest of the app code
# COPY backend/ .

# # Expose the backend port
# EXPOSE 5000

# # Start the server
# CMD ["npm", "run", "dev"]




# Use an official Node.js image as a base
FROM node:16

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the app code
COPY . .

# Expose the backend port
EXPOSE 5000

# Start the server
CMD ["npm", "run", "dev"]
