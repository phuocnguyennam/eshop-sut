FROM node:20-alpine
WORKDIR /app
# Install build tools needed for sqlite3 native addon compilation
RUN apk add --no-cache python3 make g++
COPY package*.json ./
RUN npm install
COPY . .
# Seed dữ liệu ban đầu và khởi động server
CMD sh -c "node database.js && node server.js"