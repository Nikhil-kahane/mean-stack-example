# ========== STAGE 1: Build Angular App ==========
FROM node:18-slim AS build

WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy full project and build for production
COPY . .
RUN npm run build

# ========== STAGE 2: Serve with Nginx ==========
FROM nginx:1.25-alpine

# Optional: Use your own nginx.conf if routing needed
COPY nginx.conf /etc/nginx/nginx.conf

# Copy build output from the previous stage
COPY --from=build /usr/src/app/dist/client /usr/share/nginx/html

# Expose port and run nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

