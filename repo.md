# Prepare repository and ArgoCD

## Export variables

```zsh
source .env
```

## upload secret

```zsh
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Secret
type: Opaque
metadata:
  name: kargo-demo-repo
  namespace: argocd
  labels:
    argocd.argoproj.io/secret-type: repository
  annotations:
    kargo.akuity.io/authorized-projects: kargo-demo
stringData:
  type: git
  project: default
  url: ${GITOPS_REPO_URL}
  username: ${GITHUB_USERNAME}
  password: ${GITHUB_PAT}
EOF
```

## Create Argocd applications

```zsh
kubectl apply -f infra/app.yaml
```

