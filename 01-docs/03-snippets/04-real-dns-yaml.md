=== "Real DNS"

    To configure DNS for Knative, take the External IP
    or CNAME from setting up networking, and configure it with your DNS provider as
    follows:
    要为 Knative 配置 DNS，请从设置网络中获取外部 IP 或 CNAME，并使用您的 DNS 提供商进行配置，如下所示：

    - If the networking layer produced an External IP address, then configure a
      wildcard `A` record for the domain:
      如果网络层生成了外部 IP 地址，则为该域配置通配符 A 记录：

        ```
        # Here knative.example.com is the domain suffix for your cluster
        *.knative.example.com == A 35.233.41.212
        ```

    - If the networking layer produced a CNAME, then configure a CNAME record for the domain:
      如果网络层生成了 CNAME，则为域配置 CNAME 记录：

        ```
        # Here knative.example.com is the domain suffix for your cluster
        *.knative.example.com == CNAME a317a278525d111e89f272a164fd35fb-1510370581.eu-central-1.elb.amazonaws.com
        ```

    - Once your DNS provider has been configured, direct Knative to use that domain:
      配置 DNS 提供商后，指示 Knative 使用该域：

        ```yaml
        # Replace knative.example.com with your domain suffix
        kubectl patch configmap/config-domain \
          --namespace knative-serving \
          --type merge \
          --patch '{"data":{"knative.example.com":""}}'
        ```
