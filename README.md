# kluctl-examples

![kluctl](https://github.com/kluctl/kluctl/blob/80a09dfc6c06c5fc7002d088e213664f4e047b09/logo/kluctl.png)

kluctl is the missing glue that puts together your (and any third-party) deployments into one large declarative
Kubernetes deployment, while making it fully manageable (deploy, diff, prune, delete, ...) via one unified command
line interface.

This repository contains example configurations that show how you can use kluctl to simplify deployments and make your
platform teams happy.

# List of examples
1. [simple](simple): This example is a very simple one that shows how to define a target cluster, context, create a
namespace and deploy a nginx. You can configure the name of the namespace by changing the arg `environment` in 
[.kluctl.yml](simple/.kluctl.yml).
2. [simple-with-external-repos](simple-with-external-repos): This example is very similar to `simple` except that the 
target cluster and the deployment is defined externally. You can configure the repositories and the ref in  
[.kluctl.yml](simple-with-external-repos/.kluctl.yml).