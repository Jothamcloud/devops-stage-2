# Use an official Node.js runtime as a parent image
FROM node:20.15.0-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files
#COPY package*.json ./

# Install dependencies
#RUN npm install

# Copy the rest of the application code
COPY . /app
RUN npm install
# Build the Vite app
#RUN npm run build

# Check if the build directory exists
#RUN ls -al /app/dist

# Install serve globally
#RUN npm install -g serve

# Make port 5173 available to the world outside this container
EXPOSE 5173

# Serve the application
#CMD ["serve", "-s", "dist"]
CMD [ "npm", "run", "dev", "--", "--host" ]
