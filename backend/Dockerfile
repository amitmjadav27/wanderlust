# Stage 1: Build stage
FROM node:21 AS backend-builder

# Set the working directory in the builder image
WORKDIR /app

# Copy package.json and package-lock.json
COPY . .

# Install dependencies (including development dependencies)
RUN npm install

# Copy the rest of the app files into the builder image
COPY . .

# Stage 2: Production stage
FROM node:21-slim

# Set the working directory for the production container
WORKDIR /app

# Copy only the necessary files from the builder stage
COPY --from=backend-builder /app .

COPY .env.docker .env

# Expose the port your application will run on
EXPOSE 5000

# Command to run your app
CMD ["npm", "start"]
