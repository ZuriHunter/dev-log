```
/^                                         /^^
/^ ^^                                       /^^
/^  /^^    /^^  /^^   /^^   /^^  /^^ /^^^^ /^/^ /^
/^^   /^^   /^^  /^^ /^^  /^^/^^  /^^/^^      /^^
/^^^^^^ /^^  /^^  /^^/^^   /^^/^^  /^^  /^^^   /^^
/^^       /^^ /^^  /^^ /^^  /^^/^^  /^^    /^^  /^^
/^^         /^^  /^^/^^     /^^   /^^/^^/^^ /^^   /^^
                   /^^
```
#### 2018-08-27
- **Kubernetes**
  - `Resource Requests` specify the minimum amount of a resource required to run the application.
  - 'Resource Limits' specify the maximum amount of a resource that an applciation can consume.
  - resource requests
  ```
  ...
  spec:
    containers:
      - image: gcr.io/kuar-demo/kuard-amd64:1
        name: kuard
        resources:
          requests:
            cpu: "500m"
            memory: "128Mi"
        ports:
          - containerPort: 8080
            name: http
            protocol: TCP
  ```
  - `Resources are requested per container, not per Pod.` The total resources requested by the Pod is the sum of all resources requested by all containers in the Pod.
  - Kubernetes Scheduler will ensure that the sum of all requests of all Pods on a node does not exceed the capcity of the node. (Reuest Limits)
  - CPU reursts are implementd using the `cpu-shares` functionality in the Linux kernel.
  - `When a system runs out of memory, the kubelet terminates containers whose memory usage is greater than the requested memory.`
  ```
  ...
  spec:
    containers:
      - image: gcr.io/kuar-demo/kuard-amd64:1
        name: kuard
        resources:
          requests:
            cpu: "500m"
            memory: "128Mi"
          limits:
            cpu: "1000m"
            memory: "256Mi"
        ports:
          - containerPort: 8080
            name: http
            protocol: TCP
  ```
    - Data with Volumes
      - add it under `spec.volumes` section
      - 
