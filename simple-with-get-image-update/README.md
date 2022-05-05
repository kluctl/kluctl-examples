To dynamically update image form a registry in a deployment you can use `image: "{{ images.get_image('nginx') }}"`
```yaml
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: "{{ images.get_image('nginx') }}"
          ports:
            - containerPort: 80
```
```bash
kluctl diff -t simple -u
```
output:
```
Changed objects:
  simple/Deployment/nginx-deployment

Diff for object simple/Deployment/nginx-deployment
+----------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
| Path                                   | Diff                                                                                                                              |
+----------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
| spec.template.spec.containers[0].image | -nginx:1.14.2                                                                                                                     |
|                                        | +nginx:1.21.6                                                                                                                     |
+----------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
```
