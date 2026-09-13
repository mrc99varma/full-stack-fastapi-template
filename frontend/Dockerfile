# Stage 1: Build the React application
FROM node:20-alpine AS build
WORKDIR /app

# Copy package files
COPY frontend/package.json frontend/package-lock.json* ./
RUN npm install

# Copy source code and build
COPY frontend/ ./frontend/
RUN cd frontend && npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=build /app/frontend/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]