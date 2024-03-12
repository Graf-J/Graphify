# Graphify ♾️
Developed by: <b>Johannes Graf</b>

## Getting started
### 1) Clone the repository including the submodules:
```bash
$ git clone --recurse-submodules https://github.com/Graf-J/Graphify.git
```

### 2) Navigate into the project directory:
```bash
$ cd Graphify
```
#### 2.1) To keep the project with the submodules up to date, run the following command:
```bash
$ git pull --recurse-submodules
```

### 3) Mount the output directory:
In the <b>docker-compose.yaml</b> file located in the root directory of the project, update the volume <b>C:\Users\Johannes\Programming\GraphifyProjects</b> to point to the directory in your filesystem where you want the software to place the generated projects.

```dockerfile
version: '3'
services:
  generator-service:
    container_name: 'Generator-Service'
    build: ./backend
    ports:
      - "8000:8000"
    volumes:
      - graphify-project-volume:/app/projects
      - C:\Users\Johannes\Programming\GraphifyProjects:/app/outputs

  ui:
    container_name: 'Graphify-UI'
    build: ./frontend
    ports:
      - "3000:3000"
    depends_on:
      - generator-service

volumes:
  graphify-project-volume:
```

### 4) Run Graphify:
```bash
$ docker-compose up --build
```
#### 4.1) Access the Swagger documentation of the API via http://localhost:8000
#### 4.2) Access the Web UI via http://localhost:3000

### 5) Run a generated Project
After building your first project a new folder appears in the directory specified in the docker-compose.yaml file. To run this project, navigate into the projects directory:
```bash
$ cd <project-name>
```
And run the project:
```bash
$ docker-compose up --build
```
#### 5.1) Access the GraphiQL web interface via http://localhost:5000/graphql. Replace the port of the URL with the port specified when building the project previously.