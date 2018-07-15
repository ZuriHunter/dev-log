```
```

#### 2018-07-14
- **Kubernetes** is an open-source system for automating deployment, scaling, and management of containerized applications.
  - In Zuri's understanding at the moment, I have a set of docker containers for my application, so if I need to make a whole new set of containers of my application I would Kubernetes to set that up for me automatically. It sounds to be more ideal for production.
- Kubernetes good for:
  - Automatic Binpacking: create containers base of resource usage without jeopardizing the availability of the application
  - Self Healing: removes failed nodes (???) if they didn't pass the routine healthchecks
  - Horizontal Scaling: scales application base on resources like CPU and Memory.
  - Service Discover and Load Balancing: handles the DNS setup for the many clusters of the application. Uses its built in Domain Name Service system.
  - Automated Rollbacks and Rollouts: send out or return back service versions or configurations without adding delays.
  - Secrets and Configuration Management
  - Storage Orchestration: Automatically mount local, external, and storage solutions to the containers in a seamless manner, based on software-defined storage (SDS).
  - Batch Execution
