# Multipaint-container

This is a simple Docker container that allows you to run [Multipaint](http://multipaint.kameli.net/) on macOS by encapsulating the application and its dependencies. XQuartz is used to display the GUI.

![Multipaint 2024.1](https://i.imgur.com/xtJLSRs.png)

## Prerequisites

- [Docker](https://docs.docker.com/engine/install/)

- [XQuartz](https://www.xquartz.org/): after installation, enable "Allow connections from network clients" in the XQuartz security settings and reboot your machine to apply the changes, finally type xhost +localhost in your terminal to allow connections from localhost. Further instructions can be found [here](https://gist.github.com/sorny/969fe55d85c9b0035b0109a31cbcb088).



## Quick start
Remember to run (if needed)
```bash
xhost +localhost
```

### Use image from Docker Hub ###

1. **Pull the Docker image**
```bash
docker pull tznurmin/multipaint:2024.1p4
```

Now you have the container image. In order to load and save your work, you'll mount a directory inside your filesystem. A directory named _temp_ is used in this example: use mkdir _name_of_your_directory_ in terminal to create one.

2. **Run the container and mount temp from your current working directory**
```bash
docker run --rm \
           -e DISPLAY=host.docker.internal:0 \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -v "$(pwd)/temp:/app/savedisk" \
           --name multipaint-container \
           tznurmin/multipaint:2024.1p4
```


## Or build your own ##

1. **Clone the repository**
```bash
git clone https://github.com/tznurmin/multipaint-container.git
```

2. **Build the image**
```bash
cd multipaint-container/df && docker build -t multipaint .
```

3. **Run the container**
```bash
docker run --rm \
           -e DISPLAY=host.docker.internal:0 \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -v "$(pwd)/temp:/app/savedisk" \
           --name multipaint \
           multipaint
```
Remember to create a directory (e.g. temp) for your images.

## Troubleshooting

1. **Can't connect to X11 window server using 'host.docker.internal:0' as the value of the DISPLAY variable.**
![Troubleshooting_1](https://i.imgur.com/B2b0YIo.png)
Fix it by allowing the connections from localhost
```bash
xhost +localhost
```
