FROM node:18-alpine
WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Build the frontend
COPY . .
RUN npm run build

# Serve the app
EXPOSE 3000
CMD ["npm", "start"]
