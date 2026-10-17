FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
RUN npm install react-dom@19.1.0 react-native-web @expo/metro-runtime
COPY . .
EXPOSE 8081
ENV CI=1
CMD ["npx", "expo", "start", "--web"]