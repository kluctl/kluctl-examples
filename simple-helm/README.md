#Instructions

1) Add helm repo: `helm repo add bitnami https://charts.bitnami.com/bitnami`
2) Update helm repo index: `helm repo update`
3) Pull helm chart: `kluctl helm-pull`
4) Deploy it: `kluctl deploy --target simple-helm`