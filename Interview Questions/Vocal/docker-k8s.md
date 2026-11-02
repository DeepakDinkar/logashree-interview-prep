# 🗣️ Vocal — Docker & Kubernetes (Explain Out Loud)

> Definitions: [`../../Definitions/06-Docker-definitions.md`](../../Definitions/06-Docker-definitions.md) · [`../../Definitions/07-Kubernetes-definitions.md`](../../Definitions/07-Kubernetes-definitions.md)

## Docker 🔥
1. 🟢🔥 `[GEN]` Container vs VM.

    Ans: A container is a lightweight, portable, and self-sufficient unit that encapsulates an application and its dependencies, allowing it to run consistently across different environments. Containers share the host OS kernel and isolate the application processes, making them more efficient in terms of resource usage. A virtual machine (VM), on the other hand, is a full-fledged operating system running on a hypervisor, which abstracts the underlying hardware. VMs are heavier, require more resources, and provide stronger isolation compared to containers.

2. 🟢🔥 `[TCS][CTS]` Image vs container. What is a layer?

    Ans: A Docker image is a read-only template that contains the application code, libraries, dependencies, and configuration needed to run a container. It is built from a series of layers, where each layer represents a set of changes or additions to the filesystem. Layers are stacked on top of each other to form the final image. A container, on the other hand, is a running instance of an image. It is created from an image and provides an isolated environment for the application to execute. Containers can be started, stopped, and deleted without affecting the underlying image.

3. 🟡🔥 `[WMT][INFY]` What is a multi-stage build and why use it?

    Ans: A multi-stage build is a Dockerfile technique that allows you to use multiple `FROM` statements in a single Dockerfile, creating separate build stages. Each stage can have its own base image and set of instructions. The primary purpose of multi-stage builds is to optimize the final image size by allowing you to copy only the necessary artifacts from one stage to another, while discarding unnecessary build dependencies and intermediate files. This results in smaller, more efficient images that are easier to distribute and deploy.

4. 🟡🔥 `[CTS]` CMD vs ENTRYPOINT.

    Ans: Both CMD and ENTRYPOINT are instructions in a Dockerfile that define the command to be executed when a container starts. However, they serve different purposes:
- CMD: The CMD instruction provides default arguments for the container's main process. It can be overridden by specifying a different command when running the container. CMD is typically used to provide default behavior that can be easily overridden.
- ENTRYPOINT: The ENTRYPOINT instruction defines the main command that will always be executed when the container starts. It is not easily overridden, and any arguments provided when running the container will be passed to the ENTRYPOINT command. ENTRYPOINT is often used when you want to ensure that a specific command is always executed, regardless of any additional arguments.

5. 🟡 `[CAPG]` COPY vs ADD.

    Ans: Both COPY and ADD are instructions in a Dockerfile used to copy files and directories from the host machine into the Docker image. However, they have some differences:
- COPY: The COPY instruction is a straightforward command that copies files and directories from the source path on the host machine to the destination path in the Docker image. It does not perform any additional processing or extraction of files.
- ADD: The ADD instruction is more versatile than COPY. In addition to copying files and directories, it can also handle remote URLs and automatically extract compressed files (e.g., .tar, .zip) into the image. However, this added functionality can introduce complexity and potential security risks, so it is generally recommended to use COPY unless you specifically need the features provided by ADD.

6. 🟡🔥 `[CMCST][PP]` How do you reduce Docker image size?

    Ans: To reduce Docker image size, you can follow these best practices:
- Use a minimal base image (e.g., Alpine Linux) to reduce the initial size of the image.
- Remove unnecessary files and dependencies from the image, such as build tools, temporary files, and documentation.
- Use multi-stage builds to separate the build environment from the final runtime environment, copying only the necessary artifacts into the final image.
- Combine multiple RUN commands into a single command to reduce the number of layers in the image.
- Use `.dockerignore` files to exclude unnecessary files and directories from being copied into the image during the build process.
- Optimize the order of instructions in the Dockerfile to take advantage of layer caching and minimize rebuilds.

7. 🟡 `[HEXA]` Volumes vs bind mounts — how do you persist data?

    Ans: In Docker, both volumes and bind mounts are used to persist data, but they have different characteristics:
- Volumes: Volumes are managed by Docker and are stored in a part of the host filesystem that is managed by Docker (usually `/var/lib/docker/volumes/`). They are the preferred way to persist data in Docker because they are easier to manage, can be shared between containers, and provide better isolation from the host filesystem. Volumes can be created and managed using Docker commands, and they can be backed up or migrated easily.
- Bind Mounts: Bind mounts allow you to mount a specific directory or file from the host filesystem into a container. This provides direct access to the host's filesystem, which can be useful for development and testing. However, bind mounts can introduce security risks and may lead to issues with portability, as the container relies on the host's filesystem structure.

8. 🟡 `[ACN]` How do you push an image to ECR?

    Ans: To push a Docker image to Amazon Elastic Container Registry (ECR), follow these steps:
1. **Authenticate Docker to ECR:** Use the AWS CLI to authenticate Docker to your ECR registry. Run the following command, replacing `<region>` with your AWS region and `<account-id>` with your AWS account ID:
```bash
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
```
2. **Tag the Image:** Tag your local Docker image with the ECR repository URI.
```bash
docker tag <local-image>:<tag> <account-id>.dkr.ecr.<region>.amazonaws.com/<repository-name>:<tag>
```
3. **Push the Image:** Push the tagged image to ECR using the following command:
```bash
docker push <account-id>.dkr.ecr.<region>.amazonaws.com/<repository-name>:<tag>
```

9. 🔴 `[PP]` Docker security best practices (non-root, scan, minimal base).

    Ans: Docker security best practices include:
- **Run as Non-Root User:** Avoid running containers as the root user. Create a non-root user in the Dockerfile and use the `USER` instruction to switch to that user.
- **Use Minimal Base Images:** Use minimal base images (e.g., Alpine Linux) to reduce the attack surface and limit the number of vulnerabilities in your container.
- **Scan Images for Vulnerabilities:** Regularly scan your Docker images for known vulnerabilities using tools like Docker Security Scanning, Clair, or Trivy. Address any identified vulnerabilities promptly.
- **Limit Container Capabilities:** Use the `--cap-drop` and `--cap-add` flags to limit the capabilities of your containers, reducing the potential impact of a security breach.
- **Use Read-Only Filesystems:** Mount the container filesystem as read-only whenever possible to prevent unauthorized modifications.
- **Keep Images Updated:** Regularly update your base images and dependencies to ensure that you are using the latest security patches.

10. 🟡 `[LTIM]` EXPOSE vs `-p` port publishing.

    Ans: The EXPOSE instruction in a Dockerfile is used to indicate which ports the container will listen on at runtime. It serves as documentation for users of the image and does not actually publish the ports to the host machine. The `-p` flag, on the other hand, is used when running a container to publish a container's port to the host machine, allowing external access to the application running inside the container. For example, `docker run -p 8080:80 my-image` maps port 80 in the container to port 8080 on the host.

## Kubernetes 🔥
11. 🟢🔥 `[GEN]` What is a Pod? Why not run containers directly?

    Ans: A Pod is the smallest deployable unit in Kubernetes that represents a single instance of a running process in a cluster. It can contain one or more containers that share the same network namespace, storage volumes, and lifecycle. Pods provide an abstraction layer over containers, allowing Kubernetes to manage and orchestrate them effectively. Running containers directly without Pods would limit Kubernetes' ability to manage resources, networking, and scaling, as Pods provide a higher-level construct for grouping and managing related containers.

12. 🟡🔥 `[WMT][PP]` Deployment vs StatefulSet vs DaemonSet.

    Ans: In Kubernetes, Deployment, StatefulSet, and DaemonSet are different types of controllers that manage the lifecycle of Pods:
- **Deployment:** A Deployment is used to manage stateless applications. It ensures that a specified number of replicas of a Pod are running at any given time. Deployments support rolling updates and rollbacks, making them suitable for applications that do not require persistent storage or stable network identities.
- **StatefulSet:** A StatefulSet is used to manage stateful applications that require stable network identities and persistent storage. It provides guarantees about the ordering and uniqueness of Pods, making it suitable for applications like databases and distributed systems that need to maintain state across restarts.
- **DaemonSet:** A DaemonSet ensures that a copy of a Pod runs on all (or a subset of) nodes in the cluster. It is typically used for deploying system-level services, such as log collectors, monitoring agents, or networking components, that need to run on every node.

13. 🟡🔥 `[WMT]` Service types — ClusterIP / NodePort / LoadBalancer.

    Ans: In Kubernetes, Services are an abstraction that defines a logical set of Pods and a policy to access them. There are three main types of Services:
- **ClusterIP:** The default Service type that exposes the Service on a cluster-internal IP. It is only accessible within the cluster and is used for internal communication between Pods.
- **NodePort:** This Service type exposes the Service on a static port on each node's IP address. It allows external traffic to access the Service by sending requests to any node's IP address and the specified port. NodePort is often used for development and testing purposes.
- **LoadBalancer:** This Service type provisions an external load balancer (if supported by the cloud provider) and assigns a public IP address to the Service. It allows external traffic to access the Service through the load balancer, which distributes incoming requests across the available Pods. LoadBalancer is commonly used for production applications that require high availability and scalability.

14. 🟡🔥 `[CTS][PP]` Liveness vs readiness probe.
    
    Ans: In Kubernetes, liveness and readiness probes are used to monitor the health and availability of containers within Pods:
- **Liveness Probe:** A liveness probe checks if a container is still running. If the liveness probe fails, Kubernetes will kill the container and attempt to restart it. This is useful for detecting and recovering from situations where a container is alive but stuck or unresponsive.
- **Readiness Probe:** A readiness probe checks if a container is ready to serve traffic. If the readiness probe fails, the container is removed from the Service's endpoints, preventing it from receiving traffic until it becomes ready again. This is useful for ensuring that only healthy containers receive traffic.

15. 🟡🔥 `[INFY]` ConfigMap vs Secret.

    Ans: In Kubernetes, ConfigMaps and Secrets are used to manage configuration data for applications running in Pods:
- **ConfigMap:** A ConfigMap is an object that allows you to store non-sensitive configuration data in key-value pairs. It can be used to inject configuration settings into Pods, such as environment variables, command-line arguments, or configuration files. ConfigMaps are not encrypted and are suitable for storing non-sensitive information.
- **Secret:** A Secret is an object that allows you to store sensitive information, such as passwords, API keys, or certificates, in a secure manner. Secrets are base64-encoded and can be mounted as files or injected as environment variables into Pods. Kubernetes provides mechanisms to manage and access Secrets securely, ensuring that sensitive data is protected from unauthorized access.

16. 🟡 `[CMCST]` requests vs limits. What is OOMKilled?

    Ans: In Kubernetes, resource requests and limits are used to manage the CPU and memory resources allocated to containers within Pods:
- **Requests:** A request is the amount of CPU or memory that a container is guaranteed to have. Kubernetes uses requests to schedule Pods onto nodes, ensuring that the node has enough resources to accommodate the requested amount. If a container exceeds its requested resources, it may still run, but it may be subject to throttling or eviction if the node runs out of resources.
- **Limits:** A limit is the maximum amount of CPU or memory that a container is allowed to use. If a container exceeds its limit, it may be terminated or throttled by the Kubernetes scheduler. Setting limits helps prevent a single container from consuming excessive resources and affecting the performance of other containers on the same node.
- **OOMKilled:** OOMKilled (Out of Memory Killed) is a status that indicates that a container was terminated by the Kubernetes scheduler because it exceeded its memory limit. When a container is OOMKilled, it means that the container tried to use more memory than was allocated to it, and the system had to kill it to free up memory for other processes.

17. 🔴🔥 `[WMT]` How does a rolling update work? How do you roll back?

    Ans: In Kubernetes, a rolling update is a deployment strategy that allows you to update the Pods in a Deployment gradually, without downtime. During a rolling update, Kubernetes creates new Pods with the updated version of the application while simultaneously terminating the old Pods. This process continues until all the old Pods are replaced with the new ones. The rolling update ensures that a minimum number of Pods are always available to serve traffic, maintaining application availability.
To roll back a deployment, you can use the `kubectl rollout undo` command. This command reverts the Deployment to its previous state, restoring the old Pods and configuration. You can specify the Deployment name and, optionally, the revision number to roll back to a specific version. For example:
```bash
kubectl rollout undo deployment <deployment-name>
```

18. 🔴 `[AMZN]` How does self-healing / HPA work?

    Ans: In Kubernetes, self-healing refers to the ability of the system to automatically detect and recover from failures. The Horizontal Pod Autoscaler (HPA) is a key component that enables self-healing by automatically adjusting the number of Pods in a Deployment or ReplicaSet based on observed metrics, such as CPU utilization or custom metrics. When the HPA detects that the resource usage exceeds a defined threshold, it scales up the number of Pods to handle the increased load. Conversely, when the resource usage drops below the threshold, it scales down the number of Pods to save resources. This dynamic scaling helps maintain application performance and availability while optimizing resource usage.

19. 🔴🔥 `[WMT][PP]` How does a request reach a pod? (Ingress→Service→Pod)

    Ans: In Kubernetes, when a request reaches a Pod, it typically follows this path:
1. **Ingress:** The request first hits the Ingress controller, which is responsible for managing external access to the services in the cluster. The Ingress controller evaluates the incoming request against the defined Ingress rules and determines which Service should handle the request based on the host and path specified in the rules.
2. **Service:** Once the Ingress controller routes the request to the appropriate Service, the Service acts as a load balancer and forwards the request to one of the available Pods that match the Service's selector. The Service maintains a stable IP address and DNS name, allowing clients to access the Pods without needing to know their individual IP addresses.
3. **Pod:** Finally, the request reaches the selected Pod, where the application running inside the container processes the request and generates a response. The response is then sent back through the same path, from the Pod to the Service, and then to the Ingress controller, which forwards it back to the client.

20. 🟡 `[ACN]` What is a namespace? What is RBAC?

    Ans: In Kubernetes, a namespace is a logical partitioning of cluster resources that allows you to organize and manage resources in a multi-tenant environment. Namespaces provide a way to create isolated environments within a single cluster, enabling different teams or projects to work independently without interfering with each other's resources. Each namespace has its own set of resources, such as Pods, Services, and ConfigMaps, and can have its own resource quotas and policies.
RBAC (Role-Based Access Control) is a mechanism for controlling access to Kubernetes resources based on the roles assigned to users or service accounts. RBAC allows you to define roles with specific permissions and bind those roles to users or service accounts within a namespace. This enables fine-grained access control, ensuring that users can only perform actions that are allowed by their assigned roles. RBAC is essential for maintaining security and enforcing least-privilege access in a Kubernetes cluster, especially in multi-tenant environments.

21. 🔴 `[AMZN]` On EKS, how do pods get AWS permissions? (IRSA)

    Ans: In Amazon EKS (Elastic Kubernetes Service), pods can obtain AWS permissions using IAM Roles for Service Accounts (IRSA). IRSA allows you to associate an IAM role with a Kubernetes service account, enabling pods that use that service account to assume the IAM role and gain the associated permissions. The process involves the following steps:
1. **Create an IAM Role:** Create an IAM role in AWS with the necessary permissions for the actions that the pods need to perform. Attach a trust policy that allows the EKS cluster's OIDC provider to assume the role.
2. **Create a Kubernetes Service Account:** Create a Kubernetes service account in the desired namespace and annotate it with the ARN of the IAM role created in the previous step. This annotation allows the service account to assume the IAM role when used by pods.
3. **Deploy Pods with the Service Account:** When deploying pods, specify the service account in the pod's specification. The pods will automatically assume the IAM role associated with the service account, allowing them to access AWS resources with the permissions defined in the IAM role. The AWS SDKs and CLI within the pods will use the temporary credentials provided by the IAM role to authenticate and authorize API requests to AWS services.

22. 🟡 `[LTIM]` What is Helm? Helm vs Kustomize.

    Ans: Helm is a package manager for Kubernetes that allows you to define, install, and manage Kubernetes applications using charts. A Helm chart is a collection of files that describe a related set of Kubernetes resources. Helm simplifies the deployment and management of applications by providing templating, versioning, and dependency management.

---
### ⭐ Your resume line
- "Containerized workloads, removed env-specific issues" → multi-stage Dockerfile + consistent image across dev/prod.
