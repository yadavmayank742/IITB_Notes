
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

1. `docker run <image name>` : this requests the docker daemon to instantiate image \<image name\> 