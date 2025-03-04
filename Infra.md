# Preparation of cluster

## Create kind cluster

create kind cluster by runing comand:

```zsh
kind create cluster --wait 120s --config=infra/cluster.yaml
```

## Install cert-manager

```zsh
helm install cert-manager cert-manager \
  --repo https://charts.jetstack.io \
  --version 1.11.5 \
  --namespace cert-manager \
  --create-namespace \
  --set installCRDs=true \
  --wait

```

## Install ArgoCD

```zsh
helm install argocd argo-cd \
  --repo https://argoproj.github.io/argo-helm \
  --version 5.46.6 \
  --namespace argocd \
  --create-namespace \
  --set 'configs.secret.argocdServerAdminPassword=$2a$10$V.Z2TW0MXeErKz9bZx70OOqqjbeJbpQ1njW9hOkwblnMSLC1ENKMi' \
  --set dex.enabled=false \
  --set notifications.enabled=false \
  --set server.service.type=NodePort \
  --set server.service.nodePortHttp=31443 \
  --wait
```

### Login info

User: admin
Pass: testKargoPass

## Install Kargo

```zsh
helm install kargo \
  oci://ghcr.io/akuity/kargo-charts/kargo \
  --namespace kargo \
  --create-namespace \
  --set api.service.type=NodePort \
  --set api.service.nodePort=31444 \
  --set api.adminAccount.password=admin \
  --set api.adminAccount.tokenSigningKey=iwishtowashmyirishwristwatch \
  --wait
  ```
  