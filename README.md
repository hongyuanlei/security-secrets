## security secrets

### Encrypt your root ca locally

```shell
kubectl create secret generic kube-root-ca.crt \
  --from-file=ca.crt=${HOME}/.minikube/ca.crt \
  --dry-run=client -o json | \
kubeseal \
  --controller-namespace security \
  --controller-name sealed-secrets \
  --format yaml > sealed-secret.yaml
```