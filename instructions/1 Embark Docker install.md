# Embark Docker install
We will be installing an [Embark Docker image](https://github.com/embark-framework/embark-docker) that contains all components needed to run Embark and gets us up and running quickly. Alternatively, we could [install Embark](https://embark.status.im/docs/installation.html) globally our machine, or locally in our project. 
## Check your environment
1. Prior to installing the Embark Docker image, please ensure [Docker is installed](https://docs.docker.com/install/) on your machine.
1. Ensure Docker is running on your machine.
2. Start a bash shell (v4+). Please see [bash upgrade instructions](https://github.com/embark-framework/embark-docker/blob/master/macOS-bash4-upgragde.md) for more information.
3. Ensure `docker` is in your `PATH`, alternatively we can alias `docker`: 
```alias docker="/usr/local/bin/docker"```
## Installing Embark Docker
Now that Docker is set up correctly, let's install the Embark Docker image and start a Docker container.
1. To get the Embark Docker image (with Embark v3.2.3), simply run: 
```
EMBARK_DOCKER_TAG=3.2.3
source <(curl -L https://bit.ly/run_embark)
```
2. Now, we can spin up a container using `run_embark <EMBARK COMMAND>` (but don't do this just yet).
