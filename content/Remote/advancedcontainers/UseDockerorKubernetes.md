+++
title = "Use Docker or Kubernetes"
date = 2024-01-13T13:53:43+08:00
weight = 90
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/use-docker-kubernetes](https://code.visualstudio.com/remote/advancedcontainers/use-docker-kubernetes)

# Use Docker or Kubernetes from a container 从容器中使用 Docker 或 Kubernetes



While you can build, deploy, and debug your application inside a dev container, you may also need to test it by running it inside a set of production-like containers. Fortunately, by installing the needed Docker or Kubernetes CLIs and mounting your local Docker socket, you can build and deploy your app's container images from inside your dev container.

​​	虽然您可以在开发容器内构建、部署和调试应用程序，但您可能还需要通过在类似生产环境的容器集中运行应用程序来测试它。幸运的是，通过安装所需的 Docker 或 Kubernetes CLI 并挂载本地 Docker 套接字，您可以从开发容器内构建和部署应用程序的容器映像。

Once the needed CLIs are in place, you can also work with the appropriate container cluster using the [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) extension or the [Kubernetes](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools) extension.

​​	一旦所需的 CLI 到位，您还可以使用 Docker 扩展或 Kubernetes 扩展与相应的容器集群配合使用。

See the following example Dev Container Templates for additional information on a specific scenario. To add them to your project, **open the folder** you want to work with in VS Code and run the **Dev Containers: Add Dev Container Configuration Files...** command in the Command Palette (F1).

​​	有关特定方案的其他信息，请参阅以下示例开发容器模板。若要将它们添加到您的项目，请在 VS Code 中打开您想要处理的文件夹，然后在命令面板 (F1) 中运行“开发容器：添加开发容器配置文件...”命令。

You'll be prompted to pick a pre-defined container configuration from our [first-party and community index](https://containers.dev/templates) in a filterable list sorted based on your folder's contents. From the VS Code UI, you may select one of the Templates described in the sections below.

​​	系统会提示您从我们的第一方和社区索引中选择一个预定义的容器配置，该索引是根据文件夹的内容进行排序的可筛选列表。在 VS Code UI 中，您可以选择下面各部分中描述的其中一个模板。

**Running Docker or Minikube in a development container
在开发容器中运行 Docker 或 Minikube**

- [Docker-in-Docker](https://aka.ms/vscode-remote/samples/docker-in-docker) - Illustrates how to run Docker (or Moby) entirely inside a container. Provides support for bind mounting all folders inside the development container, but cannot reuse your local machine's cache.

  ​​	Docker-in-Docker - 演示如何在容器内完全运行 Docker（或 Moby）。提供对开发容器内所有文件夹进行绑定挂载的支持，但无法重复使用本地计算机的缓存。

- [Kubernetes - Minikube-in-Docker](https://aka.ms/vscode-remote/samples/kubernetes-helm-minikube) - Illustrates how to run Minikube entirely inside a container with similar benefits and limitations as Docker-in-Docker.

  ​​	Kubernetes - Minikube-in-Docker - 演示如何在容器内完全运行 Minikube，其优点和局限性与 Docker-in-Docker 类似。

**Accessing an existing Docker or Minikube instance from a container
从容器访问现有 Docker 或 Minikube 实例**

- [Docker-from-Docker](https://aka.ms/vscode-remote/samples/docker-from-docker) - Also known as "Docker-outside-of-Docker", this illustrates how you can use the Docker (or Moby) CLI in your dev container to connect to your host's Docker daemon by bind mounting the Docker Unix socket. Lower overhead and can reuse your machine's cache, but has [bind mounting limitations](https://code.visualstudio.com/remote/advancedcontainers/use-docker-kubernetes#_mounting-host-volumes-with-docker-from-inside-a-container).

  ​​	Docker-from-Docker - 也称为“Docker-outside-of-Docker”，演示了如何在开发容器中使用 Docker（或 Moby）CLI 通过绑定挂载 Docker Unix 套接字连接到主机的 Docker 守护程序。开销较低，并且可以重复使用计算机的缓存，但存在绑定挂载限制。

- [Docker-from-Docker Compose](https://aka.ms/vscode-remote/samples/docker-from-docker-compose) - Variation of Docker-from-Docker for situations where you are using Docker Compose instead of a single Dockerfile.

  ​​	Docker-from-Docker Compose - Docker-from-Docker 的变体，适用于使用 Docker Compose 而非单个 Dockerfile 的情况。

- [Kubernetes - Local Configuration](https://aka.ms/vscode-remote/samples/kubernetes-helm) - Takes the Docker-from-Docker model and adds kubectl and Helm to illustrate how you can access a local Minikube or Docker provided Kubernetes cluster.

  ​​	Kubernetes - 本地配置 - 采用 Docker-from-Docker 模型并添加 kubectl 和 Helm，以演示如何访问本地 Minikube 或 Docker 提供的 Kubernetes 集群。

There is also documentation on the [Docker-in-Docker](https://github.com/devcontainers/features/tree/main/src/docker-in-docker), [Docker-from-Docker](https://github.com/devcontainers/features/tree/main/src/docker-from-docker), and [Kubernetes](https://github.com/devcontainers/features/tree/main/src/kubectl-helm-minikube) install scripts that you can reuse and are referenced by the samples above.

​​	在上面的示例中引用的 Docker-in-Docker、Docker-from-Docker 和 Kubernetes 安装脚本上还提供了文档，您可以重复使用这些文档。

## [Mounting host volumes with Docker from inside a container 在容器内使用 Docker 挂载主机卷](https://code.visualstudio.com/remote/advancedcontainers/use-docker-kubernetes#_mounting-host-volumes-with-docker-from-inside-a-container)

When following the [Docker-in-Docker](https://aka.ms/vscode-remote/samples/docker-in-docker) model, using the Docker CLI from inside a dev container will cause it to interact with a Docker daemon running in the same place. This means that you can "bind" mount anything inside the dev container into the "inner" containers you create.

​​	按照 Docker-in-Docker 模型，在开发容器内使用 Docker CLI 会导致它与在同一位置运行的 Docker 守护程序进行交互。这意味着您可以将开发容器内的任何内容“绑定”挂载到您创建的“内部”容器中。

For example, this will "just work":

​​	例如，这将“正常运行”：

```
docker run -v /workspace/examplefile.txt:/incontainer/path debian
```

However, if you want to bind mount a host folder available into this inner container, you need to [mount it](https://code.visualstudio.com/remote/advancedcontainers/add-local-file-mount) into your dev container first.

​​	但是，如果您想将可用于此内部容器的主机文件夹绑定挂载，则需要先将其挂载到您的开发容器中。

With [Docker-from-Docker](https://aka.ms/vscode-remote/samples/docker-from-docker), the type of bind mounting that works by default is reversed. Here, the Docker CLI inside the container interacts with the host's Docker daemon instead. This affects mounting directories from inside the container as the path inside the container may not match the path of the directory on the host.

​​	对于 Docker-from-Docker，默认情况下有效的绑定挂载类型是相反的。在此处，容器内的 Docker CLI 与主机的 Docker 守护程序进行交互。这会影响从容器内挂载目录，因为容器内的路径可能与主机上目录的路径不匹配。

The same example above will fail since the path on the host, outside the container isn't `/workspace/...`. In addition, some folders simply cannot be mounted because they only exist in the container. If you need to do this, you may find the Docker-in-Docker model fits your needs better.

​​	由于容器外部的主机上的路径不是 `/workspace/...` ，因此上面的示例将失败。此外，有些文件夹根本无法挂载，因为它们只存在于容器中。如果您需要这样做，您可能会发现 Docker-in-Docker 模型更适合您的需求。

If you are opening a folder in a container, you can pass the host directory into the container as an environment variable to allow you to mount the workspace folder. (This does not, however, work if you used a volume - Docker-in-Docker is the best choice there.) To do so, add the following to `devcontainer.json`:

​​	如果您正在容器中打开一个文件夹，您可以将主机目录作为环境变量传递到容器中，以便您挂载工作空间文件夹。（但是，如果您使用卷，则此方法不起作用 - Docker-in-Docker 是最佳选择。）为此，请将以下内容添加到 `devcontainer.json` ：

```
  "remoteEnv": {
    // Pass in the host directory for Docker mount commands from inside the container
    "HOST_PROJECT_PATH": "${localWorkspaceFolder}"
  }
```

The example below is from a `makefile` and mounts the `KUBECONFIG` file from the development container into the new Docker container it starts:

​​	下面的示例来自 `makefile` ，并将开发容器中的 `KUBECONFIG` 文件挂载到它启动的新 Docker 容器中：

```
docker run -p 8089:8089 -p 9090:9090 -v $(shell echo ${KUBECONFIG} | sed s#/workspace#${HOST_PROJECT_PATH}#):/kubeconfig.json -e KUBECONFIG=/kubeconfig.json ${IMG} -f behaviours/run_submit_locust.py
```

