# Stage 1: Build Stage
FROM node:21 AS frontend-builder

WORKDIR /app

# Copy the package.json and package-lock.json first to take advantage of Docker cache
COPY package*.json ./

# Install Dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Stage 2: Production Stage
FROM node:21-slim

WORKDIR /app

# Copy only the necessary files from the build stage
COPY --from=frontend-builder /app .

# Copy the environment file to the production environment
COPY .env.docker .env.local

# Expose the necessary port
EXPOSE 5173

# Command to run the application in development mode with host binding
CMD ["npm", "run", "dev", "--", "--host"]