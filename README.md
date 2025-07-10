## security secrets

### Encrypt your root ca locally

- Get the public key for the controller running in the security namespace
```shell
kubeseal \
  --controller-name=sealed-secrets \
  --controller-namespace=security \
  --fetch-cert > pub-cert.pem
```

- Then use that key when sealing: 
```shell
kubectl create secret generic kube-root-ca.crt \
  --from-file=ca.crt=${HOME}/.minikube/ca.crt \
  --dry-run=client -o json | \
kubeseal \
  --controller-namespace security \
  --controller-name sealed-secrets \
  --cert=pub-cert.pem \
  --format yaml > sealed-secret.yaml
```