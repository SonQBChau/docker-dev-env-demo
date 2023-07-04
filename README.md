# docker-dev-env-demo

Example used to try a Compose application with Docker Dev Environments.

This example is based on the `react-express-mysql` sample of [`awesome-compose` repository](https://github.com/docker/awesome-compose/).

## Compose sample application
React application with a NodeJS backend and a MySQL database

Project structure:
```
.
├── backend
│   ├── Dockerfile
│   ...
├── db
│   └── password.txt
├── compose.yaml
├── frontend
│   ├── ...
│   └── Dockerfile
└── README.md
```

[_.docker/docker-compose.yaml_](.docker/docker-compose.yaml)
```
services:
  backend:
    build: backend
    ports:
      - 80:80
      - 9229:9229
      - 9230:9230
    ...
  db:
    # We use a mariadb image which supports both amd64 & arm64 architecture
    image: mariadb:10.6.4-focal
    # If you really want to use MySQL, uncomment the following line
    #image: mysql:8.0.27
    ...
  frontend:
    build: frontend
    ports:
    - 3000:3000
    ...
```
The compose file defines an application with three services frontend, backend and db. When deploying the application, docker compose maps port 3000 of the frontend service container to port 3000 of the host as specified in the file. Make sure port 3000 on the host is not already being in use.
