FROM ubuntu:24.04

# Install Java and stuff
RUN apt-get update && apt-get install -y \
    openjdk-21-jre unzip wget \
    && rm -rf /var/lib/apt/lists/*

# Do the heavy lifting
WORKDIR /app
RUN wget http://multipaint.kameli.net/multipaint_P4.zip \
    && unzip multipaint_P4.zip \
    && rm multipaint_P4.zip

# DISPLAY for X
ENV DISPLAY=host.docker.internal:0

# Add save disk
RUN mkdir -p /app/savedisk
RUN ln -s /app/savedisk /root/savedisk

# We are done
CMD ["/app/multipaint/linux-amd64/multipaint"]
