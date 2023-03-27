## local_registry_in_k8s_cluster
The objective of this project was to provide a user-friendly workspace that would simplify the use of Docker images within our Kubernetes cluster. 
The project offers several benefits, such as centralized management and control of images, storage space management, and version control. Also, since the images are stored locally, it increases the ability to save them and prevents external access. 
The project is reliable thanks to Kubernetes, which ensures automatic repair and maintenance in case of any malfunction, ensuring that the project functions correctly.

## Step by step tutorial
* Before we can use an NFS volume in our Kubernetes deployment, we need to ensure that the server we want to use as the volume allows NFS.
* To access the local registry, we first need to obtain its IP address from the YAML file. This can be done by running the YAML file and then using the "kubectl get   service" command followed by the name of the service (in this case, "registry"). Look for the IP address under the "CLUSTER-IP" column in the output, and take note of it as we will use it to access the local registry.
* To configure the Docker daemon to trust the local registry, we need to create a "daemon.json" file in the Docker directory. Follow these steps to do so:
1. Navigate to the directory where Docker is installed. This directory is typically located in the "etc" directory on the node.
2. In the Docker directory, create a new file called "daemon.json".
3. Open the "daemon.json" file in a text editor.
4. Add the following content to the file:
```
$ {
$    "insecure-registries" : ["cluster-ip:port"]
$ }
```
Replace "cluster-ip:port" with the IP address and port number of your local registry, which you obtained in the previous step.
5. Save and close the "daemon.json" file.
6. The "insecure-registries" parameter in the file allows you to customize the behavior of the Docker daemon on the node and trust the local registry, which doesn't have a valid SSL certificate.
(By following these steps, you should now have the Docker daemon configured to trust the local registry.)

* Now that you have configured the Docker daemon to trust the local registry, you can use it to push, pull, and remove images:
1. Tag the image you want to push with the IP address and port number of the registry service using the following command:
```
$ docker tag image-name:tag cluster-ip:port/image-name:tag
```
(Replace "image-name:tag" with the name and tag of the image you want to push, and "cluster-ip:port" with the IP address and port number of your local registry service.)

2. Push the tagged image to the registry using the following command:
```
$ docker push cluster-ip:port/image-name:tag
```
3. Pull the image from the registry using the following command:
```
$ docker pull cluster-ip:port/image-name:tag
```
4. To see a list of all the images stored in the registry, use the curl command:
```
$ curl -X GET http://cluster-ip:port/v2/_catalog
```
