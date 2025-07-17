## security secrets

### Encrypt your root ca locally

- Install kubeseal in your laptop
```shell
brew install kubeseal
```

- Generate the sealed secret
```shell
kubectl create secret generic kube-root-ca.crt \
  --from-file=ca.crt=${HOME}/.minikube/ca.crt \
  --namespace applications \
  --dry-run=client -o json | \
kubeseal \
  --namespace applications \
  --format yaml > kube-root-ca-sealed-secret.yaml
```