# Stage 1: Build stage
FROM node:21 AS frontend-builder

# Set the working directory in the builder image
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies (including development dependencies)
RUN npm install

# Copy the rest of the app files into the builder image
COPY . .

# Stage 2: Production stage
FROM node:21-slim

# Set the working directory for the production container
WORKDIR /app

# Copy only the necessary files from the builder stage
COPY --from=frontend-builder /app .

COPY .env.docker .env.local

# Expose the port your application will run on
EXPOSE 5173

# Define the default command to run the application in development mode
CMD ["npm", "run", "dev", "--", "--host"]
