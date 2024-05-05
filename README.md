# Docker Compose

- You use single YAML file to configure and maintan your application's service.
- With a single command, you create and start all the services from your configuration.
- By Default, Compose sets up a single network for your application.

## Demo 1 Create Network, MongoDB, and Mongo Express Container

```yaml
# mongo-services.yaml
version: '3.8'
services:

  mongodb:
    image: mongo
    ports:
      - 2017:2017
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: supersecret

  mongo-express:
    image: mongo-express
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADNIMPASSWORD: supersecret
      ME_CONFIG_MONGODB_SERVER: mongodb
    depends_on:
      - "mongodb"
```

## Docker Compose Commands

### 1. Execute

```bash
docker-compose -f mongo-services.yaml up
```

- `-f`: Add specific file name.
- `up`: Build, creates and starts the defined containers. It will aggregates the output of each container (like `docker compose logs --folow` does).

### 2. Detached Mode

```bash
docker-compose -f mongo-services.yaml up -d
```

- `-d`: Detached mode, starts containers in the background and leaves them running

### 3. Remove

```bash
docker-compose -f mongo-services.yaml down
```

- `down`: Stop containers and remove containers, networks, volumes and images by "up".

### 4. Start and Stop

```bash
docker-compose -f mongo-services.yaml stop
```

```bash
docker-compose -f mongo-services.yaml start
```

- `start`: Start containers with persistance data.
- `stop`: Stop containers will keep the data.

### 5. Override Project Name

```bash
docker-compose -p projects -f mongo-services.yaml up -d
```

## Dockerize Application Example

1. Open mongo-express From Browser, Login with "admin:pass"

  ```bash
  http://localhost:8081
  ```

2. create `my-db` database, `my-collection` collection and document with {myid: 1, data: "some dynamic data loaded from db"} in mongo-express.

3. Access you nodejs application UI from browser

  ```bash
  http://localhost:3000
  ```

## Sources

- [Source repository](https://gitlab.com/twn-youtube/docker-compose-crash-course)
- [Source youtube video](https://www.youtube.com/watch?v=SXwC9fSwct8)
