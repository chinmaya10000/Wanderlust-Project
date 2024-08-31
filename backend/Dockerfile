# Stage 1: Build Stage
FROM node:21 AS backend-builder

WORKDIR /app 

# Copy the package.json and package-lock.json first to take advantage of Docker cache
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Stage 2: Production Stage
FROM node:21-slim

# Copy only the necessary files from the build stage
COPY --from=backend-builder /app .

# Copy the environment file
COPY .env.docker .env

# Expose the application port
EXPOSE 8080

# Start the application
CMD ["npm", "start"]
