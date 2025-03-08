1. Create a Dockerfile
Inside your project folder, create a file named Dockerfile (no extension) and add the following content:

# Use Node.js as the base image
FROM node:20-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json first (for better caching)
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the project files
COPY . .

# Expose port 3000 for the React app
EXPOSE 3000

# Start the React development server
CMD ["npm", "start"]
2. Create a .dockerignore File
To keep the image clean and prevent unnecessary files from being copied, create a .dockerignore file inside your project folder and add:

node_modules
build
.dockerignore
.git
.gitignore
3. Build and Run the Docker Container
Step 1: Build the Docker Image
Run the following command inside your project folder:

docker build -t my-react-app .
Step 2: Run the React App in Docker
docker run -p 3000:3000 -v $(pwd):/app -w /app my-react-app
Now, open http://localhost:3000 in your browser.

4. Why Use This Approach?
Easier to manage → No need to type long commands every time.
Consistent setup → Anyone can build and run the app with Docker.
Modular approach → Easily extendable for production and CI/CD.

5. Troubleshooting
Port 3000 is already in use? Run:

docker ps  # Find running containers
Then stop the container using:

docker stop <container_id>
Alternatively, run the app on a different port:

docker run -p 3001:3000 my-react-app
