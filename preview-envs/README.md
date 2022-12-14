# preview-envs

This directory is used to demonstrate the [template-controller's](https://github.com/kluctl/template-controller)
[GitProjector](https://github.com/kluctl/template-controller/blob/main/docs/spec/v1alpha1/gitprojector.md) and related
examples.

It simply contains a few yaml files with configuration of dynamic preview environments, which are read by the
`GitProjector` and then used with an `ObjectTemplate` to create `KluctlDeployments`.
