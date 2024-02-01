# Dockerfiles for the Talmo Lab

This repository hosts a collection of Dockerfiles used for various projects in the Mcvicker Lab. Each Dockerfile is organized into its own directory, allowing for easy navigation and isolation of different container builds.

## Repository Structure

The repository is structured with each Dockerfile and its related files in separate directories. This allows for clarity and modular management of different Docker containers. The general folder structure is as follows:

- `/container1`: Docker setup for the first container
- `/container2`: Docker setup for the second container
- `...`

## Getting Started

To get started with building and deploying these Docker containers, follow the steps below:

### Building a Docker Image

1. Navigate to the directory containing the Docker setup for the container you want to build:
    ```
    cd <directory containing the Docker setup you want>
    ```

2. Build the Docker image:
    ```
    docker build -t <your docker hub username>/<whatever_name_you_want> .
    ```

### Pushing to Docker Hub

1. If you haven't logged into Docker Hub yet, do so with the following command:
    ```
    docker login
    ```

2. Push the built image to your Docker Hub container repository:
    ```
    docker push <your docker hub username>/<the same name from before>
    ```

### Accessing the Container

Once the container image is pushed to Docker Hub, it should be accessible from RunAI or any other container orchestration platform that you use.

## Contribution Guidelines

If you wish to contribute to this repository, please follow the guidelines outlined below:

1. Ensure that your Dockerfile is well-documented and follows best practices.
2. Provide a clear and concise README in the directory of your Dockerfile, explaining what it does and how to use it.
3. Submit a pull request with a detailed explanation of the changes and improvements made.

## Support and Issues

If you encounter any problems or have questions, feel free to open an issue in this repository. Please provide as much detail as possible to help us understand and address your concerns.

---

This repository is maintained and managed by the McVicker Lab team. Contributions and feedback are always welcome. Inspired from Talmo Periera Docker Github page. 
