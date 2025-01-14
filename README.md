# Introduction

Collection of useful Dockerfiles for various purposes.

## Usage

- Each folder has a Dockerfile and other files required to build the image.
- To build an image, navigate to the folder and run `docker build -t <image-name> .` (image-name is the name you want to give to the image)
- To run the image, run `docker run --name <container-name> -it <image-name>` (container-name is the name you want to give to the container)
