# Kargo setup

## Install Kargo CLI

```zsh
arch=$(uname -m)
[ "$arch" = "x86_64" ] && arch=amd64
curl -L -o kargo https://github.com/akuity/kargo/releases/latest/download/kargo-$(uname -s | tr '[:upper:]' '[:lower:]')-${arch}
chmod +x kargo
```

Then move kargo to a location in your file system that is included in the value of your PATH environment variable.

For macs like this:

```zsh
mv kargo /usr/local/bin/kargo
```

## Login to Kargo UI

Begin by logging into Kargo:

```zsh
kargo login https://localhost:8444 \
  --admin \
  --password admin \
  --insecure-skip-tls-verify
```


Apply Kargo manifests.

```zsh
kubectl apply -f kargo/stages.yaml
```
