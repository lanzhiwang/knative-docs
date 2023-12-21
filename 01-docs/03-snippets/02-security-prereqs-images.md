## Verifying image signatures

Knative releases from 1.9 onwards are signed with [cosign](https://docs.sigstore.dev/cosign/overview).
Knative 版本从 1.9 开始使用 cosign 进行签名。

1. Install [cosign](https://docs.sigstore.dev/cosign/installation/) and [jq](https://stedolan.github.io/jq/).
   安装 cosign 和 jq。

2. Extract the images from a manifeset and verify the signatures.
   从清单集中提取图像并验证签名。

```
curl -sSL https://github.com/knative/serving/releases/download/knative-v1.10.1/serving-core.yaml \
  | grep 'gcr.io/' | awk '{print $2}' | sort | uniq \
  | xargs -n 1 \
    cosign verify -o text \
      --certificate-identity=signer@knative-releases.iam.gserviceaccount.com \
      --certificate-oidc-issuer=https://accounts.google.com
```

!!! note
    Knative images are signed in `KEYLESS` mode. To learn more about keyless signing, please refer to
    [Keyless Signatures](https://github.com/sigstore/cosign/blob/main/KEYLESS.md#keyless-signatures)
    Our signing identity(Subject) for our releases is `signer@knative-releases.iam.gserviceaccount.com` and the Issuer is `https://accounts.google.com`
    Knative 图像在 KEYLESS 模式下签名。 要了解有关无密钥签名的更多信息，请参阅无密钥签名。我们的版本的签名身份（主题）是signer@knative-releases.iam.gserviceaccount.com，发行者是https://accounts.google.com
