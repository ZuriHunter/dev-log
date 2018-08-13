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

#### 2018-08-12
- **Kubernetes**
  - Deployment is usually stored and described in YAML format.
  - `kubectl`  is a command line tool for interacting with the Kubernetes API.  
    - pods
    - replicaSets
    - services
  - `kubectl get componentstatuses` looks at the name, status, message and error of the clusters.
  - **Controller-Manager** is responsible for running various controllers that regulate behavior in the cluster.
  - **Scheduler** is a responsible for placing different pods onto different nodes in the clusters.
  - **etcd** is a server that acts as a storage for the cluster. It tells us where all of the API objects are stored.
  - `kubectl get nodes` list all of the nodes in the cluster.
  - In Kubernetes nodes ares separted into **master** nodes that contain containers like the API server, scheduler, etc., which manage the cluster, and **worker** nodes where your containers will run. (_I wonder if we can make custom changes to the master node_)
  - `kubectl describe` reveals information about each node. Example `kubectl describe nodes NAME_OF_NODE`
  - **Kubernetes Proxy** is responsible for routing network traffic to load-balanced services in the Kubernetes cluster.
    - proxy must be _present_ on every node in the cluster.
    - If proxy is running on the **DaemonSet** to view the proxies run `kubectl get daemonSets --namespace=kube-system kube-proxy`
  - To view Kubernetes DNS `kubectl get services --namespace=kube-system kube-dns`
  - To access Kubernetes UI
    - `kubectl proxy`
    - Go to http://localhost:8001/ui
  - **Namespaces** are used to organize objects in the cluster.  Think of it as a folder.
  - Change defaults like the _namespace_ that can be accomplished within the context file. Path is `$HOME/.kube/config`. The configuration file can store authentication properties for your cluster.
  _Context can also be used to manage different clusters or different users for authenticating to those clusters using the --users or --clusters flag with the set-context command_
    - `kubectl config set-context my-context --namespace=mystuff`
    - `kubectl config use-context my-context`
  - Deployments is a collection of resources and apps
    - A simple deployment would have one Pod.
  - **Pod** is an instance of a docker container.
  - **Deploying An Actual Service to Kubernetes**
    - `kubectl apply -f ./deployment.yaml` to take the yaml file that describes your deployment to kubernetes.
    - Then expose the deployment of your application as a services by running `kubectl expose deployment NAME_OF_SERVICE --type=NodePort`
    - To see the service and where its running locally on your machine using MiniKube `minikube service SERVICE_NAME --url`
  - Kubernetes operate as RESTful resource , i.e. `https://your-k8s.com/api/v1/namespaces/default/pods/my-pod`
  - `kubectl get RESOURCE_NAME` get a listing of all resources in the current _namespace_.
  - To get a specific resource run `kubectl get RESOURCE_NAME
   OBJCT_NAME`
  - To get full information of a resource object pass in the `-o wide` flag
    - View it in yaml format `-o yaml`
    - View it in json format `-o json`
  - **kubectl** uses the JSONPath query language to select fields in the returned object. `kubectl get pods my-pod -o jsonpath --template={.status.podIP}`
    - To get detailed information of the object `kubectl describe RESOURCE_NAME OBJCT_NAME`
  - If you need to edit the yaml file of your service on the fly then run this command `kubectl edit RESOURCE_NAME OBJCT_NAME` it will take the latest and launch an editor for you to make the change.
  - To delete run `kubectl delete RESOURCE_NAME OBJCT_NAME` >>> `kubectl delete -f obj.yaml`
  - **Labeling** and **Annotating** are tags for your objects.
    - Can't overwrite them unless you run the `--overwrite` flag.
  - **Debugging**
    - `kubectl logs POD_NAME` view logs of a running container.
      - tag with a `-f` to continuously see the logs running of the container
    - To log into the container run `kubectl exec -it POD_NAME -- bash`
    - To copy files from local machine to the container (visa-versa) `kubectl cp POD_NAME:/path/to/remote/file /path/to/local/file`
  - Pods = containers
  - Node = instance of all the containers needed to run your application
  - Cluster??
  - Service??
  - *Pod* can hold several containers and they can be in relation to each other.
  - **Pod** represents a collection of application containers and volumes running in the same _execution environment_.
    - The smallest artifact deployed in Kubernetes
    - _All containers of a Pod always land on the same machine_
    - Each Pod runs in its own **cgroup** but they share a number of Linux namespaces.
    - Applications in the _same_ Pod:
      - Share **same** `IP Address` and `Port Space` (Network Namespace)
      - Share `Hostname` (UTS Namespace)
      - Communicate via (Native Interprocess) System V IPC or POSIX. (IPC Namespace)
    - Applications in different pods are _completely_ isolates from each other.
    - Containers in different pods running on the same node might as well be on different servers.
    - There are antipatterns in Pods?
      - It has to be _symbiotic_. Symbiotic means denoting a mutually beneficial relationship between different people or groups.
      - Stay away from applications that use the same scaling procedure.
      - **Ask "Will these containers wrk correctly if they land on different machines?"  If the answer is "no", a Pod is the correct grouping for the containers.  If the answer is "yes", multiple Pods is probably the correct solution** <<< Dont really get it.
      -
- I still don't fully understand what is a _memory leak_
- What is System V IPC? What is POSIX message queues?
