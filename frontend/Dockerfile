# Stage 1: Build the React application
FROM node:20-alpine AS build
WORKDIR /app

# Copy package files into /app
COPY frontend/package.json frontend/package-lock.json* ./
RUN npm install

# Copy all frontend files directly into /app (not a nested frontend folder)
COPY frontend/. .

# Build the app outputting to /app/dist
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]