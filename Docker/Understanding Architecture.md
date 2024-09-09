
```text
                                                                                                                         Enquire the Registry                          
                                           ┌────── Command sent to daemon ──────┐                                     ┌─ if no local image found─┐                     
                                           │                                    │                                     │                          │                     
                                           │                                    │                                     │                          │                     
                                           │                                    │                                     │                          │                     
                                           │        ┌───────────────────┬───────▼───────┬───────────────────┐         │                          │                     
                                           │        │                   │ Docker Daemon─┼──────────┐        │         │                          │                     
                                           │        │                   └───────────────┘          │        │         │          ┌──────┌────────▼────────┐───────┐    
   ┌──────┬───────────────┬──────┐         │        │                                            check      │         │          │      │    Registry     │       │    
   │      │ Docker Client │      │         │        │   identified by the process `dockerd`      image      │         │          │      └─────────────────┘       │    
   │      └───────────────┘      │         │        │                                          availability │         │          │                                │    
   │                             │         │        │   It is responsible to execute the           │        │         │          │   (Can be public or private)   │    
   │                             │         │        │   commands issued from  `Docker Client`      │        │         │          │                                │    
   │   This is the interface     │         │        │                                              │        │         │          │    ┌──────────────────────┐    │    
   │   used to issue commands    │         │        │ ┌┬──────────────────────┬┐  ┌─┬──────────────▼────┬─┐ │         │          │    │                      │    │    
   │   like │docker run ubuntu`  │         │        │ ││It runs the Containers││  │ │ It has the images │ │ │         │          │    │    It has Images     │    │    
   │        └────────────────────┼─────────┘        │ │└──────────────────────┘│  │ └───────────────────┘ │ │         │    ┌─────┼────┼                      │    │    
   │                             │                  │ │                        │  │                       │ │         │    │     │    └──────────────────────┘    │    
   │                             │                  │ │                        │  │    if an image is  ┌──┼─┼─────────┘    │     │              and               │    
   │   Also, this is the       ◄─┼─────Response─────┼─┼────────── Running      │  │   │not found, it   │  │ │              │     │    ┌──────────────────────┐    │    
   │   interface where results   │                  │ │           Container    │  │   │fetches it from │  │ │              │     │    │                      │    │    
   │   are displayed             │                  │ │                 ▲      │  │   │the registry    │  │ │              │     │    │  It has extensions   │    │    
   │                             │                  │ │                 │      │  │   └────────────────┘  │ │              │     │    │                      │    │    
   └─────────────────────────────┘                  │ │                 └──────┼──┼──────local image◄─────┼─┼──────────────┘     │    └──────────────────────┘    │    
                                                    │ └────────────────────────┘  └───────────────────────┘ │                    └────────────────────────────────┘    
                                                    │                                                       │                                                          
                                                    └───────────────────────────────────────────────────────┘                                                          
```


# Docker Commands :
> Official [reference](https://docs.docker.com/engine/reference/commandline/container/) for the Docker command-line. 

0. The general command syntax is `docker <object> <command> <options>`, where 
   
   `<object>` is the type of Docker object you'll be manipulating - `container`, `image`, `network` or `volume` object.
   
   `<command>` indicates the task to be carried out by the daemon, e.g. the `run` command.
   
   `<options>` can be any valid parameter that can override the default behavior of the command, like the `--publish` option for port mapping.

1. `docker container run <image name>` : this requests the docker daemon to instantiate image `<image name>` .
   
   The instantiated image is called a "container".
   
   This command is same as `docker run <image name>` in versions before `1.13`. 
2.   