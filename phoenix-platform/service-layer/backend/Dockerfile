# Base image for Node.js
FROM node:16-alpine

# Set working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy all source files
COPY . .

# Expose port and start the app
EXPOSE 3000
CMD ["node", "app.js"]
