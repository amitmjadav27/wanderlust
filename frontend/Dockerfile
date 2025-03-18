# Stage 1: Build stage
FROM node:21 AS frontend-builder

# Set the working directory in the builder image
WORKDIR /app

# Copy package.json and package-lock.json to install dependencies early
COPY package*.json ./

# Install dependencies (including development dependencies)
RUN npm install

# Copy the rest of the app files into the builder image
COPY . .

# Build the frontend app (Assuming it's a build step like for React/Vue/etc.)
RUN npm run build

# Stage 2: Production stage
FROM node:21-slim

# Set the working directory for the production container
WORKDIR /app

# Copy the necessary files from the builder stage
COPY --from=frontend-builder /app /app

# Copy the environment variables file (make sure this is required for production)
COPY .env.docker .env.local

# Expose the port your application will run on
EXPOSE 5173

# Set the CMD to serve the production build instead of running in development mode
CMD ["npm", "run", "preview", "--", "--host"]
