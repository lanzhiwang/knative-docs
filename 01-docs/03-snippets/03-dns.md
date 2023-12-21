You can configure DNS to prevent the need to run curl commands with a host header.
您可以配置 DNS 以防止需要运行带有主机标头的curl 命令。

The following tabs expand to show instructions for configuring DNS.
Follow the procedure for the DNS of your choice:
以下选项卡展开以显示配置 DNS 的说明。
请按照您选择的 DNS 的过程进行操作：

=== "Magic DNS (sslip.io)"

    Knative provides a Kubernetes Job called `default-domain` that configures Knative Serving to use [sslip.io](http://sslip.io) as the default DNS suffix.
    Knative 提供了一个名为 default-domain 的 Kubernetes 作业，它将 Knative Serving 配置为使用 sslip.io 作为默认 DNS 后缀。

    ```bash
    kubectl apply -f {{artifact(repo="serving",file="serving-default-domain.yaml")}}

    kubectl apply -f https://github.com/knative/serving/releases/download/knative-v1.12.3/serving-default-domain.yaml
    ```

    !!! warning
        This will only work if the cluster `LoadBalancer` Service exposes an
        IPv4 address or hostname, so it will not work with IPv6 clusters or local setups
        like minikube unless [`minikube tunnel`](https://minikube.sigs.k8s.io/docs/commands/tunnel/)
        is running.
        仅当集群 LoadBalancer 服务公开 IPv4 地址或主机名时，此功能才有效，因此除非 minikube 隧道正在运行，否则它无法与 IPv6 集群或 minikube 等本地设置一起使用。

        In these cases, see the "Real DNS" or "No DNS" tabs.
        在这些情况下，请参阅“真实 DNS”或“无 DNS”选项卡。
