# communicator-docker
This repo contains all you need for building Docker containers from official HOOPS Communicator Packages.

#### Basic Configuration
You will need to have docker installed. The reccomended way is to use [docker-install](https://github.com/docker/docker-install).

1. Extract your communicator package.
1. Copy the contents of the folder in this repo corresponding to the communicator release into the root directory of the package.
1. Open a new terminal in the root of the package.
1. Build the docker files by running the appropriate commands (see below).

## HOOPS Converter
The container is setup to run HOOPS Converter via [xvfb](https://en.wikipedia.org/wiki/Xvfb) and provide easy conversions out of the box.  To use this container, you will need to bind mount and input and output directories.  Paths in the command line invocation should be valid for the paths inside the container.

#### Building
Run the following command in your terminal: `sudo docker build -t techsoft3d/communicator-converter -f converter.Dockerfile .`

#### Running
An example invocation would look something like this:
```
sudo docker run --mount type=bind,source=/path/to/host/inputfiles,target=/opt/ts3d/cadfiles --mount type=bind,source=/path/to/host/outputfiles,target=/opt/ts3d/output techsoft3d/communicator-converter --input /opt/ts3d/cadfiles/input_cad_file --output_sc /opt/ts3d/output/output_sc_model --sc_create_scz 1 --sc_compress_scz 0 --output_png /opt/ts3d/output/output.png --license '<your license key>
```

You may append any additional [command line parameters](https://docs.techsoft3d.com/communicator/latest/build/authoring-command-line-options.html) accepted by HOOPS Converter to your docker run command.

## CSR Viewer
The container is setup to start the sc streaming server listening for connections on port `55555`.  You should map a host port to this port for your container.  The container is also setup to configure the SC Streaming Server to launch in CSR mode and to search for models in the `/opt/ts3d/models` folder.  You should bind mount a folder containing your models to this path in the container.

#### Building
Run the following command in your terminal: `sudo docker build -t techsoft3d/communicator-csr -f csr.Dockerfile .`

#### Running
An example invocation would look something like this:
```
sudo docker run -p 55555:55555 --mount type=bind,source=/path/to/model/dir,target=/opt/ts3d/models  techsoft3d/communicator-csr --id <your id> --license '<your licence key>'
```

You may append any additional [command line parameters](https://docs.techsoft3d.com/communicator/latest/build/server-command-line-options.html) accepted by the SC Streaming Server to your docker run command.