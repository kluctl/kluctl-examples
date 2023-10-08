
# SOPS integration example

## init

Prepare env:
```
kwokctl --name simple create cluster
export KUBECONFIG=$HOME/.kwok/clusters/$ENV/kubeconfig.yaml

export KLUCTL_RENDER_OUTPUT_DIR=./.build
export SOPS_AGE_KEY_FILE=$PWD/.env.age
```

For this example, age is used for sops encryption. 
Generated private key is for example attached `.env.age` in this repo (insecure) and the public part was added to `.sops.yml`:
```
age-keygen -o .env.age
```

## encrypting
sops -e --in-place secrets.yml

## editing (already encrypted file)
sops --in-place secrets.yml

## decrypt single file
sops -d secrets.yml
sops -d deployment/nginx/secret.yml
sops -d deployment/nginx/config/server.key
sops -d deployment/nginx/config/server-config.yml
```

## secrets

The `deployment/nginx/[kustomization.yml](deploy/nginx/kustomiation.yml) contains all the secrets applied:

```
resources:
  - secret.yml                                  # deploy Secret kind, name: 'certificates'

secretGenerator:
  - name: credentials
    literals:                                     # interpolation example
      - PASSWORD={{ secrets.nginx.credentials.password }}

  - name: server-config
    files:
      - ./config/server-config.yml                # (NOT IMPLEMENTED, sops encrypted file)
  - name: certificates-from-files
    files:
      - server.crt=./config/server.crt
      - server.key=./config/server.key            # (NOT IMPLEMENTED, SOPS encrypted file)

```

## apply
```
kluctl deploy -t simple --no-obfuscate --yes
```

```
❯ kubectl get secret -n simple
NAME                      TYPE     DATA   AGE
certificates              Opaque   2      53m
certificates-from-files   Opaque   2      32m
credentials               Opaque   1      53m
server-config             Opaque   2      32m
```


## review secrets
```
kubectl get secret -n simple credentials -o json | jq '.data.PASSWORD' -r | base64 -d
kubectl get secret -n simple -o json certificates | jq '.data."server.key"' -r | base64 -d
```


Mind, some variants of secretGenerator are not yet implemented or rather say are below `kluctl` level of visibility. These
secret if SOPS encrypted will not get decrypted during render:
```
kubectl get secret -n simple -o json certificates-from-files | jq '.data."server.key"' -r | base64 -d
kubectl get secret -n simple -o json server-config           | jq '.data."server-config.yml"' -r | base64 -d

```
