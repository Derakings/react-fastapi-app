# This Dockerfile creates a multi-stage build for a React finance application.

# The first stage uses a Node.js Alpine image to build the React app.
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# The second stage uses an Nginx Alpine image to serve the built React app.
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

