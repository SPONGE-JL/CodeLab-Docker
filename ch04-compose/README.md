# Docker Compose

## Build Docker Image

```bash
# Build
docker image build -f dockerfile-go-app -t my-go-app .

  # === RESULT ===
  # Sending build context to Docker daemon   5.12kB
  # Step 1/4 : FROM golang:1.9
  #  ---> ef89ef5c42a9
  # Step 2/4 : RUN mkdir /echo
  #  ---> Running in c7a9c10f344a
  # Removing intermediate container c7a9c10f344a
  #  ---> cb5db5925c61
  # Step 3/4 : COPY main.go /echo
  #  ---> b0957155c753
  # Step 4/4 : CMD ["go", "run", "/echo/main.go"]
  #  ---> Running in 0ed8602bc2f3
  # Removing intermediate container 0ed8602bc2f3
  #  ---> 56ffa50695bd
  # Successfully built 56ffa50695bd
  # Successfully tagged my-go-app

# Check
docker image ls

  # REPOSITORY    TAG       IMAGE ID       CREATED              SIZE
  # my-go-app     latest    50c3ed52c425   About a minute ago   750MB
```

## Compose from Local Docker Image

`docker compose` can make multi-container to start on once with dependencies.

```bash
# COMPOSE UP
docker compose up -d
  # === RESULT ===
  # Creating network "step-1-compose_default" with the default driver
  # Creating step-1-compose_echo_1 ... done

# CHECK-1
docker container ls

# CHECK-2
curl -fsSL http://localhost:9000
  # === RESULT ===
  # Hello Docker!!

# COMPOSE DOWN
docker compose down
  # === RESULT ===
  # Stopping step-1-compose_echo_1 ... done
  # Removing step-1-compose_echo_1 ... done
  # Removing network step-1-compose_default
```

## Compose with building image

```bash
# COMPOSE UP WITH BUILDING
docker compose up -d --build
```
