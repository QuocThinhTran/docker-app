# Stage 1: Build React app
FROM node:18 AS build
WORKDIR /app

# Copy file cấu hình trước để cache npm install
COPY package*.json ./

# Cài dependencies
RUN npm install

# Copy toàn bộ source code
COPY . .

# Build app
RUN npm run build

# Stage 2: Serve bằng Nginx
FROM nginx:stable-alpine
WORKDIR /usr/share/nginx/html

# Xoá default file Nginx
RUN rm -rf ./*

# Copy kết quả build từ stage trước
COPY --from=build /app/build .

# Expose port
EXPOSE 80

# Chạy nginx ở foreground
CMD ["nginx", "-g", "daemon off;"]
