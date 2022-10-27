# kluctl-examples

<img alt="kluctl" src="https://raw.githubusercontent.com/kluctl/kluctl/main/logo/kluctl.svg" width="200"/>

kluctl is the missing glue that puts together your (and any third-party) deployments into one large declarative
Kubernetes deployment, while making it fully manageable (deploy, diff, prune, delete, ...) via one unified command
line interface.

This repository contains example configurations that show how you can use kluctl to simplify deployments and make your
platform teams happy. For a complete description of the examples and a getting started guide take a look at 
[kluctl.io](https://kluctl.io).

# List of examples
1. [simple](simple): This example is a very simple one that shows how to define a target cluster, context, create a
namespace and deploy a nginx. You can configure the name of the namespace by changing the arg `environment` in 
[.kluctl.yml](simple/.kluctl.yml).
2. [simple-helm](simple-helm/.kluctl.yml): This example is very similar to `simple` but it deploys a Helm-based nginx to
give a first impression how kluctl and Helm work together.
3. [microservices-demo](microservices-demo): This example is a more complex one and contains the files for the
[microservices tutorial](https://kluctl.io/docs/guides/tutorials/microservices-demo/) inspired by the
[Google Online Boutique Demo](https://github.com/GoogleCloudPlatform/microservices-demo).