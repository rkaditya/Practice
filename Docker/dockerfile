# Use a base image
FROM <base_image>
# Set the working directory in the container
WORKDIR /app
# Copy the necessary files to the container
COPY <app_files> /app
# Expose the desired port
EXPOSE <port_number>
# Define the command to run when the container starts
CMD ["<command_to_start_web_server>"]

################################################
docker build -t my-web-server 
docker run -d -p <host_port>:<container_port> my-web-server
docker run -d -p 80:80 my-nginx-image

########################################
FROM ubuntu:latest

# Set the working directory in the image
WORKDIR /app

# Copy the files from the host file system to the image file system
COPY . /app

# Install the necessary packages
RUN apt-get update && apt-get install -y python3 python3-pip

# Set environment variables
ENV NAME World

# Run a command to start the application
CMD ["python3", "app.py"]

##############################################
# BASE IMAGEWithout Multistage
###########################################

FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

ENTRYPOINT ["/app"]

############################################
With MULTI STAGE BUILD
###########################################

FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

############################################
# HERE STARTS THE MAGIC OF MULTI STAGE BUILD
############################################

FROM scratch

# Copy the compiled binary from the build stage
COPY --from=build /app /app

# Set the entrypoint for the container to run the binary
ENTRYPOINT ["/app"]
