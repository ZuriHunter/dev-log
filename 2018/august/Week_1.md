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

#### 2018-08-01
- Kubernetes
  - **Google Cloud SDK**
    - For some reason it wants python 2.7 and I have to install it as a tar file...why can't I get it from Brew.
    - Ran `/google-cloud-sdk/install.sh` and `gcloud init` to sign. Choose my existing project testingwithkubes
    - Tried spinning up a cluster with `gcloud container clusters create kuar-cluster` and got a 403 so I don't have access to this service within the CLI.
    ```
    ERROR: (gcloud.container.clusters.create) ResponseError: code=403, message=Google Compute Engine: Access Not Configured. Compute Engine API has not been used in project 736709458116 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/compute.googleapis.com/overview?project=736709458116 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.
    ```
      - Kind of not understanding what a cluster would be in this context
  - **Microsoft Azure SDK**
    - Azure sdk can be installed via brew `brew update && brew install azure-cli`
    - `az login` to sign into your Azure account
      - `No subscriptions were found for 'None'. If this is expected, use '--allow-no-subscriptions' to have tenant level accesses`
        - Apparently you got to subscribe to their services first before you can do anything ($$$)
    - `az group create --name=kuar --location=westus ` This creates the resource group **kuar** under the location of **westus**
    - `az acs create --orchestrator-type=kubernetes --resource-group=kuar --name=kuar-cluster` This is to create the cluster but got this python error
    ```
    No module named '_cffi_backend'
    Traceback (most recent call last):
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/knack/cli.py", line 197, in invoke
        cmd_result = self.invocation.execute(args)
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/azure/cli/core/commands/__init__.py", line 262, in execute
        self.commands_loader.load_arguments(command)
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/azure/cli/core/__init__.py", line 253, in load_arguments
        self.command_table[command].load_arguments()  # this loads the arguments via reflection
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/azure/cli/core/commands/__init__.py", line 141, in load_arguments
        super(AzCliCommand, self).load_arguments()
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/knack/commands.py", line 76, in load_arguments
        cmd_args = self.arguments_loader()
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/azure/cli/core/__init__.py", line 440, in default_arguments_loader
        op = handler or self.get_op_handler(operation)
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/azure/cli/core/__init__.py", line 485, in get_op_handler
        op = import_module(mod_to_import)
      File "/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/importlib/__init__.py", line 126, in import_module
        return _bootstrap._gcd_import(name[level:], package, level)
      File "<frozen importlib._bootstrap>", line 994, in _gcd_import
      File "<frozen importlib._bootstrap>", line 971, in _find_and_load
      File "<frozen importlib._bootstrap>", line 955, in _find_and_load_unlocked
      File "<frozen importlib._bootstrap>", line 665, in _load_unlocked
      File "<frozen importlib._bootstrap_external>", line 678, in exec_module
      File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/azure/cli/command_modules/acs/custom.py", line 36, in <module>
        from azure.cli.command_modules.acs import acs_client, proxy
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/azure/cli/command_modules/acs/acs_client.py", line 12, in <module>
        import paramiko
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/paramiko/__init__.py", line 22, in <module>
        from paramiko.transport import SecurityOptions, Transport
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/paramiko/transport.py", line 57, in <module>
        from paramiko.ed25519key import Ed25519Key
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/paramiko/ed25519key.py", line 17, in <module>
        import bcrypt
      File "/usr/local/Cellar/azure-cli/2.0.43/libexec/lib/python3.7/site-packages/bcrypt/__init__.py", line 25, in <module>
        from bcrypt import _bcrypt
    ModuleNotFoundError: No module named '_cffi_backend'
    ```
  - Solved by running `brew link --overwrite python3`
  - Another error after trying to create the cluster
    ```
    Deployment failed. Correlation ID: 61784043-c640-48f1-a950-12198f039f0d. {
      "error": {
        "code": "QuotaExceeded",
        "message": "Provisioning of resource(s) for container service 'kuar-cluster' in resource group 'kuar' failed.\nMessage: 'Operation results in exceeding quota limits of Core. Maximum allowed: 4, Current in use: 0, Additional requested: 8. Please read more about quota increase at http://aka.ms/corequotaincrease.'.\nDetails: ''"
      }
    }
    ```

#### 2018-08-02
- **PyxelEdit**
  - A little but of a more advanced interface. 
