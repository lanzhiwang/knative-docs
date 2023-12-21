=== "No DNS"

    If you are using `curl` to access [the sample applications](/docs/getting-started/first-service/), or your own Knative app, and are unable to use the "Magic DNS (sslip.io)" or "Real DNS" methods, there is a temporary approach. This is useful for those who wish to evaluate Knative without altering their DNS configuration, as per the "Real DNS" method, or cannot use the "Magic DNS" method due to using,
    for example, minikube locally or IPv6 clusters.
    如果您使用curl 访问示例应用程序或您自己的Knative 应用程序，并且无法使用“Magic DNS (sslip.io)”或“Real DNS”方法，则可以使用临时方法。 对于那些希望根据“真实 DNS”方法评估 Knative 而不更改其 DNS 配置的人，或者由于使用本地 minikube 或 IPv6 集群而无法使用“魔法 DNS”方法的人来说，这非常有用。

    To access your application using `curl` using this method:

    1. Configure Knative to use a domain reachable from outside the cluster:
      ```bash
      kubectl patch configmap/config-domain \
            --namespace knative-serving \
            --type merge \
            --patch '{"data":{"example.com":""}}'
      ```

    1. After starting your application, get the URL of your application:
      ```bash
      kubectl get ksvc
      ```
      The output should be similar to:
      ```bash
      NAME            URL                                        LATESTCREATED         LATESTREADY           READY   REASON
      helloworld-go   http://helloworld-go.default.example.com   helloworld-go-vqjlf   helloworld-go-vqjlf   True
      ```

    1. Instruct `curl` to connect to the External IP or CNAME defined by the
       networking layer mentioned in section 3, and use the `-H "Host:"` command-line
       option to specify the Knative application's host name.
       For example, if the networking layer defines your External IP and port to be `http://192.168.39.228:32198` and you wish to access the `helloworld-go` application mentioned earlier, use:
       指示curl连接到第3节中提到的网络层定义的外部IP或CNAME，并使用-H“Host：”命令行选项指定Knative应用程序的主机名。 例如，如果网络层将您的外部 IP 和端口定义为 http://192.168.39.228:32198，并且您希望访问前面提到的 helloworld-go 应用程序，请使用：

       ```bash
       curl -H "Host: helloworld-go.default.example.com" http://192.168.39.228:32198
       ```
       In the case of the provided `helloworld-go` sample application, using the default configuration, the output is:
       ```
       Hello Go Sample v1!
       ```
       Refer to the "Real DNS" method for a permanent solution.
