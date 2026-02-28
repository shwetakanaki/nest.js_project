# Stage 1: Build the NestJS app
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package definition files and install deps
COPY package*.json ./
RUN npm install

# Copy all source code
COPY . .

# Build the project
RUN npm run build

# Stage 2: Run the app
FROM node:18-alpine

WORKDIR /app

# Copy built files + node_modules
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules

# Environment settings
ENV NODE_ENV=production
ENV PORT=3000

EXPOSE 3000

# Start NestJS
CMD ["node", "dist/main.js"]
