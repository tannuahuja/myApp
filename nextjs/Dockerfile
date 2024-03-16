# Use the official Node.js 14 base image
FROM node:14-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json files
COPY package*.json ./

# Install dependencies
RUN npm install --quiet --no-progress

# Copy the rest of the application code
COPY . .

# Build the Next.js application
RUN npm run build

# Command to start the Next.js application
CMD ["npm", "start"]
