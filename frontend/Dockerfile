# Multi-stage Dockerfile for React Frontend with Nginx

# Stage 1: Build React application
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package files first for Docker layer caching
COPY frontend/package*.json ./

# Install dependencies
RUN npm ci

# Copy frontend source
COPY frontend/ ./

# Build production application
RUN npm run build


# Stage 2: Nginx production server
FROM nginx:1.25-alpine AS runner

# Remove default Nginx files
RUN rm -rf /usr/share/nginx/html/*

# Copy React production build
COPY --from=builder /app/build /usr/share/nginx/html

# Expose HTTP
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
