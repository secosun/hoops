# communicator-docker
This repo contains all you need for building Docker containers from official HOOPS Communicator Packages.

## Basic Configuration
You will need to have docker installed. The reccomended way is to use [docker-install](https://github.com/docker/docker-install). 
Add your user is to the docker group by using the following command:
```
sudo usermod -aG docker <your user name> 
```
Note that you may need to log out and back in for changes to take effect. 

Once docker is installed the following steps can be used to build communicator images: 

1. Extract your communicator package.
1. Copy the contents of the folder corresponding to your communicator version into the root of the package.
1. Open a new terminal in the root of the package.
1. Build the docker files by running the appropriate commands (see below).
