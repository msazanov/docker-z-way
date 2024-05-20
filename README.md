# Docker Z-Way

This project provides a Docker container for running Z-Way, the smart home controller software by Z-Wave.Me, on x64.

## Quick Start

### Prerequisites
Ensure Docker is installed on your system. Refer to the official Docker documentation for installation instructions:
- [Install Docker on Linux](https://docs.docker.com/engine/install/)
- [Install Docker on Mac](https://docs.docker.com/docker-for-mac/install/)
- [Install Docker on Windows](https://docs.docker.com/docker-for-windows/install/)

### Running the Container

1. Create a directory for the Z-Way server and navigate into it:
    ```sh
    mkdir z-way-server
    cd z-way-server
    ```

2. Run the following command to start the Z-Way container:

#### Linux & Mac
    ```sh
    docker run -d -it \
        --name z-way-server \
        --device=/dev/ttyUSB0 \
        --device=/dev/ttyUSB1 \
        -p 8083:8083 \
        -v "$(pwd)/data:/data" \
        ghcr.io/z-wave-me/docker-z-way:latest
    ```

#### Windows
    ```sh
    docker run -d -it `
        --name z-way-server `
        --device=/dev/ttyUSB0 `
        --device=/dev/ttyUSB1 `
        -p 8083:8083 `
        -v "${PWD}/data:/data" `
        ghcr.io/z-wave-me/docker-z-way:latest
    ```

### Viewing Logs
To view the logs of the running container in real-time:
    ```sh
    docker logs -f z-way-server
    ```

### Stopping and Removing the Container
To stop the container:
    ```sh
    docker stop z-way-server
    ```

To remove the container:
    ```sh
    docker rm z-way-server
    ```

## Using Docker Compose

For users who prefer Docker Compose, follow these steps:

### Clone the Repository
Clone the repository and navigate to the project directory:
    ```sh
    git clone https://github.com/msazanov/docker-z-way.git
    cd docker-z-way
    ```

### Configuration
Ensure the `docker-compose.yml` file is correctly configured for your devices. You can specify multiple devices such as Z-Wave, ZigBee, EnOcean, or Z-Station (Z-Wave + Zigbee USB station):

    ```yaml
    services:
      z-way-server:
        build:
          context: .
        container_name: z-way-container
        devices:
          - /dev/ttyUSB0:/dev/ttyUSB0 # For Z-Wave UZB Stick or Z-Station
    #      - /dev/ttyUSB1:/dev/ttyUSB1 # For additional interface like a Z-Station or ZigBee stick
        ports:
          - "8083:8083"
        volumes:
          - ./data:/data
        restart: unless-stopped
    ```

### Running the Container
To build and start the container:
    ```sh
    docker compose up -d
    ```

### Viewing Logs
To view logs in real-time:
    ```sh
    docker logs -f z-way-container
    ```

### Stopping the Container
To stop the container:
    ```sh
    docker compose down
    ```

## Building from Source

For users who want to build the Docker image from the source, follow these steps:

### Clone the Repository
Clone the repository and navigate to the project directory:
    ```sh
    git clone https://github.com/msazanov/docker-z-way.git
    cd docker-z-way
    ```

### Building the Image
Build the Docker image:
    ```sh
    docker compose build
    ```

### Running the Container
Start the container using Docker Compose:
    ```sh
    docker compose up -d
    ```

### Viewing Logs
To view logs in real-time:
    ```sh
    docker logs -f z-way-container
    ```

### Stopping the Container
To stop the container:
    ```sh
    docker compose down
    ```

For more detailed instructions, troubleshooting, and updates, visit the [GitHub repository](https://github.com/msazanov/docker-z-way).
