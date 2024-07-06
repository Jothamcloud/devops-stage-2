# Stage 1: Build the React app
FROM node:12.22.9-alpine AS build
WORKDIR /app
COPY package.json ./
COPY package-lock.json ./

# Install Git
RUN apk update && apk add git

RUN npm install
COPY . ./
RUN npm run build

# Stage 2: Serve the app using nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
