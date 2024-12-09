# Use the official Node.js image as the base
FROM node:16-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to leverage Docker caching
COPY package*.json ./

# Install dependencies using npm ci for faster and deterministic builds
RUN npm ci

# Copy the rest of the application files into the container
COPY . .

# Expose the backend API port (5000)
EXPOSE 5000

# Start the Node.js server
CMD ["npm", "start"]
