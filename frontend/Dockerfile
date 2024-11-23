# Step 1: Use an official Node.js image as the base
FROM node:18-alpine AS builder

# Step 2: Set the working directory
WORKDIR /app

# Step 3: Copy package.json and package-lock.json
COPY package*.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the rest of the application code
COPY . .

# Step 6: Build the Vite app
RUN npm run build

# Step 7: Use a lightweight server to serve the built files
FROM nginx:alpine AS production

# Step 8: Copy the built files to the Nginx HTML directory
COPY --from=builder /app/dist /usr/share/nginx/html

# Step 9: Expose the port the app runs on
EXPOSE 80

# Step 10: Start Nginx
CMD ["nginx", "-g", "daemon off;"]