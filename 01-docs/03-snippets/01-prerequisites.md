## Prerequisites

Before installing Knative, you must meet the following prerequisites:

- **For prototyping purposes**, Knative works on most local deployments of Kubernetes. For example, you can use a local, one-node cluster that has 3&nbsp;CPUs and 4&nbsp;GB of memory.
  出于原型设计的目的，Knative 适用于 Kubernetes 的大多数本地部署。 例如，您可以使用具有 3 个 CPU 和 4 GB 内存的本地单节点集群。

    !!! tip
        You can install a local distribution of Knative for development purposes
        using the [Knative Quickstart plugin](/docs/getting-started/quickstart-install/)
        您可以使用 Knative Quickstart 插件安装 Knative 的本地发行版以进行开发

- **For production purposes**, it is recommended that:
  出于生产目的，建议：

    - If you have only one node in your cluster, you need at least 6&nbsp;CPUs, 6&nbsp;GB of memory, and 30&nbsp;GB of disk storage.
      如果集群中只有一个节点，则至少需要 6 个 CPU、6 GB 内存和 30 GB 磁盘存储。

    - If you have multiple nodes in your cluster, for each node you need at least 2&nbsp;CPUs, 4&nbsp;GB of memory, and 20&nbsp;GB of disk storage.
      如果集群中有多个节点，则每个节点至少需要 2 个 CPU、4 GB 内存和 20 GB 磁盘存储。

- You have a cluster that uses Kubernetes v1.27 or newer.
  您有一个使用 Kubernetes v1.27 或更高版本的集群。

- You have installed the [`kubectl` CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
  您已经安装了 kubectl CLI。

- Your Kubernetes cluster must have access to the internet, because Kubernetes needs to be able to fetch images. To pull from a private registry, see [Deploying images from a private container registry](/docs/serving/deploying-from-private-registry/).
  您的 Kubernetes 集群必须能够访问互联网，因为 Kubernetes 需要能够获取图像。 要从私有注册表中拉取，请参阅从私有容器注册表部署映像。

!!! caution
    The system requirements provided are recommendations only. The requirements for your installation might vary, depending on whether you use optional components, such as a networking layer.
    所提供的系统要求仅供参考。 安装要求可能会有所不同，具体取决于您是否使用可选组件（例如网络层）。
