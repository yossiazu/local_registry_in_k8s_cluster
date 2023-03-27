# local_registry_in_k8s_cluster
The objective of this project was to provide a user-friendly workspace that would simplify the use of Docker images within our Kubernetes cluster. 
The project offers several benefits, such as centralized management and control of images, storage space management, and version control. Also, since the images are stored locally, it increases the ability to save them and prevents external access. 
The project is reliable thanks to Kubernetes, which ensures automatic repair and maintenance in case of any malfunction, ensuring that the project functions correctly.

# Step by step tutorial
* Before we can use an NFS volume in our Kubernetes deployment, we need to ensure that the server we want to use as the volume allows NFS.
* To access the local registry, we first need to obtain its IP address from the YAML file. This can be done by running the YAML file and then using the "kubectl get   service" command followed by the name of the service (in this case, "registry"). Look for the IP address under the "CLUSTER-IP" column in the output, and take note of it as we will use it to access the local registry.
* To configure the Docker daemon to trust the local registry, we need to create a "daemon.json" file in the Docker directory. Follow these steps to do so:
1.Navigate to the directory where Docker is installed. This directory is typically located in the "etc" directory on the node.
2.In the Docker directory, create a new file called "daemon.json".
3.Open the "daemon.json" file in a text editor.
4.Add the following content to the file:
