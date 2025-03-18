# Stage 1: Build stage
FROM node:21 AS backend-builder

# Set the working directory in the builder image
WORKDIR /app

# Copy only package.json and package-lock.json first to install dependencies
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
COPY --from=backend-builder /app /app

# Copy the environment file (make sure this is needed for production)
COPY .env.docker .env

# Install only production dependencies (to make the image leaner)
RUN npm install --only=production

# Expose the port your application will run on
EXPOSE 5000

# Command to run your app
CMD ["npm", "start"]
