# ---------- Build stage ----------
FROM node:18-alpine AS build
WORKDIR /app

# Install deps
COPY package*.json ./
RUN npm ci

# Build app
COPY . .
RUN npm run build

# ---------- Runtime stage ----------
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Copy build output to Nginx HTML folder
COPY --from=build /app/build .

# Optional: custom nginx.conf for SPA routing (React Router)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
