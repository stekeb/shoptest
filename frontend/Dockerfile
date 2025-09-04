# -----------------------------
# 1. Build stage
# -----------------------------
FROM node:24-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package files first (better caching for dependencies)
COPY package.json package-lock.json* pnpm-lock.yaml* yarn.lock* ./

# Install dependencies (use npm here, or switch to yarn/pnpm if you prefer)
RUN npm install

# Copy the rest of the project
COPY . .

# Build the project
RUN npm run build


# -----------------------------
# 2. Production stage
# -----------------------------
FROM nginx:alpine

# Copy build output to nginx's html folder
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy custom nginx config (optional)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]