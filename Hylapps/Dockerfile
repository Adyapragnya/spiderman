# Use the official Node.js image to build the app
FROM node:16-alpine AS build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json first to leverage Docker cache
COPY package*.json ./

# Install dependencies with the --legacy-peer-deps flag to handle dependency conflicts
RUN npm ci --legacy-peer-deps

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Use a multi-stage build to reduce the final image size
# The final image only needs the built files, so we use a smaller base image (nginx)
FROM nginx:alpine

# Copy the build output from the build stage to the nginx public folder
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 for nginx (default port for serving React app with nginx)
EXPOSE 80

# Use nginx to serve the app
CMD ["nginx", "-g", "daemon off;"]
