# FROM node:18

# WORKDIR /app

# COPY package*.json ./
# RUN npm install

# COPY src/ ./src

# EXPOSE 5000

# CMD ["npm", "start"]
# =========================
# Stage 1: Build
# =========================
FROM node:18-slim AS builder

WORKDIR /app

# Copy package files and install all dependencies
COPY package*.json ./
RUN npm install

# Copy the source code
COPY src/ ./src

# =========================
# Stage 2: Production image
# =========================
FROM node:18-slim

WORKDIR /app

# Copy only production dependencies from builder
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/src ./src
COPY package*.json ./

EXPOSE 5000

CMD ["npm", "start"]
