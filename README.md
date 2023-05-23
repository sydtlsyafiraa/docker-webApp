# Dockerize Web Application

## Steps in dockerize web application

1. Make sure these are install in your machine
```
   apt install docker.io -y
   systemctl start docker
```
2. Create a directory
   mkdir DockerWebApp

Navigate to the directory 
 ``` 
  cd DockerWebApp
```
3. Create index.html file
```
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to My Web</title>
</head>
<body>
    <h1>Hi, welcome to my web!</h1>
</body>
</html> 
```
4. Create Dockerfile 
    nano Dockerfile
```
FROM nginx:latest

# Copy the application files to the appropriate location in the container
COPY . /usr/share/nginx/html

# Expose port 80 for the container
EXPOSE 80

# Start Nginx when the container launches
CMD ["nginx", "-g", "daemon off;"]
```

5. Create Docker Compose file
 nano docker-compose.yml

```
version: '3'
services:
  web:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - '8080:80'
    volumes:
      - .:/usr/share/nginx/html
    deploy:
      resources:
        limits:
          cpus: '0.5'
          memory: '512M'
  ```
6. Build and run docker container
```
 docker-compose up -d
```
7. web app can be access at http://178.128.82.116:8080/
