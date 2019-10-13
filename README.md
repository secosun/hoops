# communicator-docker-converter
This repo contains all you need for building Docker containers for CAD file conversion using HOOPS Converter.


#### Configuration
You will need to have docker installed. The reccomended way is to use [docker-install](https://github.com/docker/docker-install).

#### Building
1. Extract your communicator package.
1. Copy the contents of the folder in this repo corresponding to the communicator release into the root directory of the package.
1. Open a new terminal in the root of the package.
1. Run the following command in your terminal: `sudo docker build -t techsoft3d/communicator-converter .`

#### Running
The container is setup to run HOOPS Converter via [xvfb](https://en.wikipedia.org/wiki/Xvfb).

An example invocation would look something like this:
```
sudo docker run --mount type=bind,source=/path/to/host/inputfiles,target=/opt/ts3d/cadfiles --mount type=bind,source=/path/to/host/outputfiles,target=/opt/ts3d/output techsoft3d/communicator-converter --input /opt/ts3d/cadfiles/input_cad_file --output_sc /opt/ts3d/output/output_sc_model --sc_create_scz 1 --sc_compress_scz 0 --output_png /opt/ts3d/output/output.png --license '<your license key>
```

You may append any additional [command line parameters](https://docs.techsoft3d.com/communicator/latest/build/server-command-line-options.html) accepted by HOOPS Converter to your docker run command.
