# ===========================================
# Multi-Stage Dockerfile - Frontend (React)
# ===========================================

# Stage 1: Builder
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

RUN npm run build

# Stage 2: Production
FROM node:18-alpine AS production

WORKDIR /app

RUN npm install -g serve

COPY --from=builder /app/build ./build

RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

EXPOSE 3000

CMD ["serve", "-s", "build", "-l", "3000"]