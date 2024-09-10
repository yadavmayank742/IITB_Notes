# Docker Commands :
> Official [reference](https://docs.docker.com/engine/reference/commandline/container/) for the Docker command-line. 

The general command syntax is `docker <object> <command> <options>`, where 
   
   `<object>` is the type of Docker object you'll be manipulating - `container`, `image`, `network` or `volume` object.
   
   `<command>` indicates the task to be carried out by the daemon, e.g. the `run` command.
   
   `<options>` can be any valid parameter that can override the default behavior of the command, like the `--publish` option for port mapping.

## Container Manipulation :

1. `docker container run <image name>` : this requests the docker daemon to instantiate image `<image name>` .
   
   The instantiated image is called a "container".
   
   This command is same as `docker run <image name>` in versions before `1.13`. 
   
   **IMPORTANT NOTE :** 
	   The order of the options you provide doesn't really matter. 
	   ***BUT*** One thing that you have to keep in mind in case of the `run` command is that the image name ***must come last***. If you put ***anything after the image name then that'll be passed as an argument to the container entry-point*** (check point 18 below) and may result in unexpected situations.
   
2.   `--publish <host port>:<container port>` :  it meant any request sent to `<host port>` of your host system will be forwarded to `<container port>` inside the container‌.
3. To keep a container running in background, you can include the `--detach`, i.e. the container will not stop on closing the terminal.
4. `docker container ls` : to list the **running** containers. The printed `CONTAINER ID` is first 12 characters of the actual `CONTAINER ID` viz actually 64 characters long.
5. `docker container ls --all`: lists all the containers that have run in the past.
6. `--name <container name>` : by default the containers have 2 identifiers - a random 64 character long `CONTAINER ID` and a Randomly generated name of 2 words joined by an underscore; Using `--name` we can name the container as per our wish given that the same name is not assigned to some other container.
7. `docker container rename <container identifier> <new name>` : this renames the container, yields no output on success.
8. `docker container stop <container identifier>` : to stop the container; `container identifier` can be the `CONTAINER ID` or the `NAME`.
   
   The `stop` command shuts down a container gracefully by sending a `SIGTERM` signal. 
   
   If the container doesn't stop within a certain period, a `SIGKILL` signal is sent which shuts down the container immediately.
9. `docker container kill <container identifier>` : used when you want to send a `SIGKILL` signal instead of a `SIGTERM` signal.
10. `docker container start <container identifier>` : stopped containers remain in your system. If you want you can restart them using this command.
11. `docker container restart <container identifier>` : reboot a running container.
    
	NOTE: both the `start` and `restart` are the same in case of a stopped container, but for a running container, `start` has no effect.
12. `docker container create --name <container_name> <image_name>` : creates (and does not RUN) a container from `<image_name>`; this can be run using `docker container start <container_name>`.
13. `docker container rm <container identifier>` : the stopped containers (called *DANGLING* containers) can occupy space in the disk, thus, to remove them from disk, this command is used. Check the containers using `docker container ls -a`, then choose to remove using their identifiers.
    
	Multiple container identifiers can also be provided at once separated by space (no comma.)
14. `docker container prune` : removes ***ALL*** **dangling** containers at once.
15. `docker container run --rm <other options> <image_name>`: this will remove the container as soon as the container is stopped therefore no dangling container created.
16. `docker container run -it <interactive_image>`: some images (such as `ubuntu`, `fedora`, `python` etc...) are configured to run interactively, i.e. they provide some shell like interface, to interact we need `-it` (`-i` for `--interactive` and `-t` for `--tty`.)
    
    Instead of writing `-it` you can be more verbose by writing `--interactive --tty` separately.
17. `--volume <local file system directory absolute path>:<container file system directory absolute path>:<read write access>` or `-v` instead of `--volume`: This is a  bind mount which lets you form a two way data binding between the content of a local file system directory (source) and another directory inside a container (destination).
     
    This way any changes made in the destination directory will take effect on the source directory and vise versa.
18.  The entry point to an executable image is set to the custom program whereas in general it is the shell. Therefore the text after `<image_name>` is treated as shell commands in general.
    
	   Executable images are not that common in the wild but can be very useful in certain cases.

## Image Manipulation :
This is on how to create your own `docker` `images`.
> Use [VS Code](https://code.visualstudio.com/docs/setup/linux) and [Official Docker Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

`Docker Image` is a read-only, **FROZEN** copy of a container, they're the template for creating the `Docker Container`. 

To create a `Docker Image`, one shall have a clear picture of the final state of what the `image` will be.

For the `nmap` image, it shall be running on `Ubuntu`, shall have preinstalled `nmap` and shall update it every time the `container` is initialized. 

`Docker Image` creation instructions are mentioned line by line in a file named `Dockerfile`, each line creates a layer of the image. \[ See blow for **Dockerfile** section to understand important/frequent  instructions\]

1. To build an `image` from `Dockerfile`, run `docker image build .` from the same directory as the `Dockerfile` or you can also specify the path to the `Dockerfile` using `docker build -f <path_to_Dockerfile> .`  \[***NOTE*** : there's a **dot** at the end of both versions of the command]

2. `--tag` can be used to tag an `Docker Image` during `Docker build` command 
	
	Example : `docker image build --tag ubuntu_nmap:latest .`

3. `docker image ls` can be used to list `Docker images` on the system
4. `docker image rm <image identifier>` can be used to remove the image, here `<image identifier>` can be `IMAGE ID` or `image REPOSITORY`.
5. `image prune` command to cleanup all un-tagged dangling images.
6. The `--force` or `-f` option skips any confirmation questions; use the `--all` or `-a` option to remove all cached images in your local registry.
7. To visualize the many layers of an image, you can use the `image history` command.











### Dockerfile :

- Each valid `Dockerfile` starts with a `FROM` instruction which sets the base image, 

	Example: `FROM ubuntu:latest` sets the base as `Ubuntu` and can use all the features such as `apt` package manager.

- `EXPOSE` instructions indicates the port that is to be published as in `--publish` 

	**NOTE:** `EXPOSE` does not mean that we won't have to use the `--publish` option while instantiating the image; we still need it.

	***This instruction is just a documentation for someone who is going to run a container using this image.***

-  `RUN` instruction executes the commands inside the container shell.

	Examples:
	
	`RUN apt-get update && apt-get install nmap -y` command checks for updated package versions and installs NMAP. 
	
	`RUN apt-get clean && rm -rf /var/lib/apt/lists/*` command clears the package cache to remove unnecessary baggage from the image.

	The `RUN` instructions are written in `shell` format , but they can as well be written in `exec` format, as the `CMD` command next. For more on [Shell and Exec form](https://docs.docker.com/reference/dockerfile/#shell-and-exec-form).
	
- `CMD` instruction sets the default command for the image. It is written in `exec` format.

	Example: `CMD [ "/bin/bash", "-c", "cd /var/www/html; python -m http.server 3434" ]`

- `ENV` sets the environment variable in `<key>=<value>` format \[**NO SPACES before and after** `=`\].

	Format : `ENV <key>=<value> ...`
	Example:  `ENV MY_NAME="John Doe"` 
			`ENV MY_NAME="John Doe" MY_DOG=Rex\ The\ Dog  MY_CAT=fluffy`



