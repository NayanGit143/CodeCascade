# Step 1: Use Node.js as the base image for building the app
FROM node:16 AS build

# Step 2: Set the working directory in the container
WORKDIR /app

# Step 3: Copy package.json and package-lock.json to install dependencies
COPY package*.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the rest of the Angular app files
COPY . .

# Step 6: Build the Angular app for production
RUN npm run build --prod

# Step 7: Use Nginx to serve the built Angular app
FROM nginx:alpine

# Step 8: Copy the built Angular app from the build stage to the Nginx server's html folder
COPY --from=build /app/dist/angular-16-crud /usr/share/nginx/html

# Step 9: Expose the Nginx default port (80)
EXPOSE 80

# Step 10: Run Nginx to serve the app
CMD ["nginx", "-g", "daemon off;"]
